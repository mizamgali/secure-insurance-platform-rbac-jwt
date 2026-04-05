# Report Guide

## 1. Lab Objective
Build a secure full-stack insurance platform with HTTPS, JWT, role-based authorization, protected APIs, and admin-managed RBAC.

## 2. Architecture Overview
- Next.js frontend
- Express backend
- MongoDB data storage
- HTTPS for secure communication
- JWT authentication
- Middleware for auth, roles, validation, and ownership

## 3. Authentication Flow
1. User submits username and password.
2. Backend validates credentials.
3. Backend issues signed JWT.
4. Frontend stores the token and sends it in Authorization headers.
5. Protected routes verify the token before allowing access.

## 4. Authorization Flow
- `authenticate` middleware validates JWT.
- `authorizeRoles` middleware checks role access.
- ownership middleware restricts customer access to their own records.
- admin-only routes manage users and role assignments.

## 5. User Profile Design
Explain authentication fields, business profile fields, and role-specific access rules.

## 6. RBAC Management by Admin
Describe listing users, listing roles, assigning roles, removing roles, and account activation/deactivation.

## 7. HTTPS Configuration
Mention PFX certificate, secure Express server, and API access through `https://localhost:5001`.

## 8. Required Screenshots
- backend running over HTTPS
- login success with JWT flow
- profile page
- admin user list
- role assignment page
- policies page
- amendment/reduction request page
- claims review page
- unauthorized access example
