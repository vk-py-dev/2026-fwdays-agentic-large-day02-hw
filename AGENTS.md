# AGENTS.md

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
