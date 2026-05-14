# Project: MyApp

## What This Is
A full-stack web application for task management with real-time collaboration.
Built for small teams who need a lightweight alternative to Jira or Asana.

---

## Stack
- **Language**: TypeScript (strict mode)
- **Frontend**: React 18, Vite, TailwindCSS
- **Backend**: Node.js, Express, Prisma ORM
- **Database**: PostgreSQL (local), Supabase (production)
- **Testing**: Vitest (unit), Playwright (e2e)
- **Package manager**: `pnpm` — never use `npm` or `yarn`

---

## Folder Structure
```
src/
  components/     # Reusable UI components
  pages/          # Route-level page components
  hooks/          # Custom React hooks
  lib/            # Shared utilities and helpers
  api/            # API route handlers (Express)
  db/             # Prisma schema and migrations
tests/
  unit/           # Vitest unit tests
  e2e/            # Playwright end-to-end tests
```

---

## Common Commands
```bash
pnpm dev          # Start dev server (frontend + backend)
pnpm test         # Run unit tests
pnpm test:e2e     # Run Playwright e2e tests
pnpm lint         # Run ESLint
pnpm lint --fix   # Auto-fix lint errors
pnpm db:migrate   # Run pending Prisma migrations
pnpm db:studio    # Open Prisma Studio (DB GUI)
pnpm build        # Production build
```

---

## Code Conventions

### General
- Use `const` by default; only use `let` when reassignment is needed
- Prefer named exports over default exports
- All async functions should handle errors with try/catch — no unhandled promises
- Use `zod` for all input validation (API and forms)

### TypeScript
- Strict mode is on — no `any` types unless absolutely unavoidable
- Define interfaces in `src/lib/types.ts` for shared types
- Prefer `interface` over `type` for object shapes

### React
- Functional components only — no class components
- Custom hooks for any logic that spans >1 component
- Co-locate component styles with the component file
- Use `React.memo` only when profiling shows a real need

### API
- All routes return `{ data, error }` shaped responses
- Use HTTP status codes correctly (200, 201, 400, 404, 500)
- Auth middleware is in `src/api/middleware/auth.ts` — always apply it to protected routes

### Git
- Commit format: `type(scope): message` (e.g. `feat(tasks): add due date field`)
- Types: `feat`, `fix`, `chore`, `docs`, `refactor`, `test`
- Never commit directly to `main` — always use a branch + PR

---

## Environment
- Node.js `>=20.0.0`
- `.env.local` is used for local secrets — never commit this
- `.env.example` should always be kept up to date when adding new env vars
- Key env vars:
  - `DATABASE_URL` — Postgres connection string
  - `JWT_SECRET` — Auth token signing key
  - `SUPABASE_KEY` — Production DB key

---

## Current State (update this each session)
- ✅ Auth (login/signup/JWT) — complete
- ✅ Task CRUD — complete
- 🔄 Real-time updates via WebSockets — in progress (`src/lib/socket.ts`)
- ❌ Email notifications — not started yet
- ⚠️  Known issue: Prisma migration `20240312_add_tags` is pending on production — do not run locally until confirmed safe

---

## Rules — Always Follow These

### Do
- Always run `pnpm lint` before considering a task complete
- Write a unit test for any new utility function in `src/lib/`
- Keep components under 200 lines — split if larger
- Use existing components from `src/components/` before creating new ones

### Never
- Never modify files in `legacy/` — this code is frozen and will be removed later
- Never use `console.log` in production code — use the `logger` utility in `src/lib/logger.ts`
- Never store secrets or tokens in code or comments
- Never run `pnpm db:migrate` without checking with the user first

---

## Key Decisions & Context
- We chose Prisma over Drizzle because the team is more familiar with it
- TailwindCSS utility classes are preferred over CSS modules
- We intentionally avoid Redux — React Query + local state is sufficient
- The `legacy/` folder contains the old Vue 2 codebase — ignore it

---

## Contacts & Resources
- Design system: `src/components/README.md`
- API docs: `docs/api.md`
- Deployment: Vercel (frontend), Railway (backend)
- CI/CD: GitHub Actions (`.github/workflows/`)
