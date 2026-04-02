---
name: build-verify
description: Runs yarn build at the project root after code changes, automatically fixes compilation errors, and reports build status with details. Use when the user asks to build, verify, or check compilation, or after edits that might affect compilation.
---

# Build & Verify

## Workflow

After any code changes that might affect compilation:

1. Run `yarn build` in the project root
2. **If build succeeds**: Report success, list changed files
3. **If build fails**: Fix the issue and retry (max 3 attempts)

## Build Failure Fix Workflow

When the build fails:

1. **Read the error output** — identify the file, line number, and error type
2. **Open the file** at the error location
3. **Fix the issue** — common cases:
   - Missing import statement
   - Type mismatch or type error
   - Syntax error
   - Unused variable
4. **Re-run `yarn build`**
5. **If still failing**: Repeat steps 1-4
6. **If 3 attempts fail**: Stop and report the error to the user with full context

## Safety Constraints

- ❌ Do NOT add `@ts-ignore` comments to suppress errors
- ❌ Do NOT use `any` type to mask type errors
- ❌ Do NOT modify test files to fix build errors
- ✅ DO fix the root cause of the error

## Output Format

Report the final status as:

```
Build Status: PASS ✓
Changed files: [list of modified files]
```

Or if fixes were needed:

```
Build Status: PASS ✓ (after fixes)
Files fixed:
- path/to/file1.ts (error type: description)
- path/to/file2.tsx (error type: description)

Build output: [truncated output showing success]
```

Or if build failed permanently:

```
Build Status: FAIL ✗
Attempted 3 fixes without success
Error: [full error message]
Location: [file:line]
Next steps: [user guidance]
```

## Examples

**Example 1: Missing import**
```
Error: Cannot find module 'react'
→ Add: import React from 'react'
→ Build passes
```

**Example 2: Type mismatch**
```
Error: Type 'string' is not assignable to type 'number'
→ Fix: Change type or convert value appropriately
→ Build passes
```

**Example 3: Syntax error**
```
Error: Unexpected token '}'
→ Fix: Remove or add matching bracket
→ Build passes
```
