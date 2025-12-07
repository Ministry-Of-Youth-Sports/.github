# 🏟️ Ministry of Youth & Sports Management System

A comprehensive digital ecosystem designed to modernize and digitize the operations of the Ministry of Youth and Sports.
This system bridges the gap between the ministry and the public through a user-friendly **mobile application**, while streamlining management and administrative workflows through a powerful **web dashboard**.
All components are powered by a secure and scalable **backend API**.

---

## 🌟 Project Overview

The core mission of this project is to:

* Enhance accessibility to youth and sports facilities.
* Promote transparency and engagement with the public.
* Digitize administrative operations and content management.
* Provide an integrated platform for information, activities, and communication.

The system is built on **three synchronized tracks**:

1. **Mobile Application (Public Portal)**
2. **Web Dashboard (Admin Panel)**
3. **Backend API (Central Logic & Data Source)**

---

## 🚀 Key Features

### 📱 Mobile Application (Citizen Portal)

A centralized hub for the community to explore youth and sports services.

#### **Directory Services**

* Sports Clubs listings
* Youth Centers with details and locations
* Specialized Technology Clubs & Open Clubs
* Swimming pools and open stadiums directory

#### **Engagement**

* Real-time news feed and announcements
* Browse and view upcoming activities and events
* Quick access contact channels with the ministry

#### **User Experience**

* Integrated map directions (external maps)
* Rich media: sliders, galleries, and detailed pages

---

### 💻 Web Dashboard (Admin Panel)

A complete management system for ministry administrators.

#### **Core Features**

* **Content Management:** Create / update / delete news and activities
* **Facility Management:** Manage youth centers, clubs, and facility data
* **Secure Authentication:** Role-based access, JWT-based
* **Interactive Maps:** Visual management of location data
* **Real-time updates** for mobile clients

---

### ⚙️ Backend API

The backbone that powers both the mobile and web applications.

#### **Key Functionalities**

* **RESTful API Architecture**
* JWT authentication and session management
* Rate limiting and API security
* File uploads (images & media)
* Entities: Activities, News, Centers, Users, Federations, etc.

---

## 🛠️ Technology Stack

| Component        | Technology            | Key Libraries                                       |
| ---------------- | --------------------- | --------------------------------------------------- |
| **Client (Web)** | Next.js 15 (React 19) | TypeScript, Tailwind CSS 4, Radix UI, GSAP, Leaflet |
| **Mobile App**   | Flutter               | Dart, BLoC (State Management), Dio                  |
| **Backend**      | Node.js / Express     | MongoDB (Mongoose), JWT, Bcrypt, Multer             |

---

## 📂 High-Level Project Structure

```
project/
├─ client/         # Next.js web application
├─ backend/        # Express.js backend API
└─ mobile_app/     # Flutter mobile application
```

---

# 🧩 Architecture & Folder Structure

Below is the detailed breakdown for each track.

---

## 🌐 Frontend (Next.js)

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
```

---

## 🖥️ Backend (Node.js / Express with Prisma)

```
src/
├─ app.module.ts            # Root module
├─ main.ts                  # App entry point
├─ auth/                    # Authentication (JWT, guards)
├─ users/                   # User and role management
├─ centers/                 # Centers CRUD operations
├─ activities/              # Activities management
├─ news/                    # News module
├─ files/                   # File uploads and storage
├─ common/                  # Shared utilities and decorators
├─ prisma/                  # Prisma schema and service
└─ config/                  # Environment and settings
```

---

## 📱 Mobile (Flutter)

```
android/        # Android native configuration
ios/            # iOS native configuration
lib/
├─ models/      # Data models
├─ modules/     # Screens (home, clubs, activities, etc.)
├─ layout/      # State management (Cubit/Bloc)
├─ shared/      # Common components, themes, helpers, networking
└─ main.dart    # App entry point
assets/         # Local JSON datasets (centers, clubs, federations)
test/           # Unit & widget tests
web/            # Web app entry
windows/        # Desktop build target
macos/
linux/
```

---

## 📑 Conclusion

The **Ministry of Youth & Sports Management System** provides a unified platform that empowers both the public and ministry administrators. By combining modern mobile technology, a dynamic web dashboard, and a scalable backend, the system delivers:

* Faster access to information
* Improved engagement and outreach
* Streamlined internal operations
* A more connected youth and sports ecosystem
