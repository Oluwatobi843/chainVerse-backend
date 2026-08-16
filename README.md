# ChainVerse Backend

> Scalable, modular backend infrastructure for ChainVerse Academy, a Web3 education platform.

## Overview

ChainVerse Backend is a NestJS-based backend that supports a multi-role learning platform with course management, learner progress, certifications, gamification, financial aid, organizations, subscriptions, notifications, reporting and moderation.

The project represents an architectural migration from Express.js to NestJS. The migration focuses on clear domain boundaries, dependency injection, maintainability, testability and a foundation that can evolve toward distributed services.

## Key capabilities

- Multi-role authentication and account management
- JWT access and refresh-token authentication
- Role-based access control
- Organization-scoped authorization
- Course creation, discovery and enrollment workflows
- Reviews, ratings and feedback
- Gamification, points, achievements and leaderboards
- Certificate generation and verification
- Financial-aid applications and review workflows
- Reporting and analytics
- Notifications and communication workflows
- Organization management
- Subscription plans
- Sessions and session tracking
- Abuse reporting and moderation
- Audit logging
- Upload quarantine/security controls

## Technology stack

| Layer | Technology |
|---|---|
| Framework | NestJS |
| Language | TypeScript |
| Database | MongoDB |
| ODM | Mongoose |
| Authentication | JWT / Passport-based authentication |
| Validation | class-validator / class-transformer |
| Cache | Redis |
| API documentation | Swagger / OpenAPI |
| Storage | Local / S3-compatible storage |
| Testing | Jest / Supertest |
| Containerization | Docker |
| CI/CD | GitHub Actions |

## Architecture

The backend uses a feature-based modular architecture. Each business domain is isolated into a NestJS module with controllers, services, DTOs and persistence models.

```text
                         Client Applications
                                |
                                v
                         NestJS REST API
                                |
        +-----------------------+-----------------------+
        |                       |                       |
        v                       v                       v
 Authentication            Domain Modules         Common Services
        |                       |                       |
        |              +--------+--------+              |
        |              |        |        |              |
        |           Courses  Users   Organizations      |
        |              |        |        |              |
        |              +--------+--------+              |
        |                       |                       |
        +-----------------------+-----------------------+
                                |
                    +-----------+-----------+
                    |                       |
                    v                       v
                 MongoDB                  Redis
```

## Domain modules

The codebase is organized around domains including:

```text
src/
├── auth/
├── users/
├── tutor-settings/
├── student-settings/
├── admin-settings/
├── courses/
├── reviews/
├── leaderboard/
├── gamification/
├── certification/
├── financial-aid/
├── reports/
├── notification/
├── organization/
├── subscription-plan/
├── session/
└── common/
```

A typical module follows the separation:

```text
module/
├── module.module.ts
├── module.controller.ts
├── module.service.ts
├── dto/
├── entities/
└── guards/
```

### Architectural principles

- Separation of concerns
- Dependency injection
- Single Responsibility Principle
- Domain-oriented modules
- Thin controllers
- Business logic in services
- DTO-based validation
- Reusable shared utilities

## Authentication and authorization

### JWT authentication

The API uses access and refresh tokens to support authenticated sessions.

```text
Login
  |
  v
Credential validation
  |
  +----> Access token
  |
  +----> Refresh token
          |
          v
     Token refresh
```

### Platform roles

- `ADMIN`
- `MODERATOR`
- `TUTOR`
- `STUDENT`

### Organization roles

Organizations use a separate permission axis:

- `owner`
- `admin`
- `instructor`
- `member`

Organization membership is scoped to the individual organization, preventing a role in one organization from automatically granting privileges in another.

### Guards

- `JwtAuthGuard` — validates authenticated users
- `RolesGuard` — enforces platform-level roles
- `OrganizationRolesGuard` — enforces organization membership permissions

## Security

Security is treated as a cross-cutting concern rather than an afterthought.

The repository includes documentation and implementation around:

- Immutable audit logging
- Organization-scoped authorization
- Protected uploads
- Upload quarantine/malware scanning
- DTO validation
- Authentication guards
- Secret management through environment configuration
- Protected privileged operations

## Core feature areas

### Users and identity

Supports user accounts and role-specific settings for students, tutors, administrators and moderators.

### Courses

Provides the foundation for course creation, categorization, discovery, enrollment, reviews and analytics.

### Gamification

Includes points, achievements, badges and leaderboard concepts designed to improve learner engagement.

### Certifications

Supports certificate generation, verification and controlled certificate-related workflows.

### Financial aid

Provides an application lifecycle for learners and administrative review.

### Organizations

Supports institutional structures and organization-specific permissions.

### Reporting

Provides reporting and analytics capabilities for learner, tutor and course activity.

### Notifications

Provides a foundation for email and in-app communication.

### Moderation

Includes abuse-reporting and moderation workflows for platform safety.

## API documentation

Swagger/OpenAPI is used to document the REST API and expose an interactive API interface.

When the application is running, use the Swagger route configured by the application (currently documented as `/docs`).

## Getting started

### Prerequisites

- Node.js
- npm
- MongoDB
- Redis when cache-dependent features are enabled

### Clone the repository

```bash
git clone https://github.com/Oluwatobi843/chainVerse-backend.git
cd chainVerse-backend
```

### Install dependencies

```bash
npm install
```

### Configure environment variables

Create a `.env` file using the variables expected by the application configuration. A typical configuration includes:

```env
PORT=3000
MONGODB_URI=mongodb://localhost:27017/chainverse
MONGO_URI=mongodb://localhost:27017/chainverse
JWT_SECRET=replace-with-a-strong-secret
JWT_REFRESH_SECRET=replace-with-a-strong-refresh-secret
```

Do not commit real credentials, private keys or production secrets.

### Run in development

```bash
npm run start:dev
```

### Build

```bash
npm run build
```

### Run production build

```bash
npm run start:prod
```

## Testing

```bash
# Unit tests
npm run test

# End-to-end tests
npm run test:e2e
```

The intended testing strategy is to unit-test business services, cover critical HTTP flows with end-to-end tests, and mock external dependencies where appropriate.

## Development guidelines

When extending the backend:

1. Keep controllers focused on HTTP concerns.
2. Put business rules in services.
3. Define request contracts with DTOs.
4. Validate external input.
5. Protect restricted routes with the appropriate guards.
6. Document public endpoints with Swagger decorators.
7. Keep domain-specific logic inside its module.
8. Add tests for new business-critical behavior.

## Migration from Express to NestJS

The migration is an architectural redesign rather than a framework-only rewrite.

The move to NestJS provides:

- Stronger modular boundaries
- Dependency injection
- Consistent application structure
- Reusable guards, pipes and interceptors
- Improved testability
- Easier onboarding for contributors
- A clearer path toward future distributed services

## Roadmap

Potential future work includes:

- Microservice decomposition using gRPC, Redis or RabbitMQ
- WebSocket-based real-time features
- Expanded blockchain/NFT integrations
- Payment gateway integrations
- Containerized deployment
- More comprehensive CI/CD automation
- Production observability and monitoring

## Portfolio value

This project demonstrates practical backend engineering across architecture, authentication, authorization, persistence, caching, API documentation, security and DevOps. It is particularly relevant to Backend Software Engineer roles requiring **NestJS, TypeScript, MongoDB, REST APIs and production-oriented system design**.

## Author

**Oluwatobi843**

GitHub: https://github.com/Oluwatobi843

## License

MIT License.
