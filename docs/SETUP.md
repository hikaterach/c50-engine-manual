# Setup Guide

## Prerequisites

- Node.js 18+
- PostgreSQL 15+
- Docker & Docker Compose (optional)

## Local Development Setup

### 1. Clone the Repository

```bash
git clone https://github.com/hikaterach/c50-engine-manual.git
cd c50-engine-manual
```

### 2. Environment Variables

Create `.env` files in root, backend, and frontend directories:

```bash
cp .env.example .env
```

Edit `.env` with your configuration.

### 3. Docker Setup (Recommended)

```bash
docker-compose up -d
```

This will start:
- PostgreSQL database
- Backend server (port 5000)
- Frontend application (port 3000)

### 4. Manual Setup

If not using Docker:

#### Backend

```bash
cd backend
npm install
npm run migrate
npm run dev
```

#### Frontend

```bash
cd frontend
npm install
npm run dev
```

### 5. Database Setup

```bash
cd backend
npm run migrate
```

## Access Points

- Frontend: http://localhost:3000
- Backend API: http://localhost:5000/api
- Database: localhost:5432

## OAuth Configuration

### Google OAuth

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable Google+ API
4. Create OAuth 2.0 credentials (Web application)
5. Add `http://localhost:3000` to authorized redirect URIs
6. Copy Client ID and Secret to `.env`

### Microsoft OAuth

1. Go to [Azure Portal](https://portal.azure.com/)
2. Register a new application
3. Create a client secret
4. Add `http://localhost:3000/api/auth/callback/microsoft` to redirect URIs
5. Copy Application ID and Secret to `.env`

## Troubleshooting

### Database Connection Error

```bash
# Check if PostgreSQL is running
sudo systemctl status postgresql

# Or with Docker
docker ps | grep postgres
```

### Port Already in Use

Change port in `.env` and restart services.

### Module Not Found

```bash
# Reinstall dependencies
rm -rf node_modules package-lock.json
npm install
```

## Next Steps

See [API Documentation](./API.md) for endpoint details.
