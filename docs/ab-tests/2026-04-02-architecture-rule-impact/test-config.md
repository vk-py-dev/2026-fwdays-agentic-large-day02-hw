# Test Configuration

## Test Parameters

| Parameter | Value |
|-----------|-------|
| **Prompt** | "Create a new component for displaying element coordinates" |
| **Model** | Claude 4.5 Haiku |
| **Test Date** | April 2, 2026 |
| **Test Environment** | Cursor IDE, Project: 2026-fwdays-agentic-large-day02-hw |

## Rule Configuration

### Test A: ENABLED
- **File**: `.cursor/rules/architecture.mdc`
- **Status**: Active
- **Description**: Full Excalidraw architecture constraints applied

### Test B: DISABLED
- **File**: `.cursor/rules/architecture.mdc.off` (temporarily renamed)
- **Status**: Inactive
- **Description**: No architecture.mdc constraints applied

## Architecture Rules Content (for reference)

The `architecture.mdc` rule covers:
- **State Management**: Custom state via actionManager (NOT Redux/Zustand/MobX)
- **Rendering**: Canvas 2D rendering only (NOT React DOM, fabric.js, pixi.js)
- **Dependencies**: No new npm packages without approval
- **Verification**: Includes checklist for validation

## Test Execution Steps

### Test A (Enabled)
1. Verify architecture.mdc is active
2. Run prompt in Cursor Chat
3. Capture full response
4. Save to `test-a-enabled/response.md`

### Test B (Disabled)
1. Rename `.cursor/rules/architecture.mdc` → `.cursor/rules/architecture.mdc.off`
2. Close and reopen Cursor to clear caches
3. Run same prompt in Cursor Chat
4. Capture full response
5. Save to `test-b-disabled/response.md`
6. Rename `.cursor/rules/architecture.mdc.off` back to `.cursor/rules/architecture.mdc`

## Notes

- Same prompt executed twice to isolate the effect of the architecture rule
- Responses capture full AI reasoning for comprehensive analysis
- Manual execution ensures consistent test conditions
- Any differences in response style, length, or recommendations are noted
