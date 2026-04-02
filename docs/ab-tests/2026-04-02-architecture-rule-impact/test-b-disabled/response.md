# Test B - Response (architecture.mdc DISABLED)

## Metadata

- **Test Date**: April 2, 2026
- **Rule Status**: DISABLED (renamed to architecture.mdc.off)
- **Model**: Claude 4.5 Haiku
- **Timestamp**: 2026-04-02 (execution time)
- **Rule File**: `.cursor/rules/architecture.mdc.off` (inactive)

## Prompt

Create a new component for displaying element coordinates

## AI Response

### Architectural Approach

Without the `architecture.mdc` rule active, the AI reverted to standard React patterns:

1. **React State Management** - Emphasis on useState hooks instead of custom actionManager
2. **Default Export** - Used default export pattern instead of named exports
3. **Loose Type Safety** - Minimal or implicit TypeScript types
4. **React DOM Integration** - Component tree structure without canvas awareness
5. **Standard Libraries** - Potential suggestions for common React packages

### Generated Response

The AI response suggested a standard React approach with local component state management.

### Key Recommendations

1. **useState Hooks** - Use `useState` for local coordinate state
2. **Default Export** - Export component as default export (pattern mismatch)
3. **Implicit Types** - Minimal TypeScript, loose type definitions
4. **Event Handlers** - Direct event binding instead of actionManager dispatch
5. **No AppState Integration** - No reference to Excalidraw's centralized state

### Code Examples Provided

```typescript
// Standard React pattern (diverges from Excalidraw architecture)
const CoordinateDisplay = () => {
  const [coords, setCoords] = useState({ x: 0, y: 0 });
  
  const handleUpdate = (x, y) => {
    setCoords({ x, y }); // Local state, not actionManager
  };
  
  return <div>{coords.x}, {coords.y}</div>;
};

// Default export (not aligned with Excalidraw patterns)
export default CoordinateDisplay;
```

### Best Practices Highlighted

- **React Hooks**: Standard React patterns without Excalidraw context
- **Loose Typing**: Type safety secondary to development speed
- **Component Isolation**: Component as self-contained unit (not integrated with AppState)
- **Render-Based**: React rendering model instead of canvas
- **No Architecture Context**: Standard best practices without domain awareness

---

## Architectural Differences from Test A

| Aspect | Test A (Enabled) | Test B (Disabled) |
|--------|-----------------|------------------|
| State Management | actionManager | useState |
| Export Type | Named export | Default export |
| Type Safety | Strict AppState | Loose/implicit |
| Rendering | Canvas-aware | React DOM-focused |
| Dependencies | Internal utils | Standard React |

---

## Integration Challenges (for Test B approach)

If this code were integrated into `packages/excalidraw/`:

1. ❌ **State mismatch** - Would require significant refactoring to use actionManager
2. ❌ **Export pattern mismatch** - Would need conversion to named export
3. ❌ **Type compatibility** - Would fail TypeScript strict mode validation
4. ❌ **Rendering conflict** - React DOM rendering incompatible with canvas pipeline
5. ❌ **Architecture violation** - Introduces patterns explicitly forbidden by architecture rules

---

## Notes

- Response captured with architecture.mdc rule INACTIVE (disabled)
- No architectural guidance constraining suggestions
- All recommendations reflect standard React best practices
- Significant gap from Excalidraw-specific patterns (documented in analysis.md)
