
# 🏛️ Ministry of Youth & Sports — National Management Platform

A full-scale digital transformation system for the **Ministry of Youth & Sports in Egypt**, connecting all youth and sports centers across the nation into one unified digital ecosystem.  

This platform consists of three main repositories:
1. 🌐 **Frontend (Next.js)** — Admin dashboard & public website  
2. ⚙️ **Backend (NestJS)** — Secure API and data management layer  
3. 📱 **Mobile App (Flutter)** — Cross-platform mobile experience  

---

## 🌐 Frontend (Next.js)

A production-ready **Next.js (App Router)** client that powers both the public landing website and the admin dashboard.  
It’s designed with scalability, accessibility, and RTL (Arabic) support in mind.

### 🚀 Features
- Interactive landing pages with dynamic sections (hero, features, team, etc.)  
- Admin dashboard for managing centers, activities, and news  
- Authentication system with JWT  
- Form validation using **React Hook Form** + **Zod**  
- Real-time notifications via **Sonner**  
- Responsive Arabic-first UI (RTL support)  
- Integration with OpenStreetMap for location display  

### 🛠️ Tech Stack
- **Next.js (App Router)**  
- **React.js + TypeScript**  
- **Tailwind CSS**  
- **Zod + React Hook Form**  
- **Axios**  
- **Sonner**  
- **Lucide Icons**  
- **OpenStreetMap Integration**

### 📂 Folder Structure
```

src/
├─ app/                     # Next.js routes (landing, dashboard, auth)
├─ components/
│  ├─ auth/                 # Authentication forms and components
│  ├─ dashboard/            # Dashboard widgets and UI blocks
│  ├─ global/               # Shared UI (map, loaders, selectors)
│  └─ ui/                   # Core UI primitives (buttons, modals, inputs)
├─ hooks/                   # Custom hooks (auth, API)
├─ lib/                     # Zod schemas and validations
├─ providers/               # Auth and context providers
├─ types/                   # TypeScript interfaces and types
└─ utils/                   # API utilities and helpers

````

### ⚙️ Setup
```bash
git clone https://github.com/<org>/ministry-frontend.git
cd ministry-frontend
npm install
npm run dev
````

> Runs locally at: `http://localhost:3000`

---

## ⚙️ Backend (NestJS)

A powerful **NestJS** backend built with a modular architecture and connected to **PostgreSQL** using **Prisma ORM**.
It provides secure endpoints, user authentication, and robust data management for all clients (web & mobile).

### 🚀 Features

* Modular API structure (Centers, Activities, News, Auth, Users)
* JWT authentication and role-based authorization
* File upload support using **Multer**
* PostgreSQL database with **Prisma ORM**
* RESTful APIs with Swagger documentation
* Docker-ready configuration for easy deployment

### 🛠️ Tech Stack

* **NestJS**
* **TypeScript**
* **PostgreSQL + Prisma ORM**
* **JWT Authentication**
* **Multer**
* **Docker**
* **Swagger**

### 📂 Folder Structure

```
src/
 ├─ app.module.ts            # Root module
 ├─ main.ts                  # App entry point
 ├─ auth/                    # Authentication logic (JWT, guards)
 ├─ users/                   # User and role management
 ├─ centers/                 # Centers CRUD operations
 ├─ activities/              # Activities management
 ├─ news/                    # News module
 ├─ files/                   # File uploads and storage
 ├─ common/                  # Shared utilities and decorators
 ├─ prisma/                  # Prisma schema and service
 └─ config/                  # Environment and settings
```

### ⚙️ Setup

```bash
git clone https://github.com/<org>/ministry-backend.git
cd ministry-backend
npm install
npx prisma migrate dev
npm run start:dev
```

> API runs locally at: `http://localhost:5000`
> Swagger Docs: `http://localhost:5000/api/docs`

---

## 📱 Mobile App (Flutter)

A **Flutter**-based mobile and desktop application designed to make youth and sports services accessible to everyone.
It supports Android, iOS, Web, and Desktop platforms.

### 🚀 Features

* Explore youth centers, clubs, and federations
* Access to activities, swimming pools, and stadiums
* Latest news and updates from the ministry
* Maps integration for directions and navigation
* Offline JSON-based data for enhanced performance
* Consistent responsive UI for all platforms

### 🛠️ Tech Stack

* **Flutter (Dart)**
* **Cubit / Bloc State Management**
* **JSON Data Assets**
* **Google Maps Integration**
* **Cross-Platform Support** (Android, iOS, Web, Desktop)

### 📂 Folder Structure

```
android/        # Android native files
ios/            # iOS native files
lib/
 ├─ models/     # Data models
 ├─ modules/    # Screens (home, clubs, activities, etc.)
 ├─ layout/     # State management (Cubit/Bloc)
 ├─ shared/     # Common components, themes, and networking
 └─ main.dart   # App entry point
assets/         # JSON datasets (centers, federations, etc.)
test/           # Unit and widget tests
web/            # Web app entry
windows/        # Windows build
macos/          # macOS build
linux/          # Linux build
```

### ⚙️ Setup

```bash
git clone https://github.com/<org>/ministry-mobile.git
cd ministry-mobile
flutter pub get
flutter run
```

---

## 🧩 System Architecture Overview

```
+--------------------------------------------------------------+
|                      MINISTRY PLATFORM                       |
+----------------------+--------------------+------------------+
|      FRONTEND        |      BACKEND       |      MOBILE APP  |
| (Next.js Dashboard)  |  (NestJS REST API) |  (Flutter Client)|
+----------------------+--------------------+------------------+
| Auth (JWT)           | Prisma ORM / DB    | Maps Integration |
| Admin Management     | Centers & News API | Offline Data     |
| RTL & UI Components  | Role-Based Access  | Activity Explorer |
+----------------------+--------------------+------------------+
```

---

## 🤝 Contribution

Contributions are welcome!
Please follow these steps:

1. Fork the relevant repository.
2. Create a new branch: `git checkout -b feat/your-feature`.
3. Make changes and commit with clear messages.
4. Open a pull request for review.

### 💡 Ministry of Youth & Sports — Empowering Digital Access to Youth and Sports Nationwide.

