# NorthStar Insurance Platform

Secure full-stack insurance platform built for the **Modern Web Technologies** lab.

## Features

- HTTPS-enabled Express backend
- JWT login and protected REST APIs
- Comprehensive user profile module
- Admin-only RBAC management
- Insurance workflows for policies, amendments, reductions, and claims
- Next.js frontend with protected pages for customer, internal, and admin users

## Tech Stack

### Backend
- Node.js
- Express.js
- MongoDB / Mongoose
- JWT
- HTTPS

### Frontend
- Next.js
- React
- TypeScript

## Project Structure

- `backend-api/` - secure Express REST API
- `frontend-web/` - Next.js client application
- `infrastructure/` - optional local infrastructure files

## Setup

### 1. Backend
```bash
cd backend-api
npm install
cp .env.example .env
npm run seed
npm start
```

### 2. Frontend
```bash
cd frontend-web
npm install
cp .env.local.example .env.local
npm run dev
```

## Sample Users
All sample users use the password:

```text
Password123!
```

- `admin1`
- `customer1`
- `agent1`
- `underwriter1`
- `adjuster1`

## Security Notes

- Backend runs over HTTPS using the configured certificate
- JWT is required for protected API requests
- Role checks protect privileged routes
- Ownership checks prevent customers from accessing other users' data
- Real secret-bearing `.env` files are intentionally excluded from the final submission zip
