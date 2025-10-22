The repository is a Next.js 15 app using the App Router and TypeScript. Keep instructions short, concrete, and tied to files in this project so an automated coding agent can be productive immediately.

Key facts (big picture)
- Framework: Next.js 15 (App Router). Pages and layouts live under `app/`.
- Language: TypeScript + React 19 with both Server and Client components. Client components include a top-of-file "use client" directive (e.g. `app/components/hello.tsx`).
- Styling: Tailwind via `postcss.config.mjs` + `app/globals.css`.
- Fonts: `next/font` used in `app/layout.tsx` (Geist family).

Important files to inspect
- `package.json` — dev scripts: `npm run dev` (Next dev with turbopack), `npm run build`, `npm run start`, `npm run lint`.
- `app/layout.tsx` — global HTML root layout and font setup.
- `app/global-error.tsx` and `app/(root)/error.tsx` — global and route-level error boundaries (note `"use client"` requirement).
- `app/loading.tsx` — global loading UI for suspense/segments.
- `app/(dashboard)/dashboard/*` and `app/(root)/*` — example nested layouts and route groups. See `users/[id]/page.tsx` for dynamic route params pattern.

Project-specific conventions
- Use the App Router. Prefer server components by default; mark components as client with `"use client"` at top of the file when they need state, effects, or browser-only APIs. Examples: `app/components/hello.tsx` (client) vs `app/(root)/page.tsx` (server).
- Error boundaries: route-level `error.tsx` files in segments are client components and must include `reset()` usage to re-render segments. Global error (`app/global-error.tsx`) must render full `<html><body>`.
- Layouts: Use `layout.tsx` files to wrap routes; nested layouts are used for top-level navigation (`app/(root)/layout.tsx`) and dashboard area (`app/(dashboard)/dashboard/layout.tsx`).
- Dynamic routes: follow `[param]` filename convention; access via `params` prop in the page component (`({ params }: { params: { id: string } })`). See `app/(dashboard)/dashboard/users/[id]/page.tsx`.

Build / dev / lint commands
- Start dev server (with turbopack): `npm run dev` (listens on http://localhost:3000).
- Build: `npm run build`.
- Start production server after build: `npm run start`.
- Lint: `npm run lint` (ESLint configured via `eslint.config.mjs`).

Patterns & examples to follow when editing or adding code
- Place shared UI under `app/components/` and mark client/server appropriately. Example: `app/components/hello.tsx` is a small client component.
- Add route segments under `app/` and use `layout.tsx`, `page.tsx`, `loading.tsx`, and `error.tsx` as needed for each segment.
- Use Tailwind classes in JSX; global CSS variables are defined in `app/globals.css`.
- When adding dynamic routes, ensure TypeScript types for `params` are declared as in existing files.

Testing & debugging notes
- There are no tests defined in `package.json`. For quick runtime checks, run `npm run dev` and use the browser console or server logs. Server components will log on the server (see `console.log` in `app/(root)/page.tsx`).
- Use `console.error` in error boundaries to capture exceptions; `app/(root)/error.tsx` demonstrates logging in a `useEffect` hook.

Integration & external dependencies
- This project relies on Next.js core packages only (see `package.json`). No external APIs or services are configured.

When modifying code, follow these rules
- Preserve `"use client"` where present — removing it changes component execution environment.
- Keep layout and route filenames consistent with the App Router conventions (`layout.tsx`, `page.tsx`, `error.tsx`, `loading.tsx`).
- Prefer minimal, localized changes. If adding a new route segment, include `layout.tsx` only if you need DOM structure or shared UI for that segment.

If you need clarification from a human
- Ask which routes should be server vs client components if not obvious.
- Ask for design/visual guidance if adding UI beyond simple placeholders — this repo contains only minimal styling.

Examples to reference when making edits
- Client component example: `app/components/hello.tsx` (note `"use client"` and hooks).
- Server page example: `app/(root)/page.tsx` (no `"use client"`, runs on server by default).
- Dynamic route example: `app/(dashboard)/dashboard/users/[id]/page.tsx` (uses `params.id`).

If you update this file
- Merge any older `.github/copilot-instructions.md` content here rather than replacing without reason. Keep entries that reference repo-specific conventions or off-repo workflows.

End of instructions.
