# Calourada de Biotecnologia - Event Ticket Sales System

## Overview

This is a full-stack web application for selling tickets to a biotechnology student event ("Calourada de Biotecnologia 2025"). The system handles user registration, authentication, ticket purchasing with different pricing tiers, and payment processing through MercadoPago integration.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

This application follows a modern full-stack architecture with clear separation between frontend and backend concerns:

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query (React Query) for server state management
- **UI Framework**: Shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with custom design system
- **Build Tool**: Vite for development and production builds

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **Database**: PostgreSQL with Drizzle ORM
- **Database Provider**: Neon Database (serverless PostgreSQL)
- **Authentication**: Session-based with bcrypt password hashing
- **Payment Processing**: MercadoPago SDK integration

## Key Components

### Database Schema
The application uses PostgreSQL with the following main entities:
- **Users**: Stores user account information (name, email, CPF, hashed password)
- **Tickets**: Defines ticket types with pricing tiers and availability limits
- **Orders**: Tracks purchase transactions and payment status

### Authentication System
- User registration with email/CPF validation
- Password hashing using bcrypt
- Session-based authentication (ready for session storage implementation)
- Login/logout functionality

### Payment Integration
- MercadoPago payment gateway integration
- Support for multiple payment methods (credit card, debit card, MercadoPago wallet)
- Webhook handling for payment status updates
- Preference creation for payment processing

### Admin Dashboard
- Real-time statistics and monitoring
- Order management and tracking
- Webhook event logging
- Auto-refreshing data views

## Data Flow

1. **User Registration**: Users create accounts with personal information
2. **Ticket Selection**: Users browse available ticket types and select quantities
3. **Payment Processing**: 
   - Order creation in database
   - MercadoPago preference generation
   - Payment brick rendering for user interaction
   - Webhook processing for payment confirmation
4. **Order Fulfillment**: Successful payments update order status and ticket availability

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: PostgreSQL database connectivity
- **drizzle-orm**: Type-safe database ORM
- **mercadopago**: Payment processing SDK
- **bcrypt**: Password hashing
- **express**: Web server framework
- **@tanstack/react-query**: Server state management
- **@radix-ui/***: Accessible UI components
- **tailwindcss**: Utility-first CSS framework

### Development Tools
- **vite**: Build tool and dev server
- **typescript**: Type checking and compilation
- **drizzle-kit**: Database migration tool

## Deployment Strategy

### Environment Variables Required
- `DATABASE_URL`: PostgreSQL connection string
- `MERCADOPAGO_ACCESS_TOKEN` or `MP_ACCESS_TOKEN`: Payment processing credentials
- `MERCADOPAGO_PUBLIC_KEY` or `MP_PUBLIC_KEY`: Frontend payment integration
- `MERCADOPAGO_WEBHOOK_SECRET` or `MP_WEBHOOK_SECRET`: Webhook validation (optional)

### Build Process
1. Frontend builds to `dist/public` directory using Vite
2. Backend compiles with esbuild for production
3. Single deployment artifact combines both frontend and backend

### Production Considerations
- The application is configured for serverless deployment
- Database migrations handled via Drizzle Kit
- Static assets served by Express in production
- WebSocket support configured for Neon Database

### Development Setup
- Hot reload enabled for both frontend and backend
- Replit-specific configurations for development environment
- Development banner integration for external access

## Architecture Decisions

### Database Choice
**Problem**: Need reliable, scalable database solution
**Solution**: PostgreSQL with Neon serverless hosting
**Rationale**: Type safety with Drizzle ORM, serverless scaling, and PostgreSQL's robustness for transactional data

### Payment Integration
**Problem**: Secure payment processing for Brazilian market
**Solution**: MercadoPago integration with webhook validation
**Rationale**: Popular in Brazil, comprehensive API, supports multiple payment methods

### State Management
**Problem**: Complex server state synchronization
**Solution**: TanStack Query for server state, React hooks for client state
**Rationale**: Automatic caching, background updates, error handling, and optimistic updates

### UI Framework
**Problem**: Consistent, accessible user interface
**Solution**: Shadcn/ui with Radix UI primitives and Tailwind CSS
**Rationale**: Accessibility built-in, consistent design system, developer productivity

### Monorepo Structure
**Problem**: Code sharing between frontend and backend
**Solution**: Shared schema and types in `/shared` directory
**Rationale**: Type safety across full stack, reduced duplication, easier maintenance