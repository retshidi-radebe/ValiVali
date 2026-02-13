# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Z.ai Code Scaffold — a full-stack Next.js 16 web application scaffold using Bun as the runtime and package manager. TypeScript 5, Tailwind CSS 4, shadcn/ui (new-york style), Prisma with SQLite.

## Commands

```bash
bun install              # Install dependencies
bun run dev              # Dev server on port 3000
bun run build            # Production build (standalone output)
bun start                # Production server via Bun
bun run lint             # ESLint

bun run db:push          # Push Prisma schema to DB
bun run db:generate      # Generate Prisma client
bun run db:migrate       # Run Prisma migrations
bun run db:reset         # Reset database
```

No test framework is configured.

## Architecture

- **Next.js App Router** with standalone output mode (`next.config.ts`). TypeScript build errors are ignored; React strict mode is off.
- **Path alias**: `@/*` maps to `src/*`.
- **UI components**: 48 shadcn/ui components in `src/components/ui/` built on Radix UI. Add new ones via `bunx shadcn@latest add <component>`. Configuration in `components.json` (style: new-york, RSC enabled, icon library: lucide).
- **Styling**: Tailwind CSS 4 with CSS variables in oklch color space (`src/app/globals.css`). Dark mode via class strategy. Colors, spacing, and border-radius are theme tokens.
- **Database**: Prisma ORM with SQLite (`prisma/schema.prisma`). DB file at `db/custom.db`. Prisma client singleton in `src/lib/db.ts`. `DATABASE_URL` env var required.
- **State management**: Zustand for client state, TanStack Query for server state.
- **Forms**: React Hook Form + Zod validation + `@hookform/resolvers`.
- **Auth**: NextAuth.js (v4) available but not wired up by default.
- **Internationalization**: next-intl available.
- **Mini-services**: `mini-services/` directory for optional microservices. WebSocket example in `examples/websocket/` (Socket.io on port 3003). Build/start scripts in `.zscripts/`.
- **Reverse proxy**: Caddyfile routes on port 81 with dynamic port forwarding via `XTransformPort` header.
- **Utilities**: `cn()` helper in `src/lib/utils.ts` (clsx + tailwind-merge) for className merging.

## Key Conventions

- React 19 with both server and client components. Use `"use client"` directive when needed.
- shadcn/ui components are copied into the codebase (not imported from a package) — edit them directly when customization is needed.
- ESLint is configured with most rules intentionally disabled for flexibility (see `eslint.config.mjs`).
- Animations use Framer Motion.
- Icons from `lucide-react`.
