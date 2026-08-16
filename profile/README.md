# Ministry of Youth & Sports — Digital Platform

**Multi-application platform for public access to youth and sports information, facility discovery, news, activities, and structured administration of ministry content.**

The organization contains three connected product tracks:

- **Web Client** — public website + protected administration dashboard
- **Backend API** — authentication, persistence, media, validation, and shared data services
- **Mobile App** — public Flutter application for youth/sports information and facility discovery

The application repositories are private. This public organization profile documents the product architecture and engineering scope at a high level.

---

## Platform Goals

The platform supports two main audiences.

### Public / Citizen Experience

- Discover youth centers
- Browse sports clubs and federations
- Explore swimming pools, open stadiums, and technology clubs
- Read news and activities
- Access facility/location information
- Use mobile-friendly public information flows

### Administration Experience

- Authenticate into a protected dashboard
- Manage youth/sports centers
- Create and update activities
- Create and update news
- Work with location-aware center data
- Publish data consumed by public-facing clients

---

## System Architecture

```text
                          ┌──────────────────────────┐
                          │      Backend API         │
                          │ Express + MongoDB        │
                          │ auth + data + media      │
                          └────────────┬─────────────┘
                                       │
                         shared REST/data contracts
                                       │
                   ┌───────────────────┴───────────────────┐
                   │                                       │
        ┌──────────▼──────────┐                 ┌──────────▼──────────┐
        │ Web Client          │                 │ Mobile App          │
        │ Next.js 15          │                 │ Flutter / Dart      │
        │ public + admin      │                 │ public experience   │
        └─────────────────────┘                 └─────────────────────┘
```

The backend is the authoritative security and persistence layer shared by both client applications.

---

## Product 1 — Web Client

Repository: `Ministry-Of-Youth-Sports/client`

The web application combines a public landing/information experience with a protected admin dashboard.

### Public website capabilities

- Ministry/platform presentation
- Landing sections and informational content
- Responsive public UI
- Arabic-first / RTL-oriented experience
- Supporting interaction and animation

### Administration capabilities

- Login/authentication flow
- Center listing, creation, detail, and update
- Activity listing, creation, and update
- News listing, creation, and update
- Map/location-aware center interfaces
- React Hook Form + Zod validation
- Resource-specific API utilities

### Web stack

- Next.js 15.4.6
- React 19 RC
- TypeScript
- Tailwind CSS 4
- React Hook Form
- Zod 4
- GSAP
- Leaflet / React Leaflet
- Radix UI
- Sonner

Deployed web client:

**https://ministryyouthsports.vercel.app**

---

## Product 2 — Backend API

Repository: `Ministry-Of-Youth-Sports/backend`

The backend is an Express/MongoDB service responsible for shared data and security-sensitive operations.

### Backend capabilities

- JWT-based authentication
- Password hashing
- Protected administration APIs
- MongoDB persistence through Mongoose
- Center/facility data
- Activities
- News
- Media uploads
- Cloudinary integration
- Request validation
- Rate limiting
- Security headers and request hardening
- Structured logging
- Jest/Supertest testing

### Backend stack

- Node.js
- Express 4.18.2
- MongoDB
- Mongoose 8
- JWT
- bcryptjs
- Cloudinary
- Multer
- Helmet
- express-rate-limit
- express-validator
- Winston
- Jest
- Supertest

### Security layers

The backend includes controls such as:

- Helmet
- CORS
- Request throttling
- MongoDB query sanitization
- HPP protection
- XSS-related sanitization
- Backend-enforced protected routes

Frontend route protection is treated as an access/UX layer, not the final security boundary.

---

## Product 3 — Mobile Application

Repository: `Ministry-Of-Youth-Sports/mobile_app`

The Flutter application provides public access to youth/sports information.

### Mobile content areas

- Youth centers
- Sports clubs
- Sports federations
- Swimming pools
- Open stadiums
- Technology clubs
- Activities
- News
- Contact information
- Geographic/direction-based center views

### Mobile stack

- Flutter
- Dart ^3.8.1
- flutter_bloc / Cubit
- Dio
- carousel_slider
- smooth_page_indicator
- url_launcher
- Flutter Test

### Local reference data

The app also includes bundled JSON datasets for:

- Clubs
- Federations
- Swimming pools
- Technical clubs
- Open stadiums

---

## Shared Data Flow

```text
Admin edits center/activity/news
        ↓
Web client validates input
        ↓
Backend validates + persists
        ↓
MongoDB stores authoritative record
        ↓
Public web/mobile clients request updated data
```

This keeps business data centralized instead of allowing each client to maintain independent copies of operational state.

---

## Repository Map

| Repository | Responsibility | Visibility |
| --- | --- | --- |
| `Ministry-Of-Youth-Sports/client` | Next.js public website + admin dashboard | Private |
| `Ministry-Of-Youth-Sports/backend` | Express/MongoDB backend API | Private |
| `Ministry-Of-Youth-Sports/mobile_app` | Flutter public mobile application | Private |
| `Ministry-Of-Youth-Sports/.github` | Public organization profile | Public |

---

## Engineering Practices

Across the platform, the repositories use patterns such as:

- Separation of UI, data access, validation, and domain concerns
- Resource-oriented frontend API utilities
- Schema-driven forms
- Protected client routes plus backend authorization
- Controller/model/route separation in Express
- Environment-based configuration
- Security middleware on public/protected APIs
- Reusable Flutter modules and shared networking
- Static analysis/testing before handoff

---

## Project Status

The organization represents the delivered Ministry of Youth & Sports platform implementation. Individual components may continue to receive maintenance, compatibility, content, security, or operational improvements.
