# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a T3 Stack application for trip planning, built with:
- **Next.js 15** (App Router with React Server Components)
- **tRPC** for end-to-end typesafe APIs
- **Drizzle ORM** with MySQL
- **TailwindCSS** for styling
- **TypeScript** for type safety
- **pnpm** as the package manager

The app has been stripped down to a minimal "Hello World" state, ready for new features to be built.

## Development Commands

```bash
# Development
pnpm dev                # Start dev server with Turbo
pnpm build              # Build for production
pnpm start              # Start production server
pnpm preview            # Build and start production server
pnpm typecheck          # Run TypeScript compiler check

# Database
pnpm db:push            # Push schema changes to database
pnpm db:generate        # Generate migrations from schema
pnpm db:migrate         # Run migrations
pnpm db:studio          # Open Drizzle Studio (database GUI)
```

## Architecture

### Database Setup

1. Copy `.env.example` to `.env` and configure `DATABASE_URL`
2. The database uses MySQL with table prefix `tripplanner_`
3. Schema is defined in `src/server/db/schema.ts`
4. Database instance is exported from `src/server/db/index.ts`

### tRPC Architecture

**Server-side (API):**
- `src/server/api/trpc.ts` - Core tRPC setup, context, and base procedures
  - `publicProcedure` - Base procedure for all endpoints (includes timing middleware)
  - `createTRPCContext` - Creates request context with database and headers
- `src/server/api/root.ts` - Main router that combines all sub-routers
- `src/server/api/routers/` - Directory for API route handlers (currently empty)

**Client-side:**
- `src/trpc/react.tsx` - Client-side tRPC hooks (`api.routerName.procedureName.useQuery()`)
- `src/trpc/server.ts` - Server-side tRPC caller for use in Server Components
- `src/app/layout.tsx` - Wraps app with `TRPCReactProvider`

**Adding new API endpoints:**
1. Create router file in `src/server/api/routers/`
2. Import and add router to `appRouter` in `src/server/api/root.ts`
3. Use `publicProcedure` from `src/server/api/trpc.ts` to define procedures
4. Access database via `ctx.db` in procedures

### Environment Variables

Environment variables are validated using `@t3-oss/env-nextjs` in `src/env.js`:
- Server variables must be added to both `server` schema and `runtimeEnv`
- Client variables must be prefixed with `NEXT_PUBLIC_` and added to `client` schema
- Build will fail if required environment variables are missing or invalid

### Database Schema

Define tables in `src/server/db/schema.ts` using the `createTable` helper, which automatically prefixes tables with `tripplanner_`. Use `pnpm db:push` to sync schema changes to the database during development.

### Styling

The project uses TailwindCSS v4 with extensive Radix UI components installed for building accessible UI components. Global styles are in `src/styles/globals.css`.
