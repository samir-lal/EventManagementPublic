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

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/eventpro.git
   cd eventpro
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up PostgreSQL database**

   **Option A: Local PostgreSQL Installation**
   
   Install PostgreSQL on your system:
   - **macOS**: `brew install postgresql@15 && brew services start postgresql@15`
   - **Ubuntu/Debian**: `sudo apt-get install postgresql postgresql-contrib`
   - **Windows**: [Download installer](https://www.postgresql.org/download/windows/)
   
   Create a database:
   ```bash
   # Connect to PostgreSQL
   psql postgres
   
   # Create database and user
   CREATE DATABASE eventpro;
   CREATE USER eventpro_user WITH PASSWORD 'your_password';
   GRANT ALL PRIVILEGES ON DATABASE eventpro TO eventpro_user;
   \q
   ```

   **Option B: Free Cloud Database**
   
   Use a free hosted PostgreSQL database:
   - [Neon](https://neon.tech) - Free tier available
   - [Supabase](https://supabase.com) - Free tier available
   - [Railway](https://railway.app) - Free tier available

4. **Set up environment variables**
   
   Copy the example file and update with your values:
   ```bash
   cp .env.example .env
   ```
   
   Edit `.env` file with your database credentials:
   
   ```env
   # For local PostgreSQL:
   DATABASE_URL=postgresql://eventpro_user:your_password@localhost:5432/eventpro
   PGHOST=localhost
   PGPORT=5432
   PGUSER=eventpro_user
   PGPASSWORD=your_password
   PGDATABASE=eventpro
   
   # Generate a random session secret:
   SESSION_SECRET=your-random-secret-here
   ```
   
   **Generate a secure session secret:**
   ```bash
   # On Linux/macOS:
   openssl rand -base64 32
   
   # On Windows (PowerShell):
   [Convert]::ToBase64String((1..32 | ForEach-Object { Get-Random -Maximum 256 }))
   ```
   
   **Optional: Google OAuth** (skip if you don't need "Sign in with Google")
   
   1. Go to [Google Cloud Console](https://console.cloud.google.com/apis/credentials)
   2. Create OAuth 2.0 credentials
   3. Add authorized redirect URI: `http://localhost:5000/auth/google/callback`
   4. Add credentials to `.env`:
      ```env
      GOOGLE_CLIENT_ID=your-client-id
      GOOGLE_CLIENT_SECRET=your-client-secret
      ```

5. **Initialize the database**
   
   This will create all necessary tables:
   ```bash
   npm run db:push
   ```

6. **Start the development server**
   ```bash
   npm run dev
   ```

The application will be available at `http://localhost:5000`

### First-Time Setup

After starting the application:
1. Go to `http://localhost:5000`
2. Click "Sign Up" and create a provider account
3. Complete your business profile
4. You're ready to start managing events!

### Troubleshooting

**Database connection errors:**
- Verify PostgreSQL is running: `pg_isready`
- Check your `DATABASE_URL` in `.env`
- Ensure the database exists: `psql -l`

**Port already in use:**
- Change the `PORT` in `.env` to a different value (e.g., 3000)

**Build errors:**
- Clear node_modules: `rm -rf node_modules && npm install`
- Clear Vite cache: `rm -rf .vite`

## Project Structure

```
├── client/                 # Frontend React application
│   ├── src/
│   │   ├── components/    # Reusable UI components
│   │   ├── pages/         # Page components
│   │   ├── lib/           # Utility functions and query client
│   │   └── hooks/         # Custom React hooks
├── server/                # Backend Express application
│   ├── routes.ts          # API route definitions
│   ├── storage.ts         # Database access layer
│   └── auth.ts            # Authentication configuration
├── shared/                # Shared code between frontend and backend
│   └── schema.ts          # Database schema and types
└── db/                    # Database migrations and config
```

## Database Schema

The platform includes the following core tables:
- **users**: User authentication and roles
- **providers**: Provider business information
- **clients**: Client profile information
- **services**: Service catalog
- **client_events**: Event bookings
- **client_quotes**: Quote management
- **quote_line_items**: Detailed quote breakdowns
- **discount_coupons**: Coupon management system

## Scripts

- `npm run dev` - Start development server (frontend + backend)
- `npm run build` - Build for production
- `npm run db:push` - Sync database schema
- `npm run db:studio` - Open Drizzle Studio for database management

## Authentication

EventPro supports multiple authentication methods:
- Email/password with secure password hashing (bcrypt)
- Google OAuth 2.0
- HTTP-only secure cookies with CSRF protection
- Password strength validation
- Forgot password functionality

## Security Features

- Role-based access control (RBAC)
- Secure session management with PostgreSQL store
- Password strength validation
- HTTP-only cookies with CSRF protection
- Environment-based secret management
- SQL injection prevention through Drizzle ORM

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.

## Support

For support, please open an issue in the GitHub repository.
