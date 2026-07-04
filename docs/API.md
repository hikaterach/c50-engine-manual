# C50 Engine Manual Platform - API Documentation

## Base URL
```
http://localhost:5000/api
```

## Authentication

All endpoints (except login/register) require a JWT token in the Authorization header:

```
Authorization: Bearer <token>
```

## Endpoints

### Authentication

#### POST /auth/register
- Register a new user
- Body: `{ email, password, username }`

#### POST /auth/login
- Login with email and password
- Body: `{ email, password }`
- Response: `{ token, user }`

#### POST /auth/google
- Login with Google OAuth
- Body: `{ idToken }`

#### POST /auth/microsoft
- Login with Microsoft OAuth
- Body: `{ idToken }`

### Users

#### GET /users/profile
- Get current user profile

#### PUT /users/profile
- Update user profile
- Body: `{ firstName, lastName, avatarUrl }`

#### GET /users/:id
- Get user details

### Groups

#### POST /groups
- Create a new group
- Body: `{ name, description }`

#### GET /groups
- List all groups for current user

#### GET /groups/:id
- Get group details

#### PUT /groups/:id
- Update group
- Body: `{ name, description }`

#### POST /groups/:id/members
- Add member to group
- Body: `{ userId, role }`

#### DELETE /groups/:id/members/:userId
- Remove member from group

### Manuals

#### POST /manuals
- Create a new manual
- Body: `{ title, description, groupId }`

#### GET /manuals
- List manuals with filters

#### GET /manuals/:id
- Get manual details

#### PUT /manuals/:id
- Update manual
- Body: `{ title, description, content }`

#### DELETE /manuals/:id
- Delete manual

### Tasks

#### POST /tasks
- Create a new task
- Body: `{ manualId, title, description, assignedTo, dueDate }`

#### GET /tasks
- List tasks with filters

#### PUT /tasks/:id
- Update task
- Body: `{ status, priority, assignedTo }`

### Messages (Chat)

#### GET /messages
- Get chat messages
- Query: `?groupId=X` or `?recipientId=X`

#### POST /messages
- Send a message
- Body: `{ content, recipientId or groupId }`

## WebSocket Events

### Connection
```javascript
const socket = io('http://localhost:5000');
```

### Events

- `message:send` - Send a new message
- `message:receive` - Receive a new message
- `user:online` - User comes online
- `user:offline` - User goes offline
- `task:update` - Task status updated
