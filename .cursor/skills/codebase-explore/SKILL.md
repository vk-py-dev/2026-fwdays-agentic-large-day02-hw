---
name: codebase-explore
description: Systematically explores unfamiliar codebases to understand architecture, data flow, and key components through guided analysis
---

# Skill: Codebase Explorer

## When to use

When you need to understand an unfamiliar area of the codebase.
Triggered by: "explore", "investigate", "how does X work?"

## Inputs

- Area of interest (module, feature, file pattern)
- For Excalidraw investigations, focus on:
  - `packages/excalidraw/` - Core editor library
  - `excalidraw-app/` - Web application
  - `packages/element/` - Element manipulation utilities
  - Entry points: `packages/excalidraw/index.tsx`, `excalidraw-app/index.tsx`
  - Key modules: actions, components, renderer, scene, data

## Steps

1. Identify relevant directory/files using @folder or @codebase
   - For Excalidraw: check `packages/excalidraw/`, `excalidraw-app/`, or workspace packages
   - Read top-level READMEs (e.g., `packages/excalidraw/README.md`, `dev-docs/README.md`)

2. Map the key files and their responsibilities
   - For app entry: start at `excalidraw-app/App.tsx` or `packages/excalidraw/index.tsx`
   - Trace component hierarchy and rendering pipeline

3. Trace data flow: entry point → processing → output
   - App entry → actionManager (state) → rendering (Canvas or React)
   - Example: user draws rectangle → action triggered → element created → renderer updates canvas

4. Identify dependencies (imports from other packages)
   - Check workspace imports (@excalidraw/*)
   - Note protected files (Renderer.ts, manager.tsx, restore.ts, types.ts)

5. Document findings in a summary
   - Architecture overview
   - Key file responsibilities
   - Data flow patterns
   - Dependencies and relationships

## Outputs

- Summary: purpose, key files, data flow, dependencies
- List of related files for deeper investigation
- Excalidraw-specific findings: state management patterns, rendering approach, protected file usage

## Safety

- READ-ONLY — do not modify any files during exploration
- Verify findings against actual code, not assumptions
- Note if investigation touches protected files (request full test suite review)