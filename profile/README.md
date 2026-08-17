# Ministry of Youth & Sports — Digital Platform

> A connected public-information and administration platform for youth and sports services, facilities, activities, news, geographic discovery, and structured content management across web, backend, and mobile applications.

**Web deployment:** https://ministryyouthsports.vercel.app

The Ministry of Youth & Sports platform is a multi-application system designed to serve two very different audiences:

- **Citizens and public users**, who need clear access to information about youth centers, sports-related facilities, clubs, federations, activities, news, and locations.
- **Internal administrators**, who need a protected interface for maintaining the data that public users see.

The organization is built around three connected repositories:

1. A **Next.js web client** containing the public website and protected administration dashboard.
2. A **Node.js / Express backend** that owns persistence, authentication, authorization, validation, uploads, logging, and shared API behavior.
3. A **Flutter mobile application** that provides a public mobile experience across youth/sports facilities, activities, news, and location-oriented content.

The applications are separate, but they are not unrelated. The web dashboard publishes and maintains operational content through the backend; the backend stores and protects the authoritative records; public web and mobile experiences consume those records and supporting reference data.

---

## Table of Contents

- [What This Platform Is](#what-this-platform-is)
- [Why It Exists](#why-it-exists)
- [Who Uses It](#who-uses-it)
- [Platform Goals](#platform-goals)
- [System Architecture](#system-architecture)
- [Repository Map](#repository-map)
- [Source of Truth](#source-of-truth)
- [Web Client](#web-client)
  - [Web Responsibilities](#web-responsibilities)
  - [Public Experience](#public-experience)
  - [Administration Experience](#administration-experience)
  - [Admin Route Structure](#admin-route-structure)
  - [Center Management](#center-management)
  - [Activity Management](#activity-management)
  - [News Management](#news-management)
  - [Authentication](#authentication)
  - [Forms and Validation](#forms-and-validation)
  - [Maps and Location UX](#maps-and-location-ux)
  - [Animation and Interaction](#animation-and-interaction)
  - [Web Technology](#web-technology)
  - [Web Development Workflow](#web-development-workflow)
- [Backend API](#backend-api)
  - [Backend Responsibilities](#backend-responsibilities)
  - [Runtime and Architecture](#runtime-and-architecture)
  - [API Domains](#api-domains)
  - [Authentication and Authorization](#authentication-and-authorization)
  - [Security Middleware](#security-middleware)
  - [Rate Limiting](#rate-limiting)
  - [Request Validation](#request-validation)
  - [File Uploads and Media](#file-uploads-and-media)
  - [Logging and Error Handling](#logging-and-error-handling)
  - [Health Monitoring](#health-monitoring)
  - [Database](#database)
  - [Center Data Model](#center-data-model)
  - [Center Membership Data](#center-membership-data)
  - [Center Activity Relations](#center-activity-relations)
  - [Activities Data Model](#activities-data-model)
  - [Activity Validation Rules](#activity-validation-rules)
  - [Activity Search and Indexing](#activity-search-and-indexing)
  - [News Data Model](#news-data-model)
  - [Arabic-Aware Slugs](#arabic-aware-slugs)
  - [Facility APIs](#facility-apis)
  - [Backend Technology](#backend-technology)
  - [Backend Testing and Tooling](#backend-testing-and-tooling)
- [Mobile Application](#mobile-application)
  - [Mobile Responsibilities](#mobile-responsibilities)
  - [Mobile Architecture](#mobile-architecture)
  - [Home Experience](#home-experience)
  - [Youth Centers](#youth-centers)
  - [Youth Center Directions](#youth-center-directions)
  - [Sports Clubs](#sports-clubs)
  - [Sports Federations](#sports-federations)
  - [Swimming Pools](#swimming-pools)
  - [Open Stadiums and Playgrounds](#open-stadiums-and-playgrounds)
  - [Technology Clubs](#technology-clubs)
  - [Activities](#activities)
  - [News](#news)
  - [Contact](#contact)
  - [Bundled Reference Data](#bundled-reference-data)
  - [Networking](#networking)
  - [State Management](#state-management)
  - [Mobile Technology](#mobile-technology)
- [How the Applications Work Together](#how-the-applications-work-together)
- [Core Product Flows](#core-product-flows)
  - [Admin Login Flow](#admin-login-flow)
  - [Create or Update Center Flow](#create-or-update-center-flow)
  - [Create Activity Flow](#create-activity-flow)
  - [Publish News Flow](#publish-news-flow)
  - [Public Data Consumption Flow](#public-data-consumption-flow)
  - [Facility Discovery Flow](#facility-discovery-flow)
- [Data Ownership](#data-ownership)
- [Security Boundaries](#security-boundaries)
- [Public vs Protected Responsibilities](#public-vs-protected-responsibilities)
- [Location and Geographic Data](#location-and-geographic-data)
- [Arabic-First Product Considerations](#arabic-first-product-considerations)
- [Validation Strategy](#validation-strategy)
- [Media Strategy](#media-strategy)
- [Error and Loading States](#error-and-loading-states)
- [Testing Strategy](#testing-strategy)
- [Engineering Conventions](#engineering-conventions)
- [Development and Release](#development-and-release)
- [Environment and Configuration](#environment-and-configuration)
- [Operational Considerations](#operational-considerations)
- [Privacy and Sensitive Data](#privacy-and-sensitive-data)
- [Project Status](#project-status)
- [Repository Guide for Reviewers](#repository-guide-for-reviewers)
- [In Short](#in-short)

---

# What This Platform Is

The Ministry of Youth & Sports platform is a digital information and management system.

It combines public access with internal administration.

The public side focuses on helping users discover information such as:

- youth centers,
- sports clubs,
- sports federations,
- swimming pools,
- open stadiums,
- technology clubs,
- activities,
- news,
- center contact information,
- and location/direction-related information.

The administration side focuses on maintaining the dynamic information that should not be hardcoded permanently into public interfaces.

The backend provides the shared security and persistence layer so the system does not rely on separate copies of business data inside each client.

---

# Why It Exists

A ministry-facing youth and sports platform has a different job from a normal marketing website.

The problem is not just:

> “Show a homepage.”

The system needs to organize several categories of public information and provide internal teams with a way to maintain the most dynamic records.

A useful model is:

```text
Public information
      +
Dynamic administration
      +
Shared backend
      +
Mobile access
      =
Connected digital platform
```

Without a shared backend, the web and mobile applications could easily drift into different representations of centers, activities, and news.

Without an admin interface, routine content updates would require direct source-code changes.

Without public-facing web/mobile experiences, the maintained data would not reach citizens in a practical format.

---

# Who Uses It

The platform supports at least two broad groups.

## Public users

Public users are primarily interested in discovery and information.

Typical goals include:

- Find a youth center.
- Review a center's location or contact details.
- Browse activities.
- Read ministry-related news.
- Explore clubs and federations.
- Find swimming pools or open sports facilities.
- Explore technology clubs.
- Open relevant external/location links.
- Use the information from mobile devices.

## Administrators

Administrators need controlled access to content-management workflows.

The web application includes a login flow and a protected dashboard for resources such as:

- centers,
- activities,
- news.

The backend also includes role middleware, authentication middleware, validation, and protected APIs so the dashboard is not the only security layer.

---

# Platform Goals

## Public accessibility

Make youth and sports information easier to discover through modern web and mobile interfaces.

## Centralized dynamic data

Keep records such as centers, activities, and news in a shared backend rather than duplicating them between clients.

## Controlled administration

Give authorized users dedicated management interfaces.

## Geographic usefulness

Support center/facility discovery with location-oriented data and map-aware web experiences.

## Arabic-friendly workflows

Support Arabic data and Arabic-oriented UI behavior, including Arabic-aware slugs and localized date formatting in backend models.

## Secure administration

Protect privileged operations through backend authentication, role logic, validation, sanitization, and rate limiting.

## Multi-client consistency

Allow web and mobile clients to consume the same dynamic backend records where appropriate.

---

# System Architecture

The architecture is client/server with two primary client experiences.

```text
┌──────────────────────────────────────────────────────────────────┐
│            MINISTRY OF YOUTH & SPORTS DIGITAL PLATFORM           │
└──────────────────────────────────────────────────────────────────┘

                         PUBLIC + ADMIN WEB
                         Next.js / React
                               │
                               │
                               │ REST/API
                               ▼
                    ┌──────────────────────┐
                    │   Backend API        │
                    │ Node.js + Express    │
                    │                      │
                    │ • auth               │
                    │ • centers            │
                    │ • activities         │
                    │ • news               │
                    │ • facility data      │
                    │ • validation         │
                    │ • uploads            │
                    │ • security           │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ MongoDB / Mongoose   │
                    └──────────┬───────────┘
                               ▲
                               │
                               │ REST/API where dynamic data applies
                               │
                         FLUTTER MOBILE APP
                         public experience
```

The mobile app also contains bundled JSON reference datasets for several facility categories.

That means not every mobile screen necessarily depends on a network request for every record.

---

# Repository Map

| Repository | Responsibility | Main Stack |
| --- | --- | --- |
| `Ministry-Of-Youth-Sports/client` | Public web experience + protected admin dashboard | Next.js 15, React 19 RC, TypeScript |
| `Ministry-Of-Youth-Sports/backend` | Shared API, auth, persistence, security, validation, uploads | Node.js, Express, MongoDB/Mongoose |
| `Ministry-Of-Youth-Sports/mobile_app` | Public mobile experience | Flutter, Dart, BLoC, Dio |
| `Ministry-Of-Youth-Sports/.github` | Public organization profile | Markdown |

The application repositories may be private while the organization profile remains public.

---

# Source of Truth

One of the most important documentation rules for this organization is:

> The current source code is the technical source of truth.

Older specifications or summaries should not override the actual implementation.

For example, the current backend is:

```text
Node.js
Express 4.18.2
MongoDB
Mongoose
```

not NestJS/Prisma/PostgreSQL.

This organization README intentionally reflects the current implementation.

---

# Web Client

Repository:

`Ministry-Of-Youth-Sports/client`

Deployment:

**https://ministryyouthsports.vercel.app**

The web application contains both the public website and the administration area.

---

## Web Responsibilities

The Next.js application handles:

- public presentation,
- responsive UI,
- landing content,
- navigation,
- login UI,
- dashboard routes,
- center management,
- activity management,
- news management,
- form input,
- client-side validation,
- map/location interfaces,
- loading states,
- API integration,
- animation and visual interaction.

---

# Public Experience

The public web experience is responsible for communicating the ministry/youth-sports platform clearly.

The current dependency set supports:

- responsive layouts,
- animated sections,
- sliders/carousels,
- timelines,
- smooth page interaction,
- dialogs/selects/popovers,
- location-aware interfaces,
- date handling,
- toasts and feedback.

The public application should remain focused on discovery and communication rather than exposing administration controls.

---

# Administration Experience

The administration section lives under:

```text
src/app/dashboard-admin/
```

The current protected resource areas include:

```text
activities/
centers/
news/
```

with their own dashboard layout and loading state.

This gives each major managed domain its own route family.

---

# Admin Route Structure

At a high level:

```text
src/app/
├── dashboard-admin/
│   ├── activities/
│   ├── centers/
│   ├── news/
│   ├── layout.tsx
│   └── loading.tsx
├── login/
├── actions.ts
├── layout.tsx
├── loading.tsx
└── page.tsx
```

This separation keeps login, public pages, and admin pages conceptually distinct.

---

# Center Management

Centers are a major business domain.

The web dashboard supports administrative workflows around youth/sports centers.

The backend model shows that a center can contain:

- name,
- phone,
- address,
- Facebook link,
- location,
- area,
- region,
- image,
- sports activities,
- social activities,
- art activities,
- membership information,
- timestamps.

Center administration therefore goes beyond editing a name and address.

---

# Activity Management

Activities have their own admin area.

The backend activity model contains fields for:

- project/activity name,
- coordinator,
- phone number,
- location,
- date,
- time,
- duration in days,
- participant count,
- target age range,
- gender,
- access type,
- notes,
- slug,
- status,
- timestamps.

This makes activity creation a structured workflow rather than an unvalidated free-text post.

---

# News Management

News also has its own admin route.

The backend news model contains:

- title,
- content,
- image,
- social link,
- slug,
- timestamps.

The model also provides:

- Arabic-compatible slug generation,
- formatted date virtuals,
- search indexes.

---

# Authentication

The web application includes a dedicated login route.

Authentication requests are sent to the backend.

The frontend can control navigation based on auth state, but the backend remains responsible for validating credentials and protecting privileged operations.

A normal flow is:

```text
Admin opens login
      ↓
Credentials submitted
      ↓
Backend authentication
      ↓
JWT/session token returned/used
      ↓
Dashboard navigation becomes available
      ↓
Protected API calls still require backend authorization
```

---

# Forms and Validation

The web client uses:

- React Hook Form
- Zod
- `@hookform/resolvers`

This allows forms to express validation rules as schemas rather than scattering checks throughout UI components.

Client validation exists for usability.

Server validation exists for trust.

---

# Maps and Location UX

The web client includes:

- Leaflet
- React Leaflet

The center domain also contains location-oriented fields such as:

- location,
- LocationArea,
- region,
- address.

This supports map/location-aware interfaces around centers and public discovery.

---

# Animation and Interaction

The web stack includes:

- GSAP
- `@gsap/react`
- Swiper
- react-scroll
- React Vertical Timeline
- Sonner
- Radix UI

These libraries support richer public storytelling and controlled dashboard interaction.

Animation should remain an enhancement rather than replacing semantic content or navigation.

---

# Web Technology

## Framework

- Next.js 15.4.6
- React 19 RC
- React DOM 19 RC
- TypeScript 5
- App Router
- Turbopack development mode

## Styling

- Tailwind CSS 4
- tailwind-merge
- class-variance-authority
- clsx
- tw-animate-css

## Forms

- React Hook Form
- Zod 4
- Hook Form resolvers

## UI

- Radix UI
- Lucide React
- React Icons
- cmdk
- Sonner
- React Day Picker

## Maps

- Leaflet
- React Leaflet

## Motion and content presentation

- GSAP
- `@gsap/react`
- Swiper
- react-scroll
- React Vertical Timeline

## Dates

- date-fns
- Moment

---

# Web Development Workflow

The current scripts include:

```bash
npm run dev
npm run build
npm run start
npm run lint
```

Development uses:

```bash
next dev --turbopack
```

Production uses:

```bash
next build
next start
```

---

# Backend API

Repository:

`Ministry-Of-Youth-Sports/backend`

Default/source branch currently used for the backend code:

```text
backend
```

The backend is implemented as an Express application.

---

## Backend Responsibilities

The backend owns:

- database connectivity,
- authentication,
- authorization middleware,
- role checks,
- centers,
- activities,
- activity types,
- news,
- technology clubs,
- playgrounds/open sports facilities,
- swimming pools,
- validation,
- file upload handling,
- Cloudinary integration,
- API security middleware,
- rate limiting,
- response compression,
- logging,
- centralized error handling,
- health checks,
- testing.

---

# Runtime and Architecture

The source is organized into:

```text
src/
├── app.js
├── config/
├── controllers/
├── middleware/
├── models/
├── routes/
└── utils/
```

The request flow generally follows:

```text
Request
   ↓
Express middleware
   ↓
Route
   ↓
Validation / auth / role checks where required
   ↓
Controller
   ↓
Mongoose model / service-style logic
   ↓
MongoDB
   ↓
Response
```

---

# API Domains

The main application mounts the following API groups:

```text
/api/v1/news
/api/v1/auth
/api/v1/activities
/api/v1/centers
/api/v1/activity-types
/api/v1/tech-clubs
/api/v1/playgrounds
/api/v1/swimming-pools
```

This route map is one of the clearest summaries of the backend's actual product domains.

---

# Authentication and Authorization

The backend uses:

- JSON Web Tokens
- bcryptjs
- auth middleware
- role middleware

Authentication should be understood in two parts.

## Identity

JWT/auth middleware verifies who the caller is.

## Authorization

Role middleware decides whether that authenticated identity is permitted to perform the requested action.

Frontend route hiding does not replace these checks.

---

# Security Middleware

The server applies several security layers.

## Helmet

Adds security-oriented HTTP headers.

## CORS

Controls which browser origins can make credentialed requests.

The server supports:

```text
GET
POST
PUT
DELETE
PATCH
OPTIONS
```

and allows authorization/content-related headers.

## Mongo sanitization

`express-mongo-sanitize` is used against malicious Mongo-style query injection.

## XSS cleaning

`xss-clean` is applied to request data.

## HPP

HTTP parameter pollution protection is enabled.

## Rate limiting

API routes are rate limited.

## Compression

Responses are compressed for transfer efficiency.

## Cookie parsing

Cookies can be parsed centrally.

---

# Rate Limiting

The backend applies a limiter to:

```text
/api
```

with a configured window of:

```text
15 minutes
```

and a limit of:

```text
100 requests per IP per window
```

in the current source.

The server also enables `trust proxy`, which matters when deployed behind a proxy/load balancer such as Render-style hosting.

---

# Request Validation

The backend includes:

- general validation middleware,
- activity-specific validation middleware,
- express-validator,
- schema-level Mongoose validation.

That gives the system multiple opportunities to reject malformed data.

For important business fields, backend validation is the final authority.

---

# File Uploads and Media

The backend includes:

- Multer
- Cloudinary
- upload middleware
- static `/uploads` serving

This allows media workflows to remain server-managed.

The web dashboard should send supported files; it should not own Cloudinary credentials.

---

# Logging and Error Handling

The server includes:

- Morgan
- Winston
- logger middleware
- centralized error handler

Development logging uses the `dev` Morgan format.

Non-development logging can use combined logging with the Winston stream.

Unhandled promise rejections are also handled at process level by closing the server before exit.

---

# Health Monitoring

The backend exposes:

```text
GET /health
```

The response includes:

- status,
- message,
- timestamp,
- process uptime,
- database connection state.

This is useful for deployment checks and operational diagnostics.

A frontend failure can therefore be separated from:

- backend process failure,
- database disconnect,
- client-only problems.

---

# Database

The backend uses:

- MongoDB
- Mongoose 8

Mongoose schemas are used to model:

- centers,
- activities,
- news,
- users,
- category-specific activities,
- and additional facility domains.

---

# Center Data Model

The `Center` schema includes:

```text
name
phone
address
facebookLink
location
LocationArea
region
image
sportsActivities
socialActivities
artActivities
membership
timestamps
```

This represents more than a simple geolocation point.

It combines public facility information with activity relationships and membership information.

---

# Center Membership Data

Membership information currently includes fields for:

- father ID image,
- birth certificate image,
- personal photos,
- utility bill image,
- phone,
- first-time price,
- renewal price.

This data is potentially sensitive.

It should not be treated the same way as public center name/address data.

Access controls and privacy handling matter.

---

# Center Activity Relations

The center schema contains references to:

- `SportActivity`
- `SocialActivity`
- `ArtActivity`

Conceptually:

```text
Center
 ├─ Sports Activities
 ├─ Social Activities
 └─ Art Activities
```

This lets center information connect to structured activity categories rather than embedding every activity as a single untyped array of strings.

---

# Activities Data Model

The main Activity schema includes a detailed operational structure.

Fields include:

```text
projectName
coordinatorName
phoneNumber
location
date
time
daysCount
participantsCount
targetAge.min
targetAge.max
gender
accessType
notes
slug
status
timestamps
```

The model is intentionally Arabic-oriented in several validation messages and enum values.

---

# Activity Validation Rules

The model enforces constraints such as:

## Project name

- required,
- trimmed,
- maximum length.

## Coordinator

- required,
- trimmed,
- bounded length.

## Egyptian phone number

The model validates Egyptian mobile-number format.

## Location

Required and length-limited.

## Date

Must be today or a future date.

## Time

Validated as a clock-style time.

## Days

Must be at least 1 and no more than 365.

## Participant count

Bounded between 1 and 10,000.

## Target age

Both min/max are validated and max cannot be lower than min.

## Gender

Allowed values:

```text
بنين
بنات
مختلط
```

## Access type

Allowed values:

```text
الأعضاء فقط
للجميع
```

## Status

Allowed states include:

```text
مجدول
جاري
ملغي
```

These validations turn an activity into structured operational data.

---

# Activity Search and Indexing

The Activity schema creates indexes for:

- text search across project name, location, coordinator,
- date,
- status,
- slug,
- creation time.

This supports common administrative and public retrieval patterns.

---

# News Data Model

The News schema includes:

```text
title
content
image
socialLink
slug
timestamps
```

Validation includes:

- required title,
- title length,
- required content,
- minimum content length,
- optional URL validation for social links.

---

# Arabic-Aware Slugs

Both activity and news models contain slug-generation logic that preserves Arabic characters.

This is important for Arabic-first content.

The activity slug logic also includes duplicate handling and fallback generation.

The news slug logic provides a timestamp-based fallback when a usable slug cannot be generated.

---

# Facility APIs

In addition to centers, activities, and news, the backend mounts APIs for:

- technology clubs,
- playgrounds,
- swimming pools.

These domains align with facility categories visible in the mobile experience.

---

# Backend Technology

## Runtime

- Node.js

## Web server

- Express 4.18.2

## Database

- MongoDB
- Mongoose 8

## Authentication

- jsonwebtoken
- bcryptjs

## Security

- Helmet
- CORS
- express-rate-limit
- express-mongo-sanitize
- xss-clean
- hpp

## Validation

- express-validator
- Mongoose validation

## Uploads/media

- Multer
- Cloudinary

## Logging

- Morgan
- Winston

## Utilities

- compression
- cookie-parser
- dotenv
- xlsx
- http-status-codes
- express-async-handler

---

# Backend Testing and Tooling

The backend includes:

- Jest
- Supertest
- ESLint
- Airbnb base config
- Prettier
- Husky
- lint-staged
- Nodemon

Scripts include:

```bash
npm run start
npm run dev
npm run test
npm run test:watch
npm run test:coverage
npm run lint
npm run lint:fix
npm run format
```

---

# Mobile Application

Repository:

`Ministry-Of-Youth-Sports/mobile_app`

The mobile app is implemented with Flutter.

Its role is public access to ministry/youth-sports information.

---

# Mobile Responsibilities

The mobile app includes experiences around:

- home,
- youth centers,
- youth center information,
- youth center places,
- directions,
- sports clubs,
- sports federations,
- swimming pools,
- open clubs/stadium-like facilities,
- technology clubs,
- activities,
- news,
- contact information.

---

# Mobile Architecture

The current `lib` structure contains:

```text
lib/
├── bloc_observer.dart
├── layout/
├── main.dart
├── models/
├── modules/
└── shared/
```

This is a practical Flutter organization separating:

- app entry,
- layout,
- models,
- feature screens,
- reusable/shared infrastructure.

---

# Home Experience

The mobile home module acts as a central entry point into the public experience.

It can connect users to the platform's major content/facility categories.

---

# Youth Centers

The mobile code contains dedicated modules for:

- youth center information,
- youth center places.

This reflects two different user needs:

```text
"What does this center offer?"
```

and:

```text
"Where is this center?"
```

---

# Youth Center Directions

There is a dedicated `centers_directions` module.

This indicates that geographic navigation is treated as a distinct mobile workflow rather than being reduced to plain address text.

---

# Sports Clubs

The app includes a dedicated sports-clubs screen.

Club information can also use bundled local reference data from:

```text
assets/json/clubs.json
```

---

# Sports Federations

The app has its own sports-federations module.

Bundled federation data lives in:

```text
assets/json/federations.json
```

---

# Swimming Pools

The mobile app includes a swimming-pool screen.

Bundled pool reference data lives in:

```text
assets/json/swimming_pool.json
```

The backend also exposes a swimming-pools API domain.

---

# Open Stadiums and Playgrounds

The mobile assets include:

```text
assets/json/open_stadiums.json
```

The backend mounts:

```text
/api/v1/playgrounds
```

This provides both reference-data and dynamic-backend foundations for sports facility discovery.

---

# Technology Clubs

The mobile app includes a dedicated technology-clubs screen.

Bundled data is available at:

```text
assets/json/technical_clubs.json
```

The backend also mounts:

```text
/api/v1/tech-clubs
```

---

# Activities

The mobile app contains an activities screen.

Dynamic activity data can be served through the backend's activities API.

---

# News

The mobile app contains a "show all news" module.

The backend's news API provides the dynamic domain for news content.

---

# Contact

The mobile app includes a Contact Us screen.

Contact information can be presented separately from facilities and news.

---

# Bundled Reference Data

The current Flutter configuration includes JSON assets for:

```text
federations.json
clubs.json
swimming_pool.json
technical_clubs.json
open_stadiums.json
```

This can be useful for reference-heavy datasets that do not need to be fetched on every screen load.

It also means developers need to distinguish:

- local reference data,
- dynamic backend data.

They are not automatically the same source.

---

# Networking

The mobile app includes:

- Dio

Dio provides HTTP client capability for dynamic backend communication.

---

# State Management

The mobile app uses:

- flutter_bloc

and includes a custom BLoC observer.

This provides a structured way to observe and manage state transitions rather than relying entirely on local widget state.

---

# Mobile Technology

## Core

- Flutter
- Dart `^3.8.1`

## Networking

- Dio 5.9

## State

- flutter_bloc 9.1

## UI / presentation

- carousel_slider
- smooth_page_indicator
- conditional_builder_null_safety
- Cupertino icons

## External actions

- url_launcher

## Testing and linting

- flutter_test
- flutter_lints

## App icon

- flutter_launcher_icons

---

# How the Applications Work Together

The platform is strongest when understood as a connected system.

## Example: center update

```text
Admin opens center editor in web dashboard
        ↓
Current center data loaded
        ↓
Form is updated
        ↓
Client-side validation
        ↓
Backend request
        ↓
Auth / role validation
        ↓
Server validation
        ↓
Mongoose model update
        ↓
MongoDB persists
        ↓
Public clients request current data
```

## Example: news publication

```text
Admin creates news
      ↓
Frontend validates
      ↓
Backend validates/persists
      ↓
Arabic-aware slug generated
      ↓
Public web/mobile clients can consume news
```

---

# Core Product Flows

## Admin Login Flow

```text
Login page
    ↓
Credentials
    ↓
Auth API
    ↓
Password verification
    ↓
JWT issued/used
    ↓
Protected dashboard access
    ↓
Protected API mutations
```

---

# Create or Update Center Flow

```text
Dashboard → Centers
      ↓
Create/select center
      ↓
Enter:
  • name
  • contact data
  • location
  • region/area
  • image
  • activity relationships
  • supported membership data
      ↓
Frontend validation
      ↓
Backend auth/validation
      ↓
Mongoose persistence
      ↓
Public clients receive current center
```

---

# Create Activity Flow

```text
Dashboard → Activities
      ↓
Enter structured activity data
      ↓
Validate:
  • phone
  • date
  • time
  • participants
  • age range
  • gender
  • access type
      ↓
Backend validation
      ↓
Arabic-aware unique slug
      ↓
MongoDB
      ↓
Public activity views
```

---

# Publish News Flow

```text
Dashboard → News
      ↓
Title + content + optional image/social link
      ↓
Validation
      ↓
Backend persists
      ↓
Slug generated
      ↓
News API returns current content
      ↓
Web/mobile display
```

---

# Public Data Consumption Flow

```text
Public web/mobile
      ↓
API request
      ↓
Express route
      ↓
Controller / model query
      ↓
MongoDB
      ↓
Normalized response
      ↓
Public presentation
```

---

# Facility Discovery Flow

```text
User chooses facility category
      ↓
Dynamic API data or bundled reference data
      ↓
Facility list
      ↓
Facility detail/location
      ↓
Directions / external action when available
```

---

# Data Ownership

A connected multi-client system needs explicit ownership.

## Backend-owned dynamic state

Examples:

- centers,
- activities,
- news,
- user/auth records,
- dynamic facility records,
- protected admin changes.

## Web-owned temporary state

Examples:

- open dialogs,
- current form values,
- loading state,
- selected map point,
- temporary validation messages,
- current route.

## Mobile-owned temporary/reference state

Examples:

- current screen,
- BLoC state,
- locally bundled reference datasets,
- temporary network/loading state.

Clients should not become independent permanent databases for shared dynamic resources.

---

# Security Boundaries

The security model is layered.

```text
Admin UI
   ↓
Frontend route/access behavior
   ↓
Token-bearing request
   ↓
Backend auth middleware
   ↓
Role middleware
   ↓
Validation
   ↓
Controller
   ↓
MongoDB
```

Important rule:

> If a user manually calls the backend without the dashboard, the backend must still protect the operation.

---

# Public vs Protected Responsibilities

## Public

Public clients should be able to read safe public information.

Examples:

- centers,
- facility information,
- activities,
- news.

## Protected

Administrative actions may include:

- create,
- update,
- delete,
- upload,
- edit membership-related information,
- manage protected records.

The exact route protection should remain backend-enforced.

---

# Location and Geographic Data

The platform contains several location-related concepts.

### Web

Leaflet and React Leaflet support map UI.

### Center model

Fields include:

- address,
- location,
- LocationArea,
- region.

### Mobile

Dedicated youth-center place and direction modules exist.

This gives the platform multiple ways to help users move from information to physical location discovery.

---

# Arabic-First Product Considerations

The source reflects Arabic requirements in several ways.

## Activity validation messages

Many schema messages are Arabic.

## Gender/access/status enums

Examples use Arabic values.

## Slugs

Slug generation preserves Arabic Unicode ranges.

## Dates

Activity/news models include Arabic Egypt date formatting through:

```text
ar-EG
```

## UI direction

The product is oriented toward an Arabic public-sector audience and should preserve RTL usability where relevant.

---

# Validation Strategy

Validation should be layered.

```text
User enters form data
      ↓
React Hook Form / Zod
      ↓
Request
      ↓
Express validation middleware
      ↓
Mongoose schema validation
      ↓
Database
```

Each layer has a different purpose.

## Frontend

Fast feedback.

## Middleware

Request-shape and policy checks.

## Model

Persistence-level integrity.

---

# Media Strategy

Media can appear in:

- center images,
- news images,
- uploaded administrative content.

The backend uses:

- Multer,
- Cloudinary,
- `/uploads` static serving.

Production media configuration should remain environment-driven.

---

# Error and Loading States

The platform contains explicit loading/error infrastructure.

## Web

- root loading component,
- admin loading component,
- Sonner notifications.

## Backend

- centralized error middleware,
- async-handler package,
- process-level unhandled-rejection handling,
- health endpoint.

## Mobile

BLoC/conditional rendering can represent loading/success/error states.

A missing API response should not be silently treated as an empty dataset.

---

# Testing Strategy

## Backend

The backend has the strongest explicit automated test toolchain:

- Jest
- Supertest
- coverage command
- watch mode

This supports:

- unit-style behavior,
- request-level API testing,
- regression checks.

## Mobile

Flutter includes:

- flutter_test
- flutter_lints

## Web

The web repository exposes build/lint scripts; static checks and production builds are part of handoff readiness.

---

# Engineering Conventions

The project shows several useful engineering patterns.

## Separate public and admin concerns

Admin routes live in a dedicated dashboard area.

## Keep APIs resource-oriented

Backend routes are organized by domain.

## Keep models structured

Centers, activities, and news use explicit schemas.

## Use reusable middleware

Auth, roles, validation, upload, logging, and errors are centralized.

## Validate both client and server

Client schemas improve UX; server rules protect data.

## Use environment-based configuration

Secrets/configuration are not intended to be hardcoded into public clients.

## Separate reference data from dynamic data

Mobile JSON datasets and backend API records should be understood as different data sources.

## Keep location first-class

Maps, center location fields, and mobile direction modules all treat geography as part of the product.

---

# Development and Release

## Web

Typical flow:

```bash
npm install
npm run dev
npm run lint
npm run build
```

## Backend

Typical flow:

```bash
npm install
npm run dev
npm run lint
npm run test
npm run start
```

## Mobile

Typical Flutter flow:

```bash
flutter pub get
flutter analyze
flutter test
flutter run
```

---

# Environment and Configuration

Important backend configuration can include:

- MongoDB connection information,
- JWT secrets,
- Cloudinary configuration,
- frontend origin,
- environment mode,
- port.

The backend loads environment configuration with `dotenv`.

Production secrets should never be committed into repository documentation.

---

# Operational Considerations

This platform contains both static/reference and dynamic information.

That creates several operational concerns.

## Keep reference datasets reviewed

Bundled JSON may become stale if facility information changes.

## Keep dynamic APIs available

Centers, activities, and news depend on backend/database availability.

## Monitor health

The backend health endpoint exposes process and database state.

## Preserve image availability

Cloudinary/upload changes can affect multiple public surfaces.

## Keep auth working independently of UI

Admin security must not depend only on frontend redirects.

## Validate dates

Activity date rules are important because scheduled activities should not accidentally be created with invalid past dates under current model policy.

---

# Privacy and Sensitive Data

The center membership schema can contain information such as:

- ID-document images,
- birth certificate images,
- personal photos,
- utility-bill images,
- phone numbers.

This is not ordinary public content.

Any production workflow involving these fields should apply strong access control and privacy handling.

Public READMEs should never expose actual member documents or production credentials.

---

# Project Status

The organization represents a delivered Ministry of Youth & Sports digital platform implementation.

The current system includes:

- public web presentation,
- protected web administration,
- dynamic centers,
- activities,
- news,
- facility-related APIs,
- map/location capability,
- secure Express/Mongo backend,
- Flutter mobile public experience,
- bundled facility reference data.

Individual components may continue to receive:

- content updates,
- framework compatibility updates,
- security maintenance,
- validation improvements,
- facility-data updates,
- UI/UX refinements,
- mobile maintenance,
- backend maintenance.

---

# Repository Guide for Reviewers

If you are reviewing the platform technically, use this order.

## 1. Start with the web client

Repository:

`Ministry-Of-Youth-Sports/client`

Review:

```text
src/app/
src/app/dashboard-admin/
src/app/login/
```

Then inspect:

- center UI,
- activities UI,
- news UI,
- form schemas,
- API utilities,
- map components,
- dashboard layout.

This quickly shows the public/admin split.

## 2. Review the backend

Repository:

`Ministry-Of-Youth-Sports/backend`

Start with:

```text
src/app.js
```

This reveals:

- security middleware,
- CORS,
- rate limiting,
- logging,
- route mounting,
- health check,
- error handling.

Then inspect:

```text
src/routes/
src/controllers/
src/models/
src/middleware/
```

Pay particular attention to:

- Center model,
- Activity model,
- News model,
- auth middleware,
- roles middleware,
- validation,
- uploads.

## 3. Review the mobile app

Repository:

`Ministry-Of-Youth-Sports/mobile_app`

Start with:

```text
lib/main.dart
lib/layout/
lib/modules/
lib/shared/
```

Then review:

- youth centers,
- directions,
- activities,
- news,
- sports clubs,
- federations,
- pools,
- technology clubs,
- bundled JSON datasets.

## 4. Compare data boundaries

Ask:

- Which records are dynamic?
- Which are bundled locally?
- Which mutations are protected?
- Which fields are public?
- Which fields are sensitive?
- Which clients consume the same backend state?

That gives a better understanding than judging any one repository in isolation.

---

# In Short

The Ministry of Youth & Sports organization represents a connected public-information and administration system.

```text
PUBLIC WEB
Next.js / React
      │
      │
      ▼
BACKEND API
Node.js / Express
      │
      ├─ auth
      ├─ centers
      ├─ activities
      ├─ news
      ├─ tech clubs
      ├─ playgrounds
      ├─ swimming pools
      ├─ validation
      └─ media/security
      │
      ▼
MONGODB / MONGOOSE
      ▲
      │
      │
MOBILE APP
Flutter / Dart
      │
      ├─ youth centers
      ├─ clubs
      ├─ federations
      ├─ pools
      ├─ stadiums
      ├─ technology clubs
      ├─ activities
      ├─ news
      └─ directions
```

The system's main engineering value is the separation of concerns:

- **the backend owns security and shared dynamic data,**
- **the web client serves both citizens and administrators through separate routes,**
- **the mobile app gives public users a focused discovery experience,**
- **structured models keep centers, activities, and news more reliable than unvalidated content blobs.**

That is the architecture this organization profile documents.
