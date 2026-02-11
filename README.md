# Task Manager API (Node.js + Express + MongoDB)

A simple, production-like REST API you can use for internship projects.

## Features
- JWT Authentication (Register/Login)
- Password hashing with bcrypt
- Tasks CRUD (Create, Read, Update, Delete)
- Each user can only access **their own** tasks
- Validation (express-validator)
- Centralized error handling
- Basic security: Helmet + Rate limiting
- Docker support (optional)

---

## Tech
- Node.js + Express
- MongoDB + Mongoose
- JWT (jsonwebtoken)

---

## Folder Structure
```
task-manager-api/
  src/
    app.js
    server.js
    config/db.js
    controllers/
    middleware/
    models/
    routes/
    utils/
    validators/
  postman/
  .env.example
  Dockerfile
  docker-compose.yml
```

---

## Quick Start (Local)
### 1) Install dependencies
```bash
npm install
```

### 2) Create `.env`
Copy the example:
```bash
cp .env.example .env
```
Update `MONGO_URI` and `JWT_SECRET`.

### 3) Run MongoDB
Make sure MongoDB is running locally:
- Example URI: `mongodb://localhost:27017/task_manager`

### 4) Start the server
Development (auto-reload):
```bash
npm run dev
```

Production:
```bash
npm start
```

Server runs on: `http://localhost:5000`

---

## Run with Docker (Local)
### 1) Start services
```bash
docker compose up --build
```

API will be: `http://localhost:5000`  
MongoDB will be: `mongodb://localhost:27017/task_manager`

To stop:
```bash
docker compose down
```

---

## API Endpoints

### Auth
- `POST /api/auth/register`
- `POST /api/auth/login`

### Tasks (Protected: Bearer token)
- `GET /api/tasks` (supports `?page=1&limit=10&status=pending|done`)
- `POST /api/tasks`
- `GET /api/tasks/:id`
- `PUT /api/tasks/:id`
- `DELETE /api/tasks/:id`

---

## Sample Request Bodies

### Register
```json
{
  "name": "Ahmad Idris",
  "email": "ahmad@example.com",
  "password": "Password123!"
}
```

### Login
```json
{
  "email": "ahmad@example.com",
  "password": "Password123!"
}
```

### Create Task
```json
{
  "title": "Finish report",
  "description": "Complete chapter 4 edits",
  "status": "pending",
  "dueDate": "2026-03-01"
}
```

---

## Postman
Import the collection:
`postman/TaskManagerAPI.postman_collection.json`

Tip: set the Postman variables:
- `baseUrl` = `http://localhost:5000`
- `token` = JWT you get after login

---

## Hosting Notes (simple)
This API can be hosted on platforms like Render/Railway/Fly.io.
- Set environment variables on the hosting dashboard (same keys as `.env.example`)
- Use a managed MongoDB (MongoDB Atlas) and set `MONGO_URI` to the Atlas connection string
- Start command: `npm start`

**Important:** add your deployed frontend URL to `CORS_ORIGIN` if needed.

---

## License
MIT
