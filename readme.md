# 🏋️‍♂️ FitTrack

**FitTrack** is a full-stack web app to manage and log workouts — built with  
**FastAPI + MongoDB (Beanie)** on the backend and **Vue 3 (Vite)** on the frontend.

---

## ⚙️ Tech Stack

### Backend
- FastAPI (async REST API)
- Beanie ODM + Motor (MongoDB)
- Pydantic v2 for schemas
- JWT authentication
- Passlib for password hashing

### Frontend
- Vue 3 (Composition API)
- Vite build system
- Pinia (state)
- Vue Router
- Axios for API calls

---

## 🗂️ Project Structure

```
fittrack/
│
├── backend/
│   ├── app/
│   │   ├── core/        # config, security, deps
│   │   ├── db/          # Beanie init
│   │   ├── models/      # Mongo documents (User, Plan, Circuit, etc.)
│   │   ├── routers/     # FastAPI endpoints
│   │   └── main.py      # app entrypoint
│   └── Dockerfile
│
└── fittrack-web/        # Vue 3 frontend
```

---

## 🚀 Getting Started (Dev)

### 1️⃣ Clone & enter
```bash
git clone https://github.com/<yourname>/fittrack.git
cd fittrack
```

### 2️⃣ Run backend (Docker)
```bash
docker compose up
```
This starts:
- MongoDB on **27017**
- FastAPI on **http://localhost:8000**

Docs available at:  
👉 [http://localhost:8000/docs](http://localhost:8000/docs)

### 3️⃣ Run frontend
```bash
cd fittrack-web
npm install
npm run dev
```
Vue app runs on **http://localhost:5173**

---

## 👤 Authentication

- `POST /auth/register` → Create user  
- `POST /auth/login` → Obtain JWT  
- Use `Authorization: Bearer <token>` for all other routes.

---

## 🧩 API Overview

| Route | Method | Description |
|-------|---------|-------------|
| `/auth/register` | POST | Create account |
| `/auth/login` | POST | Get JWT token |
| `/users/me` | GET | Current user info |
| `/plans/` | GET/POST | Manage workout plans |
| `/workouts/` | GET/POST/PATCH | Log workout sessions |

---

## 🧠 Data Model Overview

**User → WorkoutPlan → Circuits → Exercises**

Each circuit defines multiple **PlanExercises**, each having:
- series
- repetitions or time (rep_kind)
- recovery time
- weight

**WorkoutSession** logs:
- user
- circuit
- start / end times
- completion status

---

## 🧰 Environment Variables

| Key | Default | Description |
|-----|----------|-------------|
| `MONGO_URI` | `mongodb://localhost:27017` | Mongo connection URI |
| `MONGO_DB` | `fittrack` | Database name |
| `JWT_SECRET` | `dev-secret-change-me` | Secret key for tokens |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | `1440` | JWT lifetime |

---

## 🧱 Build for Production

```bash
# Backend
docker compose -f docker-compose.yml up --build -d

# Frontend (build)
cd fittrack-web
npm run build
```

You can serve the `dist/` folder via Nginx or similar.

---

## 🧾 License

MIT © [Your Name]

---

### ✅ Next Steps
- [ ] Add CRUD for exercises + seed data  
- [ ] Add “actual performance” tracking for workouts  
- [ ] Deploy on Fly.io / Render with Mongo Atlas  
- [ ] Implement mobile-friendly UI
