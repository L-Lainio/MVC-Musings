# Docker Setup and Testing Guide

## Overview
This project includes complete Docker configuration for:
- **Production environment** (Main/)
- **Development environment** (Develop/)
- **Testing sandbox** (isolated test environment)

---

## Prerequisites
- Docker Desktop installed and running
- Docker Compose (included with Docker Desktop)

---

## Production Environment (Main/)

### Quick Start
```bash
cd Main
docker-compose up --build
```

Access the application at: `http://localhost:3001`

### Environment Variables
Create a `.env` file in the `Main/` directory:
```env
DB_NAME=mvc_musings_db
DB_USER=postgres
DB_PASSWORD=your_secure_password
SESSION_SECRET=your_random_secret_key
```

### Services
- **Database**: PostgreSQL 15 on port `5432`
- **Application**: Node.js Express app on port `3001`

### Common Commands
```bash
# Start services
docker-compose up

# Start in background
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down

# Stop and remove volumes (WARNING: deletes database data)
docker-compose down -v

# Rebuild containers
docker-compose up --build
```

---

## Development Environment (Develop/)

### Quick Start
```bash
cd Develop
docker-compose up --build
```

Access the development application at: `http://localhost:3003`

### Services
- **Database**: PostgreSQL 15 on port `5434`
- **Application**: Node.js Express app on port `3003`

This runs on different ports to avoid conflicts with the production environment.

---

## Testing Sandbox

### Purpose
The testing sandbox provides an **isolated environment** for running tests without affecting development or production databases.

### Quick Start
```bash
cd Main
docker-compose -f docker-compose.test.yml up --build
```

### Features
- Separate PostgreSQL instance on port `5433`
- Test application on port `3002`
- Isolated database: `mvc_musings_test_db`
- Automatically seeds test data
- Runs test suite on startup

### Environment
```
DB_NAME: mvc_musings_test_db
DB_USER: test_user
DB_PASSWORD: test_password
DB_HOST: test-db
PORT: 3002
NODE_ENV: test
```

### Running Tests
```bash
# Run tests in sandbox
docker-compose -f docker-compose.test.yml up --build

# Run tests and remove containers when done
docker-compose -f docker-compose.test.yml up --build --abort-on-container-exit

# Clean up test environment
docker-compose -f docker-compose.test.yml down -v
```

---

## Database Management

### Access PostgreSQL Container
```bash
# Production database
docker exec -it mvc-musings-db psql -U postgres -d mvc_musings_db

# Development database
docker exec -it mvc-musings-develop-db psql -U postgres -d mvc_musings_dev_db

# Test database
docker exec -it mvc-musings-test-db psql -U test_user -d mvc_musings_test_db
```

### Backup Database
```bash
# Backup production database
docker exec mvc-musings-db pg_dump -U postgres mvc_musings_db > backup.sql

# Restore database
cat backup.sql | docker exec -i mvc-musings-db psql -U postgres -d mvc_musings_db
```

### Reset Database
```bash
# Stop services
docker-compose down

# Remove volumes (this deletes all data)
docker volume rm mvc-musings_postgres_data

# Restart (will reinitialize database)
docker-compose up --build
```

---

## Troubleshooting

### Port Conflicts
If you get port binding errors, check if the ports are already in use:
```powershell
# Check what's using a port
netstat -ano | findstr :3001
```

### Container Won't Start
```bash
# View detailed logs
docker-compose logs app

# Check container status
docker-compose ps

# Restart specific service
docker-compose restart app
```

### Database Connection Issues
```bash
# Check if database is healthy
docker-compose ps

# View database logs
docker-compose logs db

# Test database connection
docker exec -it mvc-musings-db pg_isready -U postgres
```

### Clean Slate
If everything is broken, start fresh:
```bash
# Stop all containers
docker-compose down

# Remove all volumes and orphan containers
docker-compose down -v --remove-orphans

# Rebuild from scratch
docker-compose up --build
```

---

## Best Practices

### For Development
1. Use the Develop/ folder for active development
2. Use volume mounts to see code changes without rebuilding
3. Keep production and development databases separate

### For Testing
1. Always use the test sandbox for running tests
2. Clean up test environment after testing: `docker-compose -f docker-compose.test.yml down -v`
3. Never run tests against production or development databases

### For Production
1. Use strong passwords in production .env files
2. Never commit .env files to version control
3. Regularly backup the database
4. Use docker-compose down (not down -v) to preserve data

---

## Docker Architecture

```
MVC-Musings/
├── Main/                          # Production environment
│   ├── Dockerfile                 # Production app image
│   ├── Dockerfile.test            # Test app image
│   ├── docker-compose.yml         # Production services
│   ├── docker-compose.test.yml    # Test sandbox services
│   └── .dockerignore              # Files to exclude
│
└── Develop/                       # Development environment
    ├── Dockerfile                 # Development app image
    ├── docker-compose.yml         # Development services
    └── .dockerignore              # Files to exclude
```

### Port Allocation
- `3001` - Production app
- `3002` - Test sandbox app
- `3003` - Development app
- `5432` - Production database
- `5433` - Test database
- `5434` - Development database

---

## Additional Resources
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [PostgreSQL Docker Hub](https://hub.docker.com/_/postgres)
- [Node.js Docker Hub](https://hub.docker.com/_/node)
