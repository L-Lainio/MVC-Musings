# MVC-Musings - Quick Start Guide

## 🚀 Getting Started

### Option 1: Docker (Recommended)
```bash
cd Main
docker-compose up --build
```
Access at: `http://localhost:3001`

### Option 2: Local Development
```bash
cd Main
npm install
cp .env.example .env
# Edit .env with your database credentials
npm run seed
npm start
```

## 🧪 Testing Sandbox
```bash
cd Main
docker-compose -f docker-compose.test.yml up --build
```
Test environment at: `http://localhost:3002`

## 📁 Project Structure
- **Main/** - Production-ready application
- **Develop/** - Development version
- **DOCKER.md** - Comprehensive Docker documentation

## 📖 Documentation
- See [README.md](README.md) for project overview
- See [DOCKER.md](DOCKER.md) for Docker setup and testing details
- See [LICENSE](LICENSE) for license information

## 🔑 Environment Variables
Required in `.env` file:
```
DB_NAME=mvc_musings_db
DB_USER=postgres
DB_PASSWORD=your_password
SESSION_SECRET=your_secret_key
```

## 🐳 Docker Ports
- `3001` - Production app
- `3002` - Test sandbox
- `3003` - Development app
- `5432` - Production database
- `5433` - Test database
- `5434` - Development database

## 💡 Common Commands

### Docker
```bash
# Start production
docker-compose up

# Start in background
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f
```

### Database
```bash
# Seed database
npm run seed

# Access PostgreSQL
docker exec -it mvc-musings-db psql -U postgres -d mvc_musings_db
```

## 🆘 Need Help?
- Check [DOCKER.md](DOCKER.md) for detailed Docker instructions
- Review [README.md](README.md) for project details
- Look at `.env.example` for required environment variables
