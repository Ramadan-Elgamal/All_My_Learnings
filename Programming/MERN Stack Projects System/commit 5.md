# 🎯 Commit Objective

Create the project's first complete feature module.

This commit introduces the application's layered architecture:

```text
Request
   │
   ▼
Router
   │
   ▼
Validation Middleware
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Database
```

By the end of this commit, the User module will support authentication endpoints and serve as the template for every future resource.

---

# 📂 Folder Structure

```text
src/
└── features/
    └── users/
        ├── controllers/
        │   └── user.controller.js
        ├── models/
        │   └── user.model.js
        ├── routes/
        │   └── user.routes.js
        ├── services/
        │   └── user.service.js
        └── validations/
            └── user.validation.js
```

---

# 🗄️ 1. User Model

- **File:** `src/features/users/models/user.model.js`
- **Type:** Feature Layer
- **Responsibility:**

Create the Mongoose schema responsible for persisting users.

The model should contain:

- username
- email
- password
- role
- bio
- avatar
- top_four_movies
- clubs

Additional responsibilities:

- timestamps
- password hashing using `pre("save")`
- password comparison instance method
- hide password by default (`select: false`)

```js
import mongoose from "mongoose";

const userSchema = new mongoose.Schema({
    username: {
        type: String,
        required: true,
        unique: true,
        trim: true
    },
    email: {
        type: String,
        required: true,
        unique: true,
        trim: true
    },
    password: {
        type: String,
        required: true,
        select: false
    },
    role: {
        type: String,
        enum: ["USER", "ADMIN"],
        default: "USER"
    },
    bio: {
        type: String,
        default: ""
    },
    avatar: {
        type: String,
        default: ""
    },
    top_four_movies: [
        {
            type: mongoose.Schema.Types.ObjectId,
            ref: "Movie"
        }
    ],
    clubs: [
        {
            type: mongoose.Schema.Types.ObjectId,
            ref: "Club"
        }
    ]
}, {
    timestamps: true
});

userSchema.pre("save", async function () {
  // Only run hashing costs if the password field was actually modified or is brand new
  if (!this.isModified("passwordHash")) {
    return
  }

  const salt = await bcrypt.genSalt(10)
  this.password = await bcrypt.hash(this.password, salt)
})

userSchema.methods.comparePassword = async function () {
    return await bcrypt.compare(plainPassword, this.password)
}

export default mongoose.model("User", userSchema);
```

---

# ✅ 2. Request Validation

- **File:** `src/features/users/validations/user.validation.js`
- **Type:** Feature Layer

Create all request validation schemas using Zod.

Schemas:

```text
registerSchema

loginSchema

updateProfileSchema

userIdSchema
```

Validation should cover:

- req.body
- req.params
- req.query (when applicable)

These schemas will be consumed by the global `validate()` middleware.

```js
import * as z from 'zod'

export const createNewUserSchema = z.object({
    body: z.object({
        username: z.string().min(2, 'Username must be at least 2 characters').max(30, 'Username must be less than 30 characters'),
        email: z.string().email('Invalid email address'),
        password: z.string().regex(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/, 'Password must be at least 8 characters long and contain at least one uppercase letter, one lowercase letter, one number, and one special character'),
    })
})

export const updateUserSchema = z.object({
    body: z.object({
        username: z.string().min(2, 'Username must be at least 2 characters').max(30, 'Username must be less than 30 characters').optional(),
        email: z.string().email('Invalid email address').optional(),
        bio: z.string().optional(),
        avatar: z.url('Invalid avatar URL').optional(),
        role: z.enum(['USER', 'ADMIN']).default('USER'),
        top_four_movies: z.array(z.string()).optional(),
        clubs: z.array(z.string()).optional()
    })
})

export const loginUserSchema = z.object({
    body: z.object({
        username: z.string().min(2, 'Username must be at least 2 characters').max(30, 'Username must be less than 30 characters'),
        password: z.string().regex(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/, 'Password must be at least 8 characters long and contain at least one uppercase letter, one lowercase letter, one number, and one special character'),
    })
})

export const userIdSchema = z.object({
    params: z.object({
        id: z.string().regex(/^[0-9a-fA-F]{24}$/, 'Invalid user ID format')
    })
})


```

