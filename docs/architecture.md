# Architecture

## High-Level Design

CircleUp is organized as a conventional full-stack web application:

```text
Browser
   │
   │ HTML / CSS / JavaScript
   ▼
Frontend
   │
   │ Fetch API
   ▼
REST API
   │
   ▼
Express.js
   │
   ├── Authentication Middleware
   ├── Validation Middleware
   ├── Error Handling
   └── Controllers
        │
        ├── Auth
        ├── Users
        ├── Posts
        ├── Comments
        ├── Likes
        └── Follows
        │
        ▼
   SQLite / better-sqlite3
```

## Backend Organization

The original application separates backend responsibilities into several areas:

```text
backend/
├── config/
│   ├── database.js
│   └── multer.js
├── controllers/
│   ├── authController.js
│   ├── userController.js
│   ├── postController.js
│   ├── commentController.js
│   ├── likeController.js
│   └── followController.js
├── middleware/
│   ├── auth.js
│   ├── errorHandler.js
│   └── validator.js
├── routes/
│   ├── authRoutes.js
│   ├── userRoutes.js
│   ├── postRoutes.js
│   └── commentRoutes.js
└── server.js
```

This separation helps keep routing, request processing, application logic, and infrastructure concerns distinct.

## Frontend Organization

The frontend uses standard web technologies:

```text
frontend/
├── index.html
├── login.html
├── register.html
├── profile.html
├── post.html
├── css/
└── js/
```

The browser communicates with the backend using the Fetch API.

## Database Model

SQLite provides relational persistence for local development.

```text
Users
 │
 ├──────── Profiles
 │
 ├──────── Posts
 │             │
 │             ├──── Comments
 │             └──── Likes
 │
 └──────── Follows
```

This structure models the major relationships in a social platform while allowing database constraints to protect relationship integrity.

## Authentication Flow

At a high level:

```text
User
 │
 ├── Register/Login
 │
 ▼
Backend
 │
 ├── Validate request
 ├── Verify/hash password
 └── Issue JWT
 │
 ▼
Authenticated client
 │
 └── Sends authenticated requests
        │
        ▼
   Protected API route
        │
        ▼
   Authorization check
        │
        ▼
      Resource
```

## File Upload Flow

Profile avatars and post images are handled through Multer-based upload processing.

For production deployment, file storage would need additional controls such as strict file validation, size limits, secure storage, access control, monitoring, and backup strategy.
