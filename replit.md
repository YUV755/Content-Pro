# Content Creator Pro

## Overview

Content Creator Pro is a full-stack web application designed to generate platform-specific content for various social media platforms using AI. The application leverages the Gemini API from Google to create tailored content for YouTube, Instagram, Facebook, and WhatsApp based on user prompts and preferences.

## User Preferences

```
Preferred communication style: Simple, everyday language.
```

## System Architecture

The application follows a modern web architecture with a clear separation between frontend and backend components:

1. **Frontend**: React-based SPA using shadcn/ui components with TailwindCSS for styling
2. **Backend**: Express.js API server providing content generation endpoints
3. **Database**: PostgreSQL with Drizzle ORM for type-safe database operations
4. **API Integration**: Google's Generative AI (Gemini) for AI-powered content generation
5. **Build/Dev Tools**: Vite for frontend bundling, TypeScript for type safety across the stack

The application uses a monorepo structure with a shared codebase between frontend and backend, while maintaining clear separation of concerns.

## Key Components

### Frontend

- **React**: Core UI library for building the interface
- **shadcn/ui**: Component library providing accessible, customizable UI elements
- **TailwindCSS**: Utility-first CSS framework for styling
- **React Query**: Data fetching, caching, and state management
- **React Hook Form**: Form handling with validation via Zod

### Backend

- **Express.js**: Web server framework for handling API requests
- **Drizzle ORM**: Type-safe database interactions with PostgreSQL
- **Google Generative AI (Gemini)**: AI model integration for content generation
- **Zod**: Schema validation for request data

### Database

- **PostgreSQL**: Relational database for storing user data and content generations
- **Database Schema**:
  - `users`: User account information
  - `content_generations`: Stored content generation results and metadata

## Data Flow

1. **User Input**: Users select a platform (YouTube, Instagram, Facebook, or WhatsApp) and provide a prompt along with additional parameters like tone, length, and keywords.

2. **Content Generation**:
   - Frontend sends a request to the `/api/generate` endpoint with platform and prompt details
   - Backend validates the request using Zod schemas
   - Backend enhances the prompt with additional context based on platform and parameters
   - Backend calls the Gemini API with safety settings to generate appropriate content
   - Generated content is returned to the client and optionally stored in the database

3. **Content Display**:
   - Frontend displays the generated content with platform-specific styling
   - Users can copy the content to the clipboard
   - Recent generations are displayed in a history list

## External Dependencies

### Frontend Libraries
- React
- TanStack Query (React Query)
- shadcn/ui (Built on Radix UI primitives)
- React Hook Form
- Zod for validation
- Lucide for icons
- wouter for routing

### Backend Services and Libraries
- Express.js
- Google Generative AI SDK
- Drizzle ORM
- PostgreSQL (via Neon Database serverless driver)

## Deployment Strategy

The application is configured for deployment on Replit with the following setup:

1. **Development**: 
   - `npm run dev` command using `tsx` to run the TypeScript server directly
   - Vite handles frontend bundling and hot module replacement

2. **Production Build**:
   - Frontend: Vite bundles the React application into static assets
   - Backend: ESBuild compiles the server code to JavaScript
   - The Express server serves the static frontend files from the dist directory

3. **Database**:
   - Uses the DATABASE_URL environment variable for PostgreSQL connection
   - Drizzle ORM handles schema migrations and database interactions

4. **Environment Variables**:
   - `GEMINI_API_KEY`: For Google Generative AI access
   - `DATABASE_URL`: For PostgreSQL connection
   - `NODE_ENV`: Environment indicator

## Getting Started

1. Ensure PostgreSQL is properly configured
2. Set up the required environment variables:
   ```
   DATABASE_URL=postgresql://...
   GEMINI_API_KEY=your_api_key_here
   ```
3. Run `npm run db:push` to update the database schema
4. Start the development server with `npm run dev`
5. For production, build with `npm run build` and start with `npm run start`

## Common Tasks

- **Add a new database table**: Update the schema in `shared/schema.ts` and run `npm run db:push`
- **Create a new API endpoint**: Add a route handler in `server/routes.ts`
- **Add a new page**: Create a component in `client/src/pages` and add it to the router in `App.tsx`
- **Modify styles**: Update theme variables in `client/src/index.css` or component-specific styles