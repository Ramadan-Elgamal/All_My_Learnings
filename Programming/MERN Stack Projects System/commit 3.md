## Commit 3: "feat: initialize server project with Express, MongoDB, and global error handling infrastructure"
### 1. update the backend `package.json` to enable ES Modules and add the Nodemon development script.

```json
{
  "type": "module",
  "scripts": {
    "dev": "nodemon src/server.js"
  }
}
```

### 🛡️2. Error Handling Infrastructure

- **`src/utils/AppError.js`** — Custom error class extending `Error` with `statusCode` and `isOperational` flag

```js
export class AppError extends Error {
  statusCode
  isOperational  

  constructor(message, statusCode) {
    super(message)
    this.statusCode = statusCode

    // Flagging this as 'true' means we expected this error might happen.
    // Untrusted/unhandled errors (like third-party package crashes) won't have this flag.
    this.isOperational = true

    // Capture the stack trace, excluding the constructor call from it
    Error.captureStackTrace(this, this.constructor)
  }
}
```

- **`src/utils/asyncHandler.js`** — Wrapper to eliminate try/catch boilerplate in async route handlers

```js
export const asyncHandler = (fn) => {
  return (req, res, next) => {
    Promise.resolve(fn(req, res, next)).catch(next)
  }
}
```

- **`src/middlewares/error.middleware.js`** — Global error handler: differentiates operational vs unexpected errors, standardized JSON error responses, stack trace logging in development
```js
import { AppError } from "../utils/AppError.js"

export const errorHandler = (err, req, res, next) => {
  let statusCode = 500
  let message = "Internal Server Error"

  // 1. Check if the error is our custom AppError
  if (err instanceof AppError) {
    statusCode = err.statusCode
    message = err.message
  }

  // 2. Secure Logging Strategy
  console.error(`[Error] ${statusCode} - ${message}`)


  // If it's NOT an operational error (it's an unexpected bug), log the full stack trace
  if (!("isOperational" in err) || !err.isOperational) {
    console.error("🚨 CRITICAL UNEXPECTED BUG:", err.stack)
  }

  // 3. Send Standardized JSON Response
  res.status(statusCode).json({
    status: "error",
    message,

    // Optional: Only leak full stack traces to the client if we are running locally
    ...(process.env.NODE_ENV === "development" && { stack: err.stack }),
  })
}
```

#### 🗄️ Database

- **`src/config/db.js`** — MongoDB connection via Mongoose with retry logic and graceful shutdown handling
```js
import mongoose from "mongoose"

const connectDB = async () => {
  const mongoURI = process.env.MONGO_URI
  
  // ==========================================
  // 1. FAIL-FAST VALIDATION
  // ==========================================
  if (!mongoURI) {
    console.error(
      "❌ CRITICAL: MONGO_URI is not defined in the environment variables."
    )
    process.exit(1) // Kill the container immediately
  }

  try {
    // ==========================================
    // 2. INITIAL CONNECTION
    // ==========================================
    const conn = await mongoose.connect(mongoURI)
    console.log(`📦 MongoDB Connected successfully: ${conn.connection.host}`)

    // ==========================================
    // 3. LIFECYCLE EVENT MONITORS
    // ==========================================
    // Attached AFTER initial boot to catch runtime drops (network blips, server restarts)
    mongoose.connection.on("disconnected", () => {
      console.warn(
        "⚠️ MongoDB Disconnected! API may fail to process incoming reads/writes."
      )
    })  

    mongoose.connection.on("error", (err) => {
      console.error(`❌ MongoDB Runtime Connection Error: ${err}`)
    })
  } catch (error) {
    console.error(
      `❌ Initial MongoDB Connection Failed: ${error.message}`
    )
    process.exit(1)
  }
}  

export default connectDB
```

#### 2. 🚀 Server Entry Points

- **`src/server.js`** — Bootstrap file: connects to DB first, then starts the HTTP listener with fail-fast error handling
```js
import app from "./app.js"
import connectDB from "./config/db.js"

const PORT = process.env.PORT || 3000

const startServer = async () => {
  try {
    // ==========================================
    // 1. INFRASTRUCTURE BOOTSTRAP
    // ==========================================
    await connectDB();

    // ==========================================
    // 2. START NETWORK LISTENER
    // ==========================================
    app.listen(PORT, () => {
      console.log(`🚀 Server is running on http://localhost:${PORT}`)
    })
  } catch (error) {
    // Fail-fast: If infrastructure fails to boot, kill the container immediately
    console.error("❌ Critical failure during server startup:", error)
    process.exit(1)
  }
}

startServer()
```

- **`src/app.js`** — Express app configuration: global middlewares (JSON, CORS, Helmet), health check route (`GET /health`), 404 catch-all handler, and global error middleware
```js
import express from "express"
import cors from "cors"
import helmet from "helmet"
import dotenv from "dotenv"
import { errorHandler } from "./middlewares/error.middleware.js"
import { AppError } from "./utils/AppError.js"

dotenv.config()
const app = express()

// ==========================================
// 1. GLOBAL MIDDLEWARES
// ==========================================
app.use(express.json())
app.use(cors())
app.use(helmet())

// ==========================================
// 2. HEALTH CHECK (Universal / Repeated)
// ==========================================
// Required by hosting platforms (AWS, Render, etc.) to verify container health
app.get("/health", (req, res) => {
  res.status(200).json({
    status: "success",
    message: "API is running normally.",
    timestamp: new Date().toISOString(),
  })
})

// ==========================================
// 3. FEATURE ROUTES (App-Specific Placeholders)
// ==========================================
// STEP 2: Import your feature routers here
// Example: import userRoutes from './routes/user.routes';

// STEP 3: Mount the routers to their base API paths
// Example: app.use('/api/v1/users', userRoutes);

// ==========================================
// 4. GLOBAL ERROR HANDLING (Configured in Phase 6)
// ==========================================
app.all("/{*path}", (req, res, next) => {
  next(
    new AppError(
      `Cannot find ${req.method} ${req.originalUrl} on this server.`,
      404
    )
  )
})

app.use(errorHandler)

export default app
```


#### 🔒 Security & Config

- **`server/.gitignore`** — Excludes `node_modules/`, `.env.local`, `.env.example`
```
node_modules/
.env.example
.env.local
.env
```

- **`server/.env`** — Environment variables file (tracked as empty placeholder)
```.env
MONGO_URI=mongodb://localhost:27017/

NODE_ENV=development

  

PORT=5000
```