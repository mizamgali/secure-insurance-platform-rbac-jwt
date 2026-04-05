# NorthStar Insurance Platform

## Project Description
NorthStar Insurance Platform is a secure full-stack insurance application built to simulate a modern digital platform used in the financial services and insurance industry. The system supports multiple insurance product types, including life, car, and home insurance, and provides secure functionality for both customers and internal staff.

The platform demonstrates:
- HTTPS-secured backend communication
- JWT-based authentication
- role-based access control (RBAC)
- protected REST APIs
- comprehensive user profile management
- insurance workflows such as policy creation, amendment requests, reduction requests, and claims processing

The backend is built with Node.js and Express.js, while the frontend is built with React and Next.js. The system is designed to show secure full-stack architecture, API protection, ownership checks, and admin-controlled role management.

---

## Technology Stack
### Backend
- Node.js
- Express.js
- MongoDB / Mongoose
- JWT
- HTTPS / HTTP (development fallback)
- dotenv

### Frontend
- React
- Next.js
- TypeScript
- Fetch / API service layer

---

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/northstar-insurance-platform.git
cd northstar-insurance-platform
````

### 2. Install Backend Dependencies

```bash
cd backend-api
npm install
```

### 3. Install Frontend Dependencies

```bash
cd ../frontend-web
npm install
```

### 4. Start MongoDB

Make sure MongoDB is running locally.

Example:

```bash
brew services start mongodb-community
```

### 5. Configure Environment Files

Create environment files based on the provided examples.

Backend:

```bash
cd backend-api
cp .env.example .env
```

Frontend:

```bash
cd ../frontend-web
cp .env.local.example .env.local
```

### 6. Seed the Database

```bash
cd ../backend-api
npm run seed
```

### 7. Start the Backend

```bash
npm start
```

### 8. Start the Frontend

Open a second terminal:

```bash
cd frontend-web
npm run dev
```

### 9. Open the Application

Frontend:

```text
http://localhost:3000
```

Backend:

```text
http://localhost:5001
```

---

## Certificate Setup Instructions

The original lab design requires the backend to run over HTTPS using development certificates. In this project, a certificate file is included in the backend certificate folder for development setup.

### Expected HTTPS Setup

The backend was originally configured to run with:

* certificate file
* HTTPS server startup
* secure frontend-to-backend communication

### Development Note

If certificate verification fails locally, the backend can be run temporarily over HTTP for development and testing. This was used as a fallback in local setup due to certificate validation issues on macOS.

### If Using HTTPS

Make sure the `.env` file includes the correct certificate path and passphrase.

Example:

```env
HTTPS_PFX_PATH=./cert/server.pfx
HTTPS_PFX_PASSPHRASE=your_passphrase_here
```

### If Using HTTP Fallback

The backend can be started using normal Express `app.listen(...)`, and the frontend API base URL must use `http://localhost:5001/api`.

---

## Environment Configuration Instructions

### Backend `.env`

Example:

```env
NODE_ENV=development
PORT=5001
MONGODB_URI=mongodb://127.0.0.1:27017/insurance_platform
JWT_SECRET=my_super_secret_key_123
JWT_EXPIRES_IN=2h
FRONTEND_URL=http://localhost:3000
HTTPS_PFX_PATH=./cert/server.pfx
HTTPS_PFX_PASSPHRASE=your_passphrase_here
```

### Frontend `.env.local`

Example:

```env
NEXT_PUBLIC_API_BASE_URL=http://localhost:5001/api
```

### Important Notes

* real secret values should not be committed
* `.env` and `.env.local` should remain local
* only `.env.example` and `.env.local.example` should be included in the repository

---

## Sample Users and Roles

The application includes sample demo accounts for testing different roles.

### Demo Accounts

* `admin1` / `Password123!`
* `customer1` / `Password123!`
* `agent1` / `Password123!`
* `underwriter1` / `Password123!`
* `adjuster1` / `Password123!`

### Roles

* Admin
* Customer
* Agent
* Underwriter
* Claims Adjuster
* Customer Service
* Compliance Officer

These accounts are used to test authentication, authorization, protected routes, and role-specific workflows.

---

## Explanation of JWT Use

JWT is used for secure user authentication.

### Login Flow

1. The user enters username and password.
2. The backend validates the credentials.
3. If valid, the backend generates a signed JWT.
4. The frontend stores the token and uses it for future protected API requests.
5. Protected backend routes verify the token before allowing access.

### JWT Payload

The token includes fields such as:

* userId
* username
* roles
* issued time
* expiration time

### Security Purpose

JWT ensures that:

* only authenticated users can access protected resources
* the backend can identify the logged-in user
* role and ownership checks can be applied on each request

Passwords are never stored inside the token.

---

## Explanation of User Profile Module

The platform includes a comprehensive user profile module instead of a minimal login-only record.

### Authentication Layer

This layer supports login and access control:

* userId
* username
* hashed password
* account status
* assigned roles

### Business Profile Layer

This layer stores insurance-related user information:

* first name
* last name
* date of birth
* email
* phone number
* address
* city, province/state, postal code, country
* customer number or employee number
* preferred contact method
* emergency contact
* createdAt / updatedAt
* internal or customer-specific profile fields

### Access Rules

* customers can view their own profile
* customers can update only allowed personal fields
* internal users may view profile data based on role
* admin can view and update all user profiles and account statuses

This module supports both business operations and secure authorization behavior.

---

## Explanation of RBAC Management

The platform uses Role-Based Access Control (RBAC) to control access to operations and data.

### Core RBAC Principle

Authentication confirms who the user is.
Authorization determines what the user is allowed to do.

### Admin Responsibilities

Only the Admin role can:

* view all users
* update user accounts
* activate or deactivate accounts
* assign roles
* remove roles
* view role assignments

### Role Separation

The system separates duties across business roles:

* Customer: manages own profile, policies, claims
* Agent: creates policies and assists customers
* Underwriter: reviews and approves amendments and reductions
* Claims Adjuster: reviews and approves or rejects claims
* Customer Service: supports customer operations
* Compliance Officer: read-only oversight functions
* Admin: full user and RBAC management

### Security Goal

RBAC prevents privilege escalation and ensures users can perform only the actions appropriate to their organizational role.

---

## Explanation of Protected Routes

The backend uses middleware-based route protection.

### Authentication Middleware

Checks:

* whether an Authorization token exists
* whether the JWT is valid
* whether the token has expired

If the token is invalid or missing, access is denied.

### Authorization Middleware

Checks:

* whether the logged-in user has the required role
* whether the action is allowed for that role

If the role is not allowed, access is denied.

### Ownership Validation

Ownership rules ensure that customers can only access:

* their own profile
* their own policies
* their own claims
* their own requests

### Examples

* a customer can view only their own policies
* an agent can create policies
* an underwriter can approve amendment and reduction requests
* a claims adjuster can approve or reject claims
* a non-admin user cannot assign roles

This protects the system from both unauthorized access and improper access to another user’s records.

---

## Main Features

* secure login with JWT
* profile management
* admin user management
* role assignment and RBAC enforcement
* policy creation and viewing
* amendment workflow
* reduction workflow
* claim submission and decision workflow
* protected frontend navigation
* protected backend REST APIs

---

## Testing

The following scenarios were tested:

* valid login returns JWT
* invalid login is rejected
* customer can view own profile
* customer cannot view another customer profile
* admin can list all users
* non-admin cannot assign roles
* agent can create policy
* underwriter can approve amendment
* claims adjuster can approve or reject claim
* unauthorized users are blocked from protected routes

---

## Notes

The main focus is secure architecture, JWT authentication, RBAC enforcement, ownership validation, and realistic insurance business workflows.
 
