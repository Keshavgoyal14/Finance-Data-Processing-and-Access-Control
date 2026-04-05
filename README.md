# Financial Data Management

Full-stack financial management system with role-based access control, analytics dashboard, records management, and Swagger/OpenAPI documentation.

## Monorepo Structure

- [backend](backend): Express + TypeScript + SQLite API
- [frontend](frontend): React + TypeScript (Vite)

## Core Features

- JWT authentication (register/login)
- Role-based authorization: viewer, analyst, admin
- Admin user management (create/update/delete users)
- Financial records CRUD with filters and pagination
- Dashboard summaries and trend analytics
- Interactive Swagger docs + OpenAPI JSON

## Prerequisites

- Node.js 20.19+ (or 22.12+)
- npm

## Quick Start (Local)

1. Start backend

```bash
cd backend
npm install
npm run dev
```

Backend default URL: http://localhost:4000

2. Start frontend in a second terminal

```bash
cd frontend
npm install
npm run dev
```

Frontend default URL: http://localhost:5173

## Backend API Docs

- Swagger UI: http://localhost:4000/api/docs
- OpenAPI JSON: http://localhost:4000/api/openapi.json

For protected endpoints, authorize in Swagger with:

```txt
Bearer <jwt-token>
```

## Environment Setup

### Backend

At minimum configure:

```env
PORT=4000
JWT_SECRET=replace-with-a-strong-secret
```

Optional seed variables:

```env
SEED_DEMO_USERS=true
SEED_USERS_JSON=[{"name":"Admin User","email":"admin@example.com","password":"strong-password","role":"admin"}]
SEED_RECORDS_JSON=[{"amount":1000,"type":"income","category":"Salary","date":"2026-04-01","notes":"Monthly","createdByEmail":"admin@example.com"}]
```

### Frontend

Optional API base override:

```env
VITE_API_BASE=https://your-backend-domain
```

When `VITE_API_BASE` is not set, frontend uses relative API paths (works with Vite proxy in local dev).

## Build Commands

### Backend

```bash
cd backend
npm run build
npm run start
```

### Frontend

```bash
cd frontend
npm run build
npm run preview
```

## Seeding Notes

- `npm run seed` in backend always clears records.
- Demo users and records are created only when `SEED_DEMO_USERS=true` and JSON env variables are provided.

## Auth and Roles

- viewer: dashboard summary access
- analyst: dashboard + records read
- admin: full access (including user management and records write)

## Deployment (Render)

For backend web service:

- Root Directory: `backend`
- Build Command: `npm install && npm run build`
- Start Command: `npm run start`
- Environment Variable: `JWT_SECRET`

Deployed docs URLs:

- `https://<your-backend>.onrender.com/api/docs`
- `https://<your-backend>.onrender.com/api/openapi.json`

## Common API Troubleshooting

- `401 Missing or invalid Authorization header`: missing `Bearer <token>`
- `403 Insufficient permissions`: token user role cannot access endpoint
- `500 NOT NULL constraint failed: users.password`: `/api/users` requires password in create body

## Detailed Docs

- Backend details: [backend/README.md](backend/README.md)
- Frontend details: [frontend/README.md](frontend/README.md)
