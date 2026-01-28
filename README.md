
# 🌱 MVC-Musing
*A tech blog exploring software architecture, design patterns, and developer insights—covering MVC and beyond.*

![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![NPM](https://img.shields.io/badge/NPM-CB3837?style=for-the-badge&logo=npm&logoColor=white)
![Handlebars](https://img.shields.io/badge/Handlebars.js-f0772b?style=for-the-badge&logo=handlebarsdotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![bcrypt](https://img.shields.io/badge/bcrypt-Hashing-orange?style=for-the-badge)
![express-session](https://img.shields.io/badge/express--session-Cookie%20Sessions-blue?style=for-the-badge)
![connect-session-sqlite](https://img.shields.io/badge/connect--session--sqlite-Session%20Store-green?style=for-the-badge)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github)

---

## 📖 Overview
**MVC-Musings** is a full-stack web application built using the Model-View-Controller architectural pattern. This project demonstrates modern web development practices with Node.js, Express, Handlebars templating, and PostgreSQL database integration with user authentication and session management.

---

## 🛠 Tech Stack
- **Express.js** – Web framework for Node.js  
- **Node.js & NPM** – JavaScript runtime and package manager  
- **Handlebars.js** – Templating engine for dynamic views  
- **PostgreSQL** – Relational database with Sequelize ORM  
- **bcrypt** – Secure password hashing  
- **express-session** – Session management middleware  
- **connect-session-sequelize** – PostgreSQL-backed session store  
- **Docker** – Containerization for development and testing

---

## ✨ Features
- MVC architecture for clean separation of concerns  
- User authentication and authorization with **bcrypt**  
- Persistent sessions using **express-session** with PostgreSQL storage  
- Dynamic views powered by **Handlebars.js**  
- RESTful API routes for user and project management  
- Docker support for consistent development and testing environments
- Isolated sandbox environment for testing

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- PostgreSQL (v12 or higher) OR Docker

### Local Development

Clone the repository:
```bash
git clone https://github.com/yourusername/MVC-Musings.git
cd MVC-Musings/Main
```

Install dependencies:
```bash
npm install
```

Create a `.env` file in the Main directory:
```env
DB_NAME=mvc_musings_db
DB_USER=your_username
DB_PASSWORD=your_password
SESSION_SECRET=your_secret_key
```

Set up the database:
```bash
# Create database using schema
psql -U postgres -f db/schema.sql

# Seed the database
npm run seed
```

Start the application:
```bash
npm start
```

Visit `http://localhost:3001` in your browser.

### Docker Development

Build and run with Docker Compose:
```bash
docker-compose up --build
```

The application will be available at `http://localhost:3001`

### Testing Sandbox

Run tests in an isolated sandbox environment:
```bash
docker-compose -f docker-compose.test.yml up --build
```

This creates a separate PostgreSQL instance for testing without affecting your development data.

---

## 📁 Project Structure

```
Main/
├── config/          # Database connection configuration
├── controllers/     # Route handlers (MVC Controllers)
├── models/          # Sequelize models (MVC Models)
├── views/           # Handlebars templates (MVC Views)
├── public/          # Static assets (CSS, JS)
├── utils/           # Helper functions and middleware
├── seeds/           # Database seed data
└── server.js        # Application entry point
```

---

## 🔐 Authentication
- User passwords are hashed using bcrypt
- Sessions are stored in PostgreSQL via connect-session-sequelize
- Protected routes require authentication via middleware

---

## 🤝 Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📝 License
This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.
