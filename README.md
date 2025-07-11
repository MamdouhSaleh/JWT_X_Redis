# JWT_X_Redis

# 🔐 JWT Auth System with Refresh Tokens & Redis

A robust and secure authentication system built with **Node.js**, **Express**, **JWT**, **MongoDB**, and **Redis**. Designed with production in mind — including support for **token rotation**, **session tracking**, and **access token blacklisting** using Redis.

---

## 📦 Tech Stack

- **Node.js** & **Express** – Backend runtime and framework
- **JWT (JSON Web Tokens)** – Stateless authentication
- **MongoDB** – Persistent user and session storage
- **Redis** – Fast in-memory store for token blacklisting
- **bcrypt / crypto** – Password hashing and token hashing
- **uuid** – Unique session tracking
- **dotenv** – Environment configuration

---

## ✅ Features

- 🔐 Access & Refresh Tokens with rotation
- 🧠 Session management using `sessionId` (UUID)
- 🗑️ Blacklist access tokens in Redis until expiry
- 🔐 Refresh tokens stored in secure httpOnly cookies
- 🔒 Hashed refresh tokens in MongoDB for added security
- 🧱 Modular architecture for clean code separation

---

## 🔄 Authentication Flow

1. **Login**
   - Validate credentials
   - Generate `accessToken` and `refreshToken`
   - Send `accessToken` in response, `refreshToken` in `httpOnly` cookie

2. **Accessing Protected Routes**
   - Send `accessToken` in `Authorization: Bearer ...`
   - Middleware validates the token and attaches user ID

3. **Token Refresh**
   - Client hits `/auth/refresh` with cookie and session ID
   - Server verifies token, replaces it, and returns new tokens

4. **Logout**
   - Removes refresh token from user sessions
   - Blacklists current `accessToken` in Redis

5. **Session Tracking**
   - Uses `sessionId` to track multiple device logins

6. **Access Token Blacklisting**
   - Blacklists `accessToken` in Redis on logout

---

## 🧪 API Endpoints

| Method | Endpoint         | Description                    |
|--------|------------------|--------------------------------|
| POST   | `/auth/signup`   | Register a new user            |
| POST   | `/auth/login`    | Login and receive tokens       |
| GET    | `/auth/refresh`  | Refresh access token           |
| POST   | `/auth/logout`   | Logout and invalidate session  |
| GET    | `/auth/profile`  | Protected route (test access)  |

---

## 🛡️ Security Highlights

- 🔐 Refresh tokens are hashed before storing in MongoDB
- 🔁 Refresh token rotation with session ID tracking
- 🚫 Access tokens are blacklisted in Redis on logout
- 🧠 Session-based auth supports multiple device logins
- 🧹 Redis auto-cleans expired blacklisted tokens using TTL

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git https://github.com/MamdouhSaleh/JWT_X_Redis.git
cd JWT_X_Redis
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Create a `.env` file:

```env
PORT=3000
MONGO_URI=mongodb://localhost:27017/auth-db
JWT_SECRET=your_access_secret
REFRESH_SECRET=your_refresh_secret

```

### 4. Start the server

```bash
npm start dev
```

---

## 💡 Design Philosophy

> **"Stateless doesn’t mean careless."**  
> This system aims to bring the simplicity of JWT together with the security of server-side session control and token invalidation.

It’s designed for:
- Clean architecture and modularity
- Scalability for multi-device and multi-user sessions
- Security best practices

---

## 📄 License

MIT — Free to use, modify, and share.