# Ministry of Youth & Sports Management System

A multi-application digital platform built to support public access to youth and sports information while giving administrators a structured system for managing centers, activities, news, and related operational content.

The ecosystem is composed of three connected applications:

- **Web Client** — public landing experience + administrative dashboard
- **Backend API** — authentication, content/facility data, media handling, and shared business logic
- **Mobile App** — public-facing Flutter application for browsing ministry-related information and facilities

> The repositories are private, while the organization profile documents the product architecture and engineering scope at a high level.

## Product Scope

The platform supports two main audiences:

### Public / Citizen Experience

- Browse youth centers and sports-related facilities
- Explore clubs, swimming pools, open stadiums, and specialized clubs
- Read news and activities
- Access location-related information and map directions
- Consume rich media and informational content through the mobile experience

### Administration Experience

- Authenticated dashboard access
- Manage youth centers and facility records
- Create, update, and delete activities
- Create, update, and delete news content
- Manage location-aware content through map-enabled interfaces
- Publish operational content consumed by public-facing clients

## System Architecture

```text
                    ┌──────────────────────┐
                    │   Backend REST API   │
                    │ Express + MongoDB    │
                    └──────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
        ┌────────▼────────┐         ┌────────▼────────┐
        │   Web Client    │         │   Mobile App    │
        │ Next.js / React │         │ Flutter / Dart  │
        └─────────────────┘         └─────────────────┘
```

The backend is the shared data and authentication layer for both client applications.

## Technology Stack

| Component | Core Technology | Supporting Libraries / Tools |
| --- | --- | --- |
| **Web Client** | Next.js 15, React 19, TypeScript | Tailwind CSS 4, React Hook Form, Zod, Radix UI, GSAP, Leaflet, Sonner |
| **Backend API** | Node.js, Express 4 | MongoDB, Mongoose, JWT, Cloudinary, Multer, Helmet, rate limiting, Winston |
| **Mobile App** | Flutter, Dart | BLoC, Dio, Carousel Slider, URL Launcher |

## Web Client

The web repository combines a public information website with a protected administrative dashboard.

### Main capabilities

- Public landing and informational sections
- Administrator authentication
- Center management
- Activity management
- News management
- Schema-driven CRUD forms using React Hook Form + Zod
- Map-enabled location interfaces with Leaflet
- RTL / Arabic-first UI
- Loading, feedback, and responsive states

### Frontend structure

```text
src/
├── app/                 # Next.js routes, landing pages, dashboard and auth
├── components/          # Feature, global and UI components
├── constants/           # Shared content/configuration
├── hooks/               # Reusable React hooks
├── lib/                 # Validation schemas and shared helpers
├── providers/           # Authentication/context providers
├── types/               # TypeScript contracts
└── utils/               # API utilities grouped by domain
```

## Backend API

The backend is an **Express + MongoDB/Mongoose** service organized around conventional Node.js application layers.

```text
src/
├── app.js               # Application bootstrap
├── config/              # Environment and infrastructure configuration
├── controllers/         # Request handlers
├── middleware/          # Authentication, validation and security middleware
├── models/              # Mongoose models
├── routes/              # REST API routes
└── utils/               # Shared helpers
```

### Backend capabilities

- RESTful API architecture
- JWT-based authentication
- MongoDB persistence through Mongoose
- Media/file upload handling
- Cloudinary integration
- Request rate limiting
- Security hardening with Helmet, sanitization and HPP/XSS protections
- Structured request/application logging
- Jest + Supertest testing setup

## Mobile Application

The Flutter application acts as the public mobile experience and consumes the shared backend APIs.

Its current technology foundation includes:

- Flutter / Dart
- BLoC for state management
- Dio for API communication
- Carousel and media-focused interfaces
- URL launcher integration
- Local data assets for clubs, federations, swimming pools, technical clubs, and open stadiums

## Repositories

| Repository | Responsibility | Visibility |
| --- | --- | --- |
| `Ministry-Of-Youth-Sports/client` | Next.js public website + admin dashboard | Private |
| `Ministry-Of-Youth-Sports/backend` | Express / MongoDB REST API | Private |
| `Ministry-Of-Youth-Sports/mobile_app` | Flutter public mobile application | Private |
| `Ministry-Of-Youth-Sports/.github` | Public organization profile and project overview | Public |

## Web Deployment

The web client repository references the deployed frontend at:

**https://ministryyouthsports.vercel.app**

## Engineering Practices

Across the platform, the repositories use patterns such as:

- Separation of UI, API access, validation, and domain utilities
- Feature-oriented frontend organization
- Schema-driven forms and validation
- Backend controller / model / route separation
- Authentication middleware and protected routes
- Environment-based configuration
- Security-focused API middleware
- Automated backend testing

## Project Status

This repository set represents the completed platform implementation delivered for the project. Individual components may still receive maintenance or operational updates over time.
