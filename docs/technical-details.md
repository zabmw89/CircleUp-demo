# Technical Details

## API Design

CircleUp exposes REST-style endpoints under `/api`.

The API is organized around application resources:

- Authentication
- Users
- Profiles
- Posts
- Comments
- Likes
- Follows

HTTP methods communicate the intended operation:

```text
GET     → retrieve
POST    → create / perform an action
PUT     → update
DELETE  → remove
```

## Authentication

Authentication uses:

- `bcryptjs` for password hashing
- JSON Web Tokens (JWT) for authenticated API access

Protected routes use authentication middleware before allowing access to protected resources.

Authorization is also applied to user-owned resources so that operations such as editing or deleting content are associated with the appropriate account.

## Validation & Middleware

The backend includes middleware for:

- Authentication
- Request validation
- Error handling
- Security-related request processing

This provides a consistent place to handle cross-cutting backend concerns.

## Security Measures

The application includes:

- Helmet security headers
- CORS configuration
- Express rate limiting
- Password hashing
- JWT authentication
- Authorization checks
- Request validation
- Environment-based configuration
- Upload handling

These measures are valuable for a learning and portfolio application, but they do not by themselves make the application production-ready.

## Testing

Jest and Supertest are used for automated API testing.

The tests focus on application workflows rather than only isolated functions, including authentication, authorization, posts, comments, likes, follows, and feed behavior.

## Development Data

Two seed workflows are available in the original application:

```bash
npm run seed
npm run seed:demo
```

The demo seed is intended for portfolio demonstrations and local development.

## Local Development

The original application expects:

- Node.js 18+
- npm 9+
- SQLite
- A local environment configuration

Typical commands:

```bash
npm install
npm run seed
npm start
```

Development mode:

```bash
npm run dev
```

Tests:

```bash
npm test
```

## Production Considerations

The project README explicitly identifies areas requiring additional hardening before public production use:

- HTTPS / TLS
- Secret management
- JWT storage and expiration strategy
- CORS configuration
- Rate-limit tuning
- Upload restrictions and storage
- Database backups
- Logging and monitoring
- Dependency maintenance
- Reverse-proxy configuration
- Production error handling
- Secure cookie configuration if cookies are adopted

This distinction is intentional: a strong portfolio project should communicate both what has been implemented and what would still be required for production.
