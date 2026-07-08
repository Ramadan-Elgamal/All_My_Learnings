
### 1. The Authentication Flow (Identity Verification)

This is the lifecycle of how a user logs into the SmartCare ICU platform and maintains their session securely.

1. **Login Request:** The user submits their credentials (email and password) via the React frontend.
    
2. **Backend Verification:** The Express/Node.js backend receives the request and verifies the credentials against the user records in MongoDB.
    
3. **Token Generation:** If valid, the backend generates a **JSON Web Token (JWT)**. The payload of this token must include the user's `id` and their specific `role` (e.g., `role: "Nurse"`).
    
4. **Token Delivery:** The server sends the JWT back to the client. (For healthcare apps, it is highly recommended to store this in an `HttpOnly` cookie to prevent Cross-Site Scripting (XSS) attacks, rather than in `localStorage`).
    
5. **Authenticated Requests:** For every subsequent action, the React frontend automatically sends this token. The backend verifies the token's validity before processing the request.
    

### 2. The Authorization Flow (Role-Based Access Control)

Once the user is authenticated, the backend must enforce strict boundaries on what they are allowed to see and modify. In an Express backend, this is handled via **Middleware functions** that check the `role` attached to the user's JWT before allowing the request to hit the database.

Here is the exact mapping of who can see and do what across the platform:

#### Access Control Matrix

| **Feature / Action**            | **System Admin** | **ICU Nurse** | **Medical Resident** | **ICU Specialist** |
| ------------------------------- | ---------------- | ------------- | -------------------- | ------------------ |
| **Manage Users & Roles**        | ✅ Yes            | ❌ No          | ❌ No                 | ❌ No               |
| **Create Patient Profile**      | ❌ No             | ✅ Yes         | ✅ Yes                | ✅ Yes              |
| **Input Vitals & Metrics**      | ❌ No             | ✅ Yes         | ✅ Yes                | ✅ Yes              |
| **Upload Radiology & PDFs**     | ❌ No             | ✅ Yes         | ✅ Yes                | ✅ Yes              |
| **Write Medical History**       | ❌ No             | ❌ No          | ✅ Yes                | ✅ Yes              |
| **View Patient Dashboard**      | ❌ No (Privacy)   | ✅ Yes         | ✅ Yes                | ✅ Yes              |
| **Query RAG System (Chat)**     | ❌ No             | ❌ No          | ✅ Yes                | ✅ Yes              |
| **Trigger AI Summarization**    | ❌ No             | ❌ No          | ✅ Yes                | ✅ Yes              |
| **Approve Treatment/Discharge** | ❌ No             | ❌ No          | ❌ No                 | ✅ Yes              |
