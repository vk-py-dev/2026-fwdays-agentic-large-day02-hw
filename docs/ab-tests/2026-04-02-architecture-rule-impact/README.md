# A/B Test: Architecture Rule Impact on Component Design

## Hypothesis

The `architecture.mdc` rule significantly influences AI-generated component design approaches. With the rule enabled, responses should emphasize Canvas-first rendering, custom state management via actionManager, and adherence to Excalidraw's architectural constraints. Without the rule, responses may suggest standard React patterns, external libraries, or different state management solutions.

## Test Objective

Quantify and document the differences in architectural recommendations provided by the AI when the `architecture.mdc` rule is active vs. inactive.

## Methodology

- **Prompt**: "Create a new component for displaying element coordinates"
- **Model**: Claude 4.5 Haiku (Cursor default)
- **Execution**: Manual prompting through Cursor Chat
- **Test A**: architecture.mdc ENABLED
- **Test B**: architecture.mdc DISABLED (renamed to .mdc.off)
- **Comparison**: Side-by-side analysis of responses, focusing on architectural guidance

## Key Areas of Analysis

1. **Rendering Approach**: Canvas 2D vs. React DOM vs. external libraries
2. **State Management**: ActionManager vs. Redux/Zustand/other solutions
3. **Dependencies**: Use of external packages vs. internal utilities
4. **Component Structure**: File organization and folder suggestions
5. **Best Practices**: How well recommendations align with Excalidraw patterns

## Test Date

April 2, 2026

## Results Summary

### Key Finding: Rule IS Effective

The `architecture.mdc` rule **successfully constrains AI recommendations** toward Excalidraw patterns:

| Metric | Test A (Enabled) | Test B (Disabled) |
|--------|-----------------|------------------|
| ActionManager usage | ✅ Yes | ❌ useState only |
| Named exports | ✅ Yes | ❌ Default exports |
| Strict types | ✅ Yes | ⚠️ Loose types |
| No external libs | ✅ Yes | ⚠️ Potential issues |
| Canvas awareness | ✅ Yes | ❌ React DOM only |

**Conclusion**: Rule prevents architectural drift and ensures integration compatibility. **Recommend keeping active.**

---

## Test Documentation

### Browse Results

1. **[analysis.md](analysis.md)** — Comprehensive side-by-side analysis and effectiveness scoring
2. **[test-config.md](test-config.md)** — Test execution parameters and methodology
3. **[test-a-enabled/](test-a-enabled/)** — Rule ACTIVE responses
   - [prompt.md](test-a-enabled/prompt.md) — Test A prompt and context
   - [response.md](test-a-enabled/response.md) — AI response with architecture rule
4. **[test-b-disabled/](test-b-disabled/)** — Rule INACTIVE responses
   - [prompt.md](test-b-disabled/prompt.md) — Test B prompt and context
   - [response.md](test-b-disabled/response.md) — AI response without architecture rule
