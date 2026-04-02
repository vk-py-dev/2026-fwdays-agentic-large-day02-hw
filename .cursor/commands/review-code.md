# Review Code

Perform a comprehensive code review on the selected file(s) or code snippet.

## Instructions

Please review the following code for:

1. **Security Issues**
   - Input validation and sanitization
   - XSS prevention and HTML injection risks
   - CSRF protection in state-changing operations
   - Sensitive data handling and exposure
   - Authentication/authorization checks
   - File upload validation

2. **Code Quality**
   - Readability and maintainability
   - Adherence to project conventions and patterns
   - Unnecessary complexity or duplication
   - Performance considerations
   - Memory leaks or resource management issues
   - Proper error handling and edge cases

3. **Type Safety**
   - TypeScript type annotations
   - Potential type errors
   - Use of `any` types
   - Proper generic typing

4. **Testing**
   - Test coverage adequacy
   - Test quality and edge cases
   - Mocking and dependency injection patterns

5. **Documentation**
   - Missing or unclear comments
   - JSDoc completeness for public APIs
   - Consistency with existing documentation

6. **Architecture**
   - Adherence to project architecture patterns
   - Proper separation of concerns
   - Appropriate use of abstractions
   - Dependencies on protected files

## Output Format

Provide a structured review with:
- ✅ Strengths (things done well)
- ⚠️ Issues (problems to fix)
- 💡 Suggestions (improvements to consider)
- 🔒 Security notes (if applicable)
- 📋 Checklist of action items (if any)

## Context

This project follows specific security and architectural standards defined in:
- `.cursor/rules/security.mdc` - Security best practices
- `.cursor/rules/architecture.mdc` - Architectural patterns
- `.cursor/rules/conventions.mdc` - Code conventions
- `AGENTS.md` - Project structure and workflow

## Example Usage for Excalidraw

**Command:**
```bash
/review-code packages/excalidraw/components/Button.tsx
```

**Expected Output Checklist:**

✅ **Strengths**
- Named exports used correctly
- TypeScript types properly applied

⚠️ **Issues**
- Security: Check SVG sanitization if rendering user content
- Architecture: Verify state management uses actionManager not useState
- Dependencies: Confirm no external canvas libraries imported

🔒 **Security Notes**
- Input validation: User-supplied element data validated
- XSS Prevention: No innerHTML used with user data
- File imports: If handling .excalidraw files, validate schema

📋 **Action Items**
- [ ] Verify actionManager usage for state
- [ ] Check for any forbidden patterns (.cursor/rules/do-not-touch.mdc)
- [ ] Run yarn test:typecheck to validate types


