<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" width="120" alt="Nest Logo" /></a>
</p>

[circleci-image]: https://img.shields.io/circleci/build/github/nestjs/nest/master?token=abc123def456
[circleci-url]: https://circleci.com/gh/nestjs/nest

  <p align="center">A progressive <a href="http://nodejs.org" target="_blank">Node.js</a> framework for building efficient and scalable server-side applications.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/dm/@nestjs/common.svg" alt="NPM Downloads" /></a>
<a href="https://circleci.com/gh/nestjs/nest" target="_blank"><img src="https://img.shields.io/circleci/build/github/nestjs/nest/master" alt="CircleCI" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer" target="_blank"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor" target="_blank"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-ff3f59.svg" alt="Donate us"/></a>
    <a href="https://opencollective.com/nest#sponsor"  target="_blank"><img src="https://img.shields.io/badge/Support%20us-Open%20Collective-41B883.svg" alt="Support us"></a>
  <a href="https://twitter.com/nestframework" target="_blank"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow" alt="Follow us on Twitter"></a>
</p>
  <!--[![Backers on Open Collective](https://opencollective.com/nest/backers/badge.svg)](https://opencollective.com/nest#backer)
  [![Sponsors on Open Collective](https://opencollective.com/nest/sponsors/badge.svg)](https://opencollective.com/nest#sponsor)-->

## Description

# Auth API on NestJS

Project for authentication and authorization of users using JWT tokens.

## Tech stack

- NestJS
- TypeORM
- PostgreSQL (or SQLite for testing)
- JWT for authentication
- bcrypt for password hashing
- Swagger for API documentation

## Features

- User registration
- Authentication (login) with access and refresh tokens
- Refreshing access token via refresh token
- Logout
- Getting current user profile
- User roles (USER, ADMIN)
- Protected routes for admins only

## Installation and launch

### Prerequisites

- Node.js (version 14+)
- npm or yarn
- PostgreSQL (or you can use SQLite for tests)

### Installation steps

1. Clone repository:
```bash
git clone <repository-url>
cd auth-api
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
- Rename `.env.example` to `.env`
- Edit `.env` with your database connection parameters and secret keys for JWT

4. Run the application:
```bash
# Development mode
npm run start:dev

# Production mode
npm run start:prod
```

5. Open Swagger documentation:
http://localhost:3000/api

## API Endpoints

### Authentication

- `POST /auth/register` - Register a new user
- `POST /auth/login` - Authenticate a user and get tokens
- `POST /auth/refresh` - Refresh an access token
- `POST /auth/logout` - Logout (requires JWT token)

### Users

- `GET /users/me` - Get current user data (requires JWT token)
- `GET /users/all` - Get all users (admins only)

## Project structure

```
src/
├── auth/ # Authentication module
│ ├── decorators/ # Decorators (GetUser, Roles)
│ ├── dto/ # Data Transfer Objects for API
│ ├── guards/ # Guards (JwtAuthGuard, RolesGuard)
│ ├── strategies/ # Passport strategies for JWT
│ ├── auth.controller.ts # Controller authentication
│ ├── auth.module.ts # Authentication module
│ └── auth.service.ts # Authentication service
│
├── users/ # Users module
│ ├── dto/ # Data Transfer Objects for API
│ ├── entities/ # User model
│ ├── users.controller.ts# Users controller
│ ├── users.module.ts # Users module
│ └── users.service.ts # Users service
│
├── common/ # Common components
│ └── filters/ # Exception filters
│
├── app.module.ts # Main application module
└── main.ts # Application entry point
```

## Security

- All passwords are hashed using bcrypt
- JWT tokens have a limited validity period
- Access token (15 minutes), Refresh token (7 days)
- User roles for accessing protected routes
