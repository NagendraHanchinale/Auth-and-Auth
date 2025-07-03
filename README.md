# AuthApp

A Node.js authentication and authorization API using Express, MongoDB (Mongoose), JWT, and role-based access control. This app provides user registration, login, and protected routes for different user roles (Admin, Student, Visitor).

## Features

- User registration (signup) with hashed passwords
- User login with JWT authentication
- Role-based access control (Admin, Student, Visitor)
- Protected API routes for different roles
- MongoDB integration with Mongoose
- Environment variable support with dotenv
- Cookie-based JWT storage

## Project Structure

```
.
├── .env
├── .gitignore
├── index.js
├── package.json
├── config/
│   └── database.js
├── Controllers/
│   └── Auth.js
├── middlewares/
│   └── auth.js
├── models/
│   └── User.js
└── routes/
    └── user.js
```

## Getting Started

### Prerequisites

- Node.js (v14+ recommended)
- MongoDB instance (local or cloud)

### Installation

1. Clone the repository:

    ```sh
    git clone https://github.com/NagendraHanchinale/Auth-Auth.git
    cd AuthApp
    ```

2. Install dependencies:

    ```sh
    npm install
    ```

3. Create a `.env` file in the root directory with the following variables:

    ```
    PORT=4000
    MONGODB_URL=<your-mongodb-connection-string>
    JWT_SECRET=<your-secret-key>
    ```

4. Start the server:

    ```sh
    npm run dev
    ```

    The server will run on `http://localhost:4000` by default.

## API Endpoints

All endpoints are prefixed with `/api/v1`.

### Auth Routes

- **POST `/api/v1/signup`**  
  Register a new user.  
  **Body:**  
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "yourpassword",
    "role": "Student" // or "Admin", "Visitor"
  }
  ```

- **POST `/api/v1/login`**  
  Login an existing user.  
  **Body:**  
  ```json
  {
    "email": "john@example.com",
    "password": "yourpassword"
  }
  ```
  **Response:**  
  - Sets a `token` cookie (JWT)
  - Returns user info (without password) and token

### Protected Routes

- **GET `/api/v1/test`**  
  Protected route, requires authentication.

- **GET `/api/v1/student`**  
  Protected route, requires authentication and `Student` role.

- **GET `/api/v1/admin`**  
  Protected route, requires authentication and `Admin` role.

## Main Components

- [`index.js`](index.js): Entry point, sets up Express, middleware, database connection, and routes.
- [`config/database.js`](config/database.js): Connects to MongoDB using Mongoose.
- [`models/User.js`](models/User.js): Mongoose schema/model for users.
- [`Controllers/Auth.js`](Controllers/Auth.js): Handles signup and login logic.
- [`middlewares/auth.js`](middlewares/auth.js): JWT authentication and role-based authorization middleware.
- [`routes/user.js`](routes/user.js): Defines API routes and applies middleware.

## Security Notes

- Passwords are hashed using bcrypt before storage.
- JWT tokens are signed with a secret and stored in HTTP-only cookies.
- Role-based middleware restricts access to certain routes.

---

**Author:**  
Nagendra B Hanchinale
