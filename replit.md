# Portfolio Website

## Overview

This is a modern, dark-themed portfolio website built as a full-stack application. The project showcases a developer's work, skills, and contact information through an elegant, animated user interface. It features a public-facing portfolio site with sections for hero, about, work/projects, and contact, plus an admin dashboard for managing profile content.

The application uses a React frontend with TypeScript and Vite, an Express backend, and PostgreSQL database with Drizzle ORM for data persistence.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- **Framework:** React 18 with TypeScript
- **Build Tool:** Vite for fast development and optimized production builds
- **Routing:** Wouter for lightweight client-side routing
- **State Management:** TanStack Query (React Query) for server state management
- **UI Components:** Shadcn UI component library built on Radix UI primitives
- **Styling:** Tailwind CSS with custom dark theme configuration

**Design System:**
- Dark-first aesthetic with ambient, glassmorphism effects
- Custom color palette with primary purple accent (#a855f7)
- Typography using Inter/DM Sans for UI, JetBrains Mono for code/accent text
- Responsive grid system (12-column) with mobile-first breakpoints
- Component-based architecture with reusable UI primitives

**Key Pages:**
- **Home (/):** Main portfolio showcase with Hero, About, Portfolio, and Contact sections
- **Admin (/admin):** Protected dashboard for updating profile information
- **404:** Custom not-found page

**Component Structure:**
- Presentational components for each major section (Hero, About, Portfolio, Contact, Navigation)
- Animated background with gradient effects
- Glassmorphism cards with hover states and glow effects
- Form handling with React Hook Form and Zod validation

### Backend Architecture

**Technology Stack:**
- **Runtime:** Node.js with TypeScript
- **Framework:** Express.js for HTTP server
- **Database:** PostgreSQL via Neon serverless
- **ORM:** Drizzle ORM for type-safe database queries
- **File Upload:** Multer for handling profile image uploads
- **Session Management:** Express sessions with PostgreSQL store

**API Design:**
- RESTful API endpoints under `/api` prefix
- Authentication via API key for admin operations (header: `x-api-key`)
- File serving for uploaded profile images from `/uploads` directory
- JSON request/response format

**Key Endpoints:**
- `GET /api/profile` - Fetch profile data (public)
- `PUT /api/profile` - Update profile (requires API key)
- `POST /api/profile/upload` - Upload profile image (requires API key)
- `GET /uploads/:filename` - Serve uploaded images

**Database Schema:**
- Single `profiles` table storing user profile information
- Fields: id, name, title, bio, profileImage, email, phone, location, github, linkedin, twitter
- UUID primary key with PostgreSQL's `gen_random_uuid()`
- Schema validation using Zod with Drizzle integration

**Development vs Production:**
- Development: Vite middleware for HMR and dev server
- Production: Static file serving from `dist/public`
- Conditional loading of Replit dev tools (cartographer, dev banner) only in development

### External Dependencies

**Database:**
- **Neon Serverless PostgreSQL:** Cloud-hosted Postgres database
- Connection via `@neondatabase/serverless` with WebSocket support
- Environment variable: `DATABASE_URL`

**UI Component Library:**
- **Shadcn UI:** Pre-built, customizable React components
- **Radix UI:** Headless UI primitives (accordion, dialog, dropdown, etc.)
- Configuration in `components.json` with New York style variant

**Authentication:**
- Simple API key-based authentication for admin operations
- Environment variable: `ADMIN_API_KEY`
- No user session management; stateless API authentication

**File Storage:**
- Local filesystem storage for uploaded images in `uploads/` directory
- File validation: images only (JPEG, PNG, GIF, WebP)
- 5MB file size limit
- Auto-generated unique filenames using timestamps

**Google Fonts:**
- Architects Daughter, DM Sans, Fira Code, Geist Mono
- Loaded via Google Fonts CDN in HTML head

**Development Tools (Replit-specific):**
- `@replit/vite-plugin-runtime-error-modal` - Error overlay
- `@replit/vite-plugin-cartographer` - Code navigation
- `@replit/vite-plugin-dev-banner` - Development banner

**Build & Deployment:**
- TypeScript compilation with strict mode enabled
- ESBuild for server bundling (ESM format)
- Vite for client bundling with code splitting
- Single production build outputs server to `dist/` and client to `dist/public/`