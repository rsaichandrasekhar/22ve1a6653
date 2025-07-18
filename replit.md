# URL Shortener Application

## Overview

This is a full-stack URL shortener application built with React, Express, and in-memory storage. The application allows users to create up to 5 shortened URLs concurrently with custom short codes, set expiration times, and track analytics. It features a Material UI inspired design built with shadcn/ui components and includes extensive logging middleware for backend operations.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **UI Library**: shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **State Management**: TanStack Query (React Query) for server state
- **Build Tool**: Vite with custom configuration for development and production

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Storage**: In-memory storage with IStorage interface for flexibility
- **API Structure**: RESTful endpoints under `/api` prefix
- **Logging**: Extensive logging middleware integrated with external evaluation service
- **Session Management**: Express sessions with memory store
- **Error Handling**: Comprehensive error handling with detailed logging

### Project Structure
- `client/` - React frontend application
- `server/` - Express backend with API routes
- `shared/` - Shared TypeScript schemas and types
- `migrations/` - Database migration files

## Key Components

### Database Schema (shared/schema.ts)
- **Users Table**: User authentication and management
- **URLs Table**: Shortened URL records with metadata including:
  - Original URL and short code
  - Custom short codes (optional)
  - Expiration tracking (validity in minutes)
  - Click counting and analytics
  - Active/inactive status

### API Endpoints (server/routes.ts)
- `POST /api/urls` - Create new shortened URL
- `GET /api/urls` - Retrieve all URLs
- `GET /api/urls/stats` - Get URL statistics
- `DELETE /api/urls/:id` - Delete URL (referenced but not implemented)

### Frontend Pages
- **URL Shortener** (`/`) - Main interface for creating up to 5 concurrent shortened URLs
- **Statistics** (`/statistics`) - Analytics dashboard with filtering, export, and URL management
- **Redirect** (`/s/:shortCode`) - Handles URL redirection with click tracking

### Storage System
- **Interface-based Design**: IStorage interface for flexible storage implementations
- **Memory Storage**: In-memory implementation with full CRUD operations
- **Logging Integration**: All storage operations include comprehensive logging

## Data Flow

1. **URL Creation**:
   - User submits URL with optional custom short code and validity period
   - Frontend validates input using Zod schemas
   - Backend creates database record and generates short code if needed
   - Response includes shortened URL details

2. **URL Access**:
   - User visits shortened URL (`/s/:shortCode`)
   - Frontend redirects to backend for processing
   - Backend tracks click, updates statistics, and redirects to original URL

3. **Analytics**:
   - Statistics page fetches URL data and aggregated metrics
   - Real-time updates using React Query's caching and refetching

## External Dependencies

### UI and Styling
- **Radix UI**: Comprehensive component primitives for accessibility
- **Tailwind CSS**: Utility-first CSS framework
- **Lucide React**: Icon library
- **Class Variance Authority**: Component variant management

### State Management and Data Fetching
- **TanStack Query**: Server state management and caching
- **React Hook Form**: Form handling and validation
- **Zod**: Runtime type validation and schema definition

### Logging and Backend
- **External Logging**: Integration with evaluation service API for comprehensive logging
- **Memory Storage**: In-memory data persistence with interface-based design
- **Express Sessions**: Session management with memory store

### Development Tools
- **TypeScript**: Static type checking
- **Vite**: Fast build tool and development server
- **ESBuild**: JavaScript bundler for production builds

## Deployment Strategy

### Development
- **Dev Server**: Vite development server with HMR
- **Backend**: tsx for TypeScript execution with hot reload
- **Database**: Drizzle Kit for schema management and migrations

### Production Build
- **Frontend**: Vite builds optimized React bundle to `dist/public`
- **Backend**: ESBuild bundles Express server to `dist/index.js`
- **Static Serving**: Express serves built frontend in production

### Key Features
- **Concurrent URL Creation**: Support for creating up to 5 URLs simultaneously
- **Custom Shortcodes**: Optional user-defined shortcodes with validation
- **Expiration Management**: Configurable validity periods (1-10080 minutes)
- **Analytics Dashboard**: Comprehensive statistics with filtering and export
- **Material UI Design**: Clean, professional interface with responsive design
- **Error Handling**: Robust client and server-side error management

### Key Architectural Decisions

1. **Monorepo Structure**: Shared types and schemas between frontend and backend
2. **Type Safety**: End-to-end TypeScript with Zod validation
3. **Component Library**: shadcn/ui for consistent, accessible UI components
4. **Server State**: React Query for efficient API state management
5. **Storage**: In-memory storage with interface-based design for flexibility
6. **Logging**: Comprehensive logging middleware integrated with external evaluation service
7. **Material Design**: Material UI inspired styling with Tailwind CSS