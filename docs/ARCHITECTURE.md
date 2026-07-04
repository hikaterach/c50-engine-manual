# Architecture Overview

## System Architecture

```
┌─────────────────┐
│   Browser       │
│  (Next.js)      │
└────────┬────────┘
         │ HTTP/WebSocket
         ▼
┌─────────────────────────┐
│   Frontend (Port 3000)  │
│  - React Components     │
│  - Tailwind CSS         │
│  - Socket.io Client     │
└────────┬────────────────┘
         │ API Calls
         ▼
┌──────────────────────────────┐
│  Backend (Port 5000)         │
│  - Express Server            │
│  - WebSocket (Socket.io)     │
│  - Authentication (JWT)      │
│  - Business Logic            │
└────────┬─────────────────────┘
         │ SQL Queries
         ▼
┌──────────────────────────────┐
│  PostgreSQL (Port 5432)      │
│  - User Data                 │
│  - Manuals & Versions        │
│  - Tasks & Progress          │
│  - Messages & Chat           │
└──────────────────────────────┘
```

## Directory Structure

```
c50-engine-manual/
├── frontend/                 # Next.js Frontend
│   ├── app/                 # Page routes
│   ├── components/          # React components
│   ├── lib/                 # Utilities & API client
│   ├── styles/              # Global styles
│   └── public/              # Static assets
├── backend/                 # Express Backend
│   ├── src/
│   │   ├── routes/          # API routes
│   │   ├── controllers/     # Request handlers
│   │   ├── services/        # Business logic
│   │   ├── middleware/      # Auth, validation
│   │   ├── models/          # Database models
│   │   └── config/          # Configuration
│   └── tests/               # Unit tests
├── database/
│   └── migrations/          # SQL migration files
├── docs/                    # Documentation
└── docker-compose.yml       # Docker configuration
```

## Data Models

### User
- id (Primary Key)
- email (Unique)
- username (Unique)
- password_hash
- role (viewer, editor, admin)
- auth_provider (google, microsoft, email)
- created_at

### Group
- id (Primary Key)
- name
- description
- created_by (FK: User)
- members (Many-to-Many: GroupMember)
- created_at

### Manual
- id (Primary Key)
- title
- description
- content
- author_id (FK: User)
- group_id (FK: Group)
- status (draft, published)
- version
- created_at

### Task
- id (Primary Key)
- manual_id (FK: Manual)
- title
- description
- status (todo, in_progress, done)
- priority (low, medium, high)
- assigned_to (FK: User)
- due_date
- created_at

### Message
- id (Primary Key)
- sender_id (FK: User)
- recipient_id or group_id
- content
- is_read
- created_at

## Authentication Flow

1. **Email/Password**
   - User registers with email & password
   - Password is hashed with bcryptjs
   - JWT token is issued on login

2. **OAuth (Google/Microsoft)**
   - User clicks OAuth button
   - Redirected to provider
   - Provider returns ID token
   - Backend verifies token & creates/updates user
   - JWT token issued

3. **JWT Token**
   - Stored in HTTP-only cookie
   - Sent with every request
   - Verified by backend middleware

## Real-time Features (WebSocket)

- **Chat Messages**: Real-time group & direct messages
- **Task Updates**: Instant task status changes
- **User Presence**: Online/offline status
- **Notifications**: Real-time alerts

## Security Measures

- ✅ JWT authentication
- ✅ Password hashing (bcryptjs)
- ✅ CORS enabled
- ✅ SQL injection prevention (Parameterized queries)
- ✅ XSS protection (React escaping)
- ✅ CSRF protection (SameSite cookies)
- ✅ Role-based access control (RBAC)
