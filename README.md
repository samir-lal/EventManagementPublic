# EventPro

A full-stack event management platform designed for DJ and event service providers. EventPro streamlines the entire event lifecycle from booking to service delivery with a professional dual-portal system.

## Overview

EventPro provides a comprehensive solution for event service providers to manage their business and for clients to book and manage events. The platform features a client-facing booking system with an intuitive multi-step form and a provider-facing admin dashboard for complete business management.

## Features

### For Clients
- **Easy Event Booking**: Multi-step form for seamless event creation
- **Real-time Quote Viewing**: Professional invoice-style quotes with detailed breakdowns
- **Event Management**: Edit and track event details throughout the lifecycle
- **Multiple Authentication Options**: Sign in with email/password or Google OAuth

### For Providers
- **Admin Dashboard**: Comprehensive business management interface
- **Quote Management**: "The Flow" - a seven-column, color-coded workflow tracking system for quotes from initial receipt to payment
- **Discount Coupon System**: Create and manage various coupon types with usage limits and expiration dates
- **Service Catalog**: Manage service offerings and pricing
- **Client Management**: Track and manage client relationships
- **Profile Management**: Editable business profiles with contact information and branding

### Core Capabilities
- Role-based access control (client, provider, admin)
- Professional quote generation with line items and discounts
- File upload support with drag-and-drop interface
- Real-time updates and notifications
- Responsive design for all devices
- Legal compliance with integrated Privacy Policy and Terms of Service

## Tech Stack

### Frontend
- **React** with TypeScript
- **Vite** for build tooling and development
- **Wouter** for client-side routing
- **TanStack Query** (React Query) for state management
- **Radix UI** primitives with **shadcn/ui** components
- **Tailwind CSS** for styling
- **React Hook Form** with **Zod** validation
- **Uppy.js** for file uploads

### Backend
- **Node.js** with **Express.js**
- **TypeScript** with ES modules
- **Passport.js** for authentication (OpenID Connect)
- PostgreSQL session store
- RESTful API design with structured error handling

### Database
- **PostgreSQL** (serverless)
- **Drizzle ORM** for type-safe database operations
- Automated migrations

### Storage
- **Google Cloud Storage** for file uploads
- Uppy.js integration for progress tracking

## Installation

### Prerequisites
- **Node.js 18+** - [Download here](https://nodejs.org/)
- **PostgreSQL** - See setup instructions below
- **Google Cloud Storage** (optional for basic testing)
- **Google OAuth credentials** (optional, only for "Sign in with Google")



## Project Structure

```
├── client/                 # Frontend React application
│   ├── src/
│   │   ├── components/    # Reusable UI components
│   │   ├── pages/         # Page components
│   │   ├── lib/           # Utility functions and query client
│   │   └── hook/         # Custom React hooks
├── server/                # Backend Express application
│   ├── routes.ts          # API route definitions
│   ├── storage.ts         # Database access layer
│   └── auth.ts            # Authentication configuration
├── shared/                # Shared code between frontend and backend
│   └── schema.ts          # Database schema and types
└── db/                    # Database migrations and config
```


## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.

## Support

For support, please open an issue in the GitHub repository.
