# Backend API

Secure insurance platform backend API for the Modern Web Technologies lab.

## Features
- HTTPS server configuration
- JWT authentication
- Protected profile APIs
- Admin RBAC management
- Policy, amendment, reduction, and claim workflows
- Ownership enforcement for customer data

## Setup
1. Install dependencies:
   ```bash
   npm install
   ```
2. Create environment file:
   ```bash
   cp .env.example .env
   ```
3. Seed sample data:
   ```bash
   npm run seed
   ```
4. Start the secure API:
   ```bash
   npm start
   ```

## Important Routes
- `POST /api/auth/login`
- `GET /api/profile/me`
- `PUT /api/profile/me`
- `GET /api/admin/users`
- `POST /api/admin/rbac/users/:userId/roles`
- `GET /api/policies`
- `POST /api/amendments`
- `POST /api/reductions`
- `POST /api/claims`
