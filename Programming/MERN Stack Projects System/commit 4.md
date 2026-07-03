
## Commit 4: "feat: implement JWT-based authentication and role-based access control middleware"
---

## 📦 1. Core Dependency Installation

- Run these commands to install the JWT library

```bash
# Install JSON Web Token library
npm install jsonwebtoken
```

---

## 🔑 2. The Stateless Auth Utility (`src/utils/jwt.js`)

- Create `src/utils/jwt.js` to encapsulate token generation and verification.

```js
import jwt from "jsonwebtoken"
import { AppError } from "./AppError"

const getSecret = () => {
  const secret = process.env.JWT_SECRET
  if (!secret) {
    throw new Error(
      "❌ CRITICAL: JWT_SECRET is not defined in environment variables."
    )
  }
  return secret
}

// ==========================================
// 1. ISSUE TOKEN
// ==========================================
export const signToken = (payload) => {
  return jwt.sign(payload, getSecret(), {
    expiresIn: process.env.JWT_EXPIRES_IN || "1d", // Default to 1 day expiration
  })
}

// ==========================================
// 2. VERIFY TOKEN
// ==========================================
export const verifyToken = (token) => {
  try {
    return jwt.verify(token, getSecret())
  } catch (error) {
    // Return a clean, operational 401 Unauthorized error if the token is tampered/expired
    throw new AppError(
      "Invalid or expired authentication token. Please log in again.",
      401
    )
  }
}
```

---

## 🛡️ 3. The Authentication Guard (`src/middlewares/auth.middleware.js`)

- Create `src/middlewares/auth.middleware.ts`.

```js
import { verifyToken } from "../utils/jwt";
import { AppError } from "../utils/AppError";

export const requireAuth = (req, res, next) => {

    //get the auth header
    const header = req.headers.authorization

    if(!header || !header.startsWith("Bearer ")) {
        throw new AppError("Unauthorized", 401)
    }

    //get the token
    const token = header.split(' ')[1]

    //verify the token
    try {
        const decodedPayload = verifyToken(token)

        req.user = decodedPayload

        next()
    } catch (error) {
        next(error)
    }
}
```

---

## 🛑 4. Role-Based Access Control (`src/middlewares/role.middleware.js`)

- Create `src/middlewares/role.middleware.ts`.

This is a higher-order middleware factory. It inspects the `req.user` object attached by `requireAuth` and rejects access if the user's role does not match the permitted list.

```js
import { AppError } from "../utils/AppError"

export const requireRole = (allowedRoles) => {
  return (req, res, next) => {
    // Safety check: Ensure requireAuth ran first
    if (!req.user) {
      return next(
        new AppError("Authentication required before verifying roles.", 401)
      )
    }

    // Verify if the user's role exists inside the allowed array
    if (!allowedRoles.includes(req.user.role)) {
      return next(
        new AppError(
          "Forbidden: You do not have the required permissions to perform this action.",
          403
        )
      )
    }

    next()
  }
}
```

---

## 🔗 5. Blueprint Implementation Example

- Here is exactly how you apply these guards to your route dictionaries (e.g., inside `src/routes/user.routes.js` or any feature router).

```tsx
import { Router } from "express"
import { requireAuth } from "../middlewares/auth.middleware"
import { requireRole } from "../middlewares/role.middleware"
// Placeholder imports for feature controllers
// import { getProfile, getAllUsers, deleteUser } from '../controllers/user.controller';

const router = Router()

// ==========================================
// 1. PUBLIC ROUTES (No guards)
// ==========================================
// router.post('/login', loginController);

// ==========================================
// 2. PROTECTED ROUTES (Requires valid JWT)
// ==========================================
// Any route defined below this middleware requires authentication
router.use(requireAuth)

// Example: GET /api/v1/users/me -> Only accessible to authenticated users
// router.get('/me', getProfile);

// ==========================================
// 3. RESTRICTED ROUTES (Requires specific roles)
// ==========================================
// Example: GET /api/v1/users -> Only accessible if req.user.role === 'admin'
// router.get('/', requireRole(['admin']), getAllUsers);

// Example: DELETE /api/v1/users/:id -> Only admin
// router.delete('/:id', requireRole(['admin']), deleteUser);

export default router
```