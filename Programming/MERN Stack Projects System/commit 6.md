# 🎯 Commit Objective

`25f8243` — **feat: implement user authentication and profile management services with Zod validation**

This commit wires together the application's first fully functional request lifecycle. It introduces the authentication pipeline — from HTTP entry point through validation, business logic, and database interaction — and establishes the layered pattern that every future resource will follow.

```text
Request
   │
   ▼
Router  (auth.routes.js)
   │
   ▼
Validation Middleware  (validate.js + auth.validation.js)
   │
   ▼
Controller  (auth.controller.js)
   │
   ▼
Service  (auth.service.js)
   │
   ▼
Database  (user.model.js)
```

---

# 📂 Files Changed

```text
server/src/
├── app.js                              ← mounted /api/v1/auth router
├── controllers/
│   └── auth.controller.js              ← NEW: register & login handlers
├── middlewares/
│   └── validate.js                     ← NEW: global Zod validation middleware
├── models/
│   └── user.model.js                   ← MODIFIED: added bcrypt hooks & comparePassword
├── routes/
│   └── auth.routes.js                  ← NEW: POST /register, POST /login
├── services/
│   ├── auth.service.js                 ← NEW: register() and login() business logic
│   └── user.services.js                ← DELETED: replaced by auth.service.js
└── validations/
    └── user.validation.js              ← minor: trailing newline fix
```

---

# 🗄️ 1. User Model — `user.model.js`

**Responsibility:** Persist users and secure their credentials.

### What changed

- Imported `bcrypt`
- Added `pre("save")` hook that hashes the password only when it is new or modified
- Added `comparePassword(plainPassword)` instance method for login verification

```js
userSchema.pre("save", async function () {
  if (!this.isModified("password")) return;
  const salt = await bcrypt.genSalt(10);
  this.password = await bcrypt.hash(this.password, salt);
});

userSchema.methods.comparePassword = async function (plainPassword) {
  return await bcrypt.compare(plainPassword, this.password);
};
```

> [!NOTE]
> `password` has `select: false` on the schema — it is never returned in query results unless explicitly opted in with `.select('+password')`.

---

# ✅ 2. Validation Middleware — `validate.js`

**Responsibility:** Parse and validate every incoming request against a Zod schema before it reaches a controller.

```js
export const validateSchema = (schema) => {
    return (req, res, next) => {
        const result = schema.safeParse({
            body: req.body,
            query: req.query,
            params: req.params
        });

        if (!result.success) {
            return next(new AppError(result.error.issues[0].message, 400));
        }

        // Validated & parsed data attached — never mutates req.body
        req.validatedData = result.data;
        next();
    };
};
```

> [!IMPORTANT]
> Validated data is stored on `req.validatedData`, **not** by overwriting `req.body`. Controllers must read from `req.validatedData.body`, `req.validatedData.params`, etc.

### Validation schemas used — `user.validation.js`

| Schema | Validates | Used by |
|---|---|---|
| `createNewUserSchema` | `username`, `email`, `password` (regex strength check) | `POST /register` |
| `loginUserSchema` | `username`, `password` | `POST /login` |
| `updateUserSchema` | all profile fields (all optional) | future `PATCH /me` |
| `userIdSchema` | `params.id` as a 24-char hex ObjectId | future `GET /users/:id` |

---

# 🧠 3. Auth Service — `auth.service.js`

**Responsibility:** All authentication business logic. Never touches `req`, `res`, or `next`.

### `register(userData)`

1. Destructures `email` and `username` from the incoming data
2. Checks for conflicts using `$or` — blocks both duplicate email **and** duplicate username in a single query
3. Creates the user (password is hashed automatically by the model hook)
4. Signs a JWT containing `{ id, role }`
5. Returns `{ token, user }`

```js
const user = await User.findOne({ $or: [{ email }, { username }] });
if (user) throw new AppError('User with this email or username already exists', 409);
```

### `login({ email, password })`

1. Finds the user by email with `select('+password')` to opt into the hidden field
2. Uses generic `'Invalid Credentials'` for both "not found" and "wrong password" (prevents user enumeration)
3. Verifies password via `user.comparePassword(password)`
4. Signs and returns a JWT

> [!IMPORTANT]
> Both `register` and `login` return `{ token, user }`. The token is currently included in the JSON response body. Consider moving it to an `HttpOnly` cookie in a future commit to protect against XSS.

---

# 🎮 4. Controller — `auth.controller.js`

**Responsibility:** Translate HTTP requests into service calls. Thin layer — no business logic.

```js
export const registerController = asyncHandler(async (req, res) => {
    const { body } = req.validatedData;        // reads validated, parsed data
    const { token, user } = await register(body);
    res.status(201).json({ status: 'success', message: 'User registered successfully', user, token });
});

export const loginController = asyncHandler(async (req, res) => {
    const { body } = req.validatedData;
    const { token, user } = await login(body);
    res.status(200).json({ status: 'success', message: 'User logged in successfully', user, token });
});
```

> [!NOTE]
> `asyncHandler` wraps each handler and forwards any thrown `AppError` to the global error middleware automatically — no try/catch needed, no `next` parameter.

---

# 🌐 5. Routes — `auth.routes.js`

**Responsibility:** Define endpoints and compose their middleware chain.

```js
router.post("/register", validate(registerSchema), registerController);
router.post("/login",    validate(loginSchema),    loginController);
```

Middleware order per route:

```text
validate()     ← rejects invalid payloads before they hit the service
    ↓
Controller     ← calls service, sends response
```

---

# 🔗 6. Route Registration — `app.js`

```js
import authRoutes from "./routes/auth.routes.js"

app.use("/api/v1/auth", authRoutes)
```

| Method | Full URL | Handler |
|---|---|---|
| `POST` | `/api/v1/auth/register` | `registerController` |
| `POST` | `/api/v1/auth/login` | `loginController` |

---

# 🧹 Cleanup

- Deleted `server/src/services/user.services.js` — a leftover stub file with only imports and no logic. Its responsibilities are now properly split between `auth.service.js` and `user.service.js`.
- Deleted `controllers/.gitkeep` and `routes/.gitkeep` — placeholder files no longer needed now that real files exist.

---

# 🧪 Test Scenarios

Before moving to the next resource, verify each endpoint.

## `POST /api/v1/auth/register`

| Scenario | Expected |
|---|---|
| Valid `username`, `email`, `password` | `201` — `{ status, message, user, token }` |
| Duplicate email | `409` — `'User with this email or username already exists'` |
| Duplicate username | `409` — `'User with this email or username already exists'` |
| Missing `email` | `400` — Zod validation message |
| Weak password (no special char, etc.) | `400` — regex validation message |

## `POST /api/v1/auth/login`

| Scenario | Expected |
|---|---|
| Valid `email` + `password` | `200` — `{ status, message, user, token }` |
| Unknown email | `401` — `'Invalid Credentials'` |
| Wrong password | `401` — `'Invalid Credentials'` |
| Missing fields | `400` — Zod validation message |

---

# 📋 Commit Checklist

- [x] Added `bcrypt` import to `user.model.js`
- [x] Fixed `pre("save")` to check `isModified("password")` (not `passwordHash`)
- [x] Added `comparePassword(plainPassword)` instance method
- [x] Created Zod validation schemas (`createNewUserSchema`, `loginUserSchema`, `updateUserSchema`, `userIdSchema`)
- [x] Created global `validate()` middleware that attaches parsed data to `req.validatedData`
- [x] Implemented `register()` service with duplicate check via `$or` query
- [x] Implemented `login()` service with generic error messages to prevent user enumeration
- [x] Created thin `auth.controller.js` reading from `req.validatedData`
- [x] Created `auth.routes.js` composing `validate → controller`
- [x] Registered `authRoutes` at `/api/v1/auth` in `app.js`
- [x] Deleted stale `user.services.js` stub
- [ ] Test all endpoints (Register / Login)
- [ ] Commit the completed feature

---

# 🏗️ Next Steps

Every future resource follows this exact flow:

```text
ERD
    ↓
Model
    ↓
Validation (Zod schemas)
    ↓
Service (business logic only)
    ↓
Controller (thin HTTP layer)
    ↓
Routes (compose middleware chains)
    ↓
Register in app.js
    ↓
Test every endpoint
```

Apply this blueprint next for: **User Profile**, **Movies**, **Clubs**, **Reviews**, **Watchlists**.