---

# 🧠 3. Business Service

- **File:** `src/features/users/services/user.service.js`
- **Type:** Feature Layer

The service contains **business logic only**.

It must never access:

- req
- res
- next

Initial services:

```text
register()

login()

getProfile()

updateProfile()

deleteAccount()
```

Responsibilities include:

- querying MongoDB
- generating JWTs
- verifying credentials
- enforcing business rules

```js
import { AppError } from "../utils/AppError.js"
import User from "../models/user.model.js"

//Authentication services
//logout()
//refreshToken()
//forgotPassword()
//resetPassword()
//changePassword()
//verifyEmail()

const registerUser = async (userData) => {

    //create the user
    const newUser = await User.create(userData);

    //generate token
    const token = signToken({
        id: newUser._id,
        role: newUser.role
    });

    //return the data to the controller
    return {
        token,
        user: newUser
    }
}

const loginUser = async ({email, password}) => {
    //check if the user exist in the database
    const user = await User.findOne({ email }).select('+password')

    //check if the user exist
    if(!user) {
        throw new AppError('User not found', 404)
    }

    //compare the password
    const isPasswordValid = await user.comparePassword(password)

    if(!isPasswordValid){
        throw new AppError('Invalid password', 401)
    }

    //generate token
    const token = signToken({
        id: user._id,
        role: user.role
    })

    //return the data to the controller
    return {
        token,
        user
    }
}

//User Profile Service
// getProfile()
// updateProfile()
// deleteAccount()


//Public User Service
// getUserById()
// getUsers()

//Favorite Movies Service
// getFavoriteMovies()
// addFavoriteMovie()
// removeFavoriteMovie()
//clearFavoriteMovies()

//Movie Club Service
// getClubs()
// getClub()
// createClub()
// joinClub()
// leaveClub()
// deleteClub()



//export all services
export {
    registerUser,
    loginUser
}
```

---

# 🎮 4. Controller

- **File:** `src/features/users/controllers/user.controller.js`
- **Type:** Feature Layer

Controllers translate HTTP requests into service calls.

Responsibilities:

- receive validated request data
- call the appropriate service
- send HTTP responses

Controllers should remain thin and contain little to no business logic.

---

# 🌐 5. Routes

- **File:** `src/features/users/routes/user.routes.js`
- **Type:** Feature Layer

Define all API endpoints.

Example structure:

```text
POST   /register

POST   /login

GET    /me

PATCH  /me

DELETE /me
```

Each endpoint should compose middleware in the following order:

```text
Validation
        ↓
Authentication (when required)
        ↓
Authorization (when required)
        ↓
Controller
```

---

# 🔗 6. Register the Routes

Inside `src/app.js`

```js
import userRoutes from "./features/users/routes/user.routes.js"

app.use("/api/users", userRoutes)
```

---

# 🧪 7. Test Every Endpoint

Before moving to another resource, verify each endpoint using:

- Bruno
- Postman
- Insomnia

Test scenarios should include:

## Register

- successful registration
- duplicate username
- duplicate email
- invalid request body

---

## Login

- successful login
- invalid email
- invalid password

---

## Profile

- authenticated request
- missing token
- invalid token
- expired token

---

# 📋 Feature Flow Checklist

- [ ] Create the User model.
- [ ] Add password hashing middleware.
- [ ] Add password comparison method.
- [ ] Create Zod validation schemas.
- [ ] Implement User service.
- [ ] Implement User controller.
- [ ] Create feature routes.
- [ ] Register routes inside `app.js`.
- [ ] Test every endpoint.
- [ ] Commit the completed feature.

---

# 🏗️ Resource Development Blueprint

Every future resource in the project should follow the exact same implementation flow.

```text
ERD
    ↓
Model
    ↓
Validation
    ↓
Service
    ↓
Controller
    ↓
Routes
    ↓
Register Routes
    ↓
Testing
```

This blueprint should be repeated for Movies, Clubs, Reviews, Watchlists, and every future feature module.