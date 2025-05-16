# user-auth-system
Backend-only user authentication with Node.js, Express, MongoDB

- New user registration
- Existing user login 
- Accessing of user data (Protected)

Step by Step:

1. User Registration:

User sends POST /api/auth/register request:

{
  "username": "example",
  "email": "example@example.com",
  "password": "123456"
}

Server:

- Checks if email is already in use
- Hashes password using bcrypt
- Stores the new user in MongoDB

2. User Login:

The user sends a POST /api/auth/login request:

{
  "email": "example@example.com",
  "password": "123456"
}

Server:

- Looks up the user by email
- Compares the entered password with the stored hashed password
- If correct, a JWT token is generated, returning:

{
  "token": "jwt.token.here",
  "user": {
    "id": "...",
    "username": "...",
    "email": "..."
  }
}

3. User Accessing Protected Route:

The client sends a GET /api/auth/profile request:
Request includes a JWT token

Server:

- Uses middleware (auth.js) to verify the JWT token
- If valid, allows access to the route and returns the user's profile data


Security Features:

- Passwords are never stored as plain text - salted and hashed
- Tokens are signed using a secret key and expire after 1 hour
- Protected routes are only accessible if valid token is provided
- Sensitive values are stored in an .env file and ignored via .gitignore



Tech Stack:

Runtime - Node.js
Server - Express.js
Database - MongoDB
Auth - bcrypt + JWT
Config - dotenv
Testing Tool - Postman