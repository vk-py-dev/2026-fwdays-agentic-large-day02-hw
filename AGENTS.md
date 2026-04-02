# AGENTS.md

## Project Overview

Excalidraw is a collaborative whiteboard application built with React and Canvas. This is a **monorepo** containing the core drawing library (`packages/excalidraw/`), the web application (`excalidraw-app/`), and supporting packages for shared utilities, element management, and math operations.

**Key Goals**:
- Provide a free, open-source drawing/sketching tool
- Enable real-time collaboration on drawings
- Maintain high performance with Canvas rendering
- Support importing/exporting drawings and libraries
- Ensure security in file handling and data transmission

**Who Uses This**: Web developers integrating Excalidraw into apps, end-users at excalidraw.com, library authors using `@excalidraw/excalidraw` npm package.

## Tech Stack

**Frontend**:
- React 18+ (component framework)
- TypeScript (strict mode)
- Canvas API (rendering)
- Vite (build tool for app)
- esbuild (package bundling)

**Backend/Real-time**:
- Firebase/WebSocket (real-time collaboration)
- Node.js (tooling)

**Testing & Quality**:
- Vitest (unit tests)
- TypeScript (type checking)
- ESLint + Prettier (linting/formatting)

**State Management**:
- Custom `actionManager` (not Redux/Zustand)
- Immutable patterns for drawing state

## Conventions

**Code Style**:
- Named exports only (no default exports)
- Strict TypeScript types (no `any`)
- Immutable state updates via `actionManager`
- PascalCase for components, camelCase for functions

**Architecture**:
- `packages/excalidraw/` contains the core library
- `excalidraw-app/` contains the web application
- Internal packages for shared logic: `@excalidraw/common`, `@excalidraw/element`, `@excalidraw/math`, `@excalidraw/utils`
- Use path aliases from `vitest.config.mts`

**File Organization**:
- React components in dedicated directories
- Utilities in `utils/` subdirectories
- Tests colocated with source files (`.test.ts` / `.test.tsx`)
- Types in separate `types.ts` files or inline

**SVG & Import Security**:
- Always sanitize imported SVG and `.excalidraw` files
- Validate element schema for imported drawings
- Use `DOMPurify` for untrusted content

## Do-Not-Touch / Constraints

**Protected Core Files** — These require full test suite verification before modification:
- `packages/excalidraw/scene/Renderer.ts` — render pipeline
- `packages/excalidraw/actions/manager.tsx` — action system
- `packages/excalidraw/data/restore.ts` — file format compatibility
- `packages/excalidraw/types.ts` — core types

**Forbidden Patterns**:
- Do NOT use `useState` for app state (use `actionManager`)
- Do NOT use external canvas libs (fabric.js, react-konva, pixi.js)
- Do NOT add unvetted npm packages without security audit
- Do NOT modify protected files without running complete test suite
- Do NOT commit `.env` files or secrets; use `.env.example` as template

**Security Constraints**:
- Validate and sanitize all user input
- Never render untrusted HTML directly
- Enforce Content Security Policy headers
- Use E2E encryption for real-time collaboration data
- Verify file imports against schema before processing

## Project Structure

Excalidraw is a **monorepo** with a clear separation between the core library and the application:

- **`packages/excalidraw/`** - Main React component library published to npm as `@excalidraw/excalidraw`
- **`excalidraw-app/`** - Full-featured web application (excalidraw.com) that uses the library
- **`packages/`** - Core packages: `@excalidraw/common`, `@excalidraw/element`, `@excalidraw/math`, `@excalidraw/utils`
- **`examples/`** - Integration examples (NextJS, browser script)

## Development Workflow

1. **Package Development**: Work in `packages/*` for editor features
2. **App Development**: Work in `excalidraw-app/` for app-specific features
3. **Testing**: Always run `yarn test:update` before committing
4. **Type Safety**: Use `yarn test:typecheck` to verify TypeScript

## Memory bank (`docs/memory/`)

The **memory bank** is the canonical place for long-lived project context (goals, stack, architecture patterns, product UX, active focus, progress, and decisions). Agents and contributors should treat it as living documentation, not a one-time dump.

**Location**: [`docs/memory/`](docs/memory/) — see [`docs/memory/README.md`](docs/memory/README.md) for the file index and navigation hints.

**After project changes**, update the memory bank so it stays accurate. Match edits to the change:

| Change type | Prefer updating |
|-------------|-----------------|
| Goals, scope, or high-level overview | `projectbrief.md` |
| Dependencies, tooling, or environment | `techContext.md` |
| Architecture, modules, or coding patterns | `systemPatterns.md` |
| UX goals, flows, or product stance | `productContext.md` |
| Current sprint/focus, priorities, or “what’s hot” | `activeContext.md` |
| Milestones, debt, or lessons learned | `progress.md` |
| Meaningful technical or product decisions | `decisionLog.md` |
| Index or cross-links | `README.md` |

**Minimum bar**: After any non-trivial change (feature, refactor, dependency shift, decision), touch at least the files that are now wrong or incomplete — typically `activeContext.md` and any specialized file the change affects. When several files change, refresh `README.md` “Last updated” (and version if you maintain one) if the memory bank content materially changed.

## Development Commands

```bash
yarn build           # Build all packages and the application
yarn start           # Start development server for excalidraw-app/
yarn test:typecheck  # TypeScript type checking
yarn test:update     # Run all tests (with snapshot updates)
yarn fix             # Auto-fix formatting and linting issues
```

## Available Skills

Skills provide specialized capabilities and domain knowledge. Use them to complete tasks more effectively.

### build-verify

**Purpose**: Runs `yarn build` after code changes, automatically fixes compilation errors, and reports build status.

**When to use**: After edits that might affect compilation, or when the user asks to build, verify, or check compilation.

**Workflow**:
1. Run `yarn build` at the project root
2. If build fails, automatically fix the issue (max 3 attempts)
3. Report build status and changed files

**Key constraints**: Do NOT use `@ts-ignore`, `any` types, or modify test files to suppress errors—fix the root cause.

### codebase-explore

**Purpose**: Systematically explores unfamiliar codebases to understand architecture, data flow, and key components.

**When to use**: When you need to understand an unfamiliar area of the codebase, or when investigating "how does X work?"

**Process**:
1. Identify relevant directory/files
2. Read README or top-level comments
3. Map key files and responsibilities
4. Trace data flow: entry point → processing → output
5. Identify dependencies and document findings

**Key constraint**: READ-ONLY—do not modify files during exploration.

### repomix-reference-2026-fwdays-agentic-large-day02-hw

**Purpose**: Reference codebase containing structure, implementation patterns, and code details for this project.

**When to use**: When you need to understand project structure, find where specific functionality is implemented, or search for code patterns.

**Key files**:
- `references/summary.md` — Start here for project statistics and file format explanation
- `references/project-structure.md` — Directory tree with line counts per file
- `references/files.md` — All file contents (searchable by file path or keywords)
- `references/tech-stack.md` — Languages, frameworks, and dependencies

**Usage tips**:
- Use line counts to estimate file complexity
- Search for `## File:` pattern to jump between files
- Check `tech-stack.md` for dependencies and language details

## Architecture Notes

### Package System

- Uses Yarn workspaces for monorepo management
- Internal packages use path aliases (see `vitest.config.mts`)
- Build system uses esbuild for packages, Vite for the app
- TypeScript throughout with strict configuration
