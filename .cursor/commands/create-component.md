# Create Component Command

**Shortcut:** `create-component` or `cc`

**Description:** Scaffolds a new React component with TypeScript support following project conventions.

## Usage

```bash
create-component <ComponentName> [options]
```

### Options

- `--app` — Create in `excalidraw-app/components/` (default)
- `--package` — Create in `packages/excalidraw/components/`
- `--hook` — Create as a custom hook (exported as `useComponentName.ts`)
- `--functional` — Create as functional component (default)
- `--with-tests` — Generate associated test file (`.test.tsx`)
- `--path <dir>` — Create at custom path relative to project root

### Examples

#### Create a simple functional component in app
```bash
create-component Button
```

Generates:
- `excalidraw-app/components/Button.tsx`

#### Create component with test file
```bash
create-component Modal --with-tests
```

Generates:
- `excalidraw-app/components/Modal.tsx`
- `excalidraw-app/components/Modal.test.tsx`

#### Create a custom hook in the main package
```bash
create-component useLocalStorage --hook --package
```

Generates:
- `packages/excalidraw/components/useLocalStorage.ts`

#### Create at custom path
```bash
create-component ThemeProvider --path excalidraw-app/contexts
```

Generates:
- `excalidraw-app/contexts/ThemeProvider.tsx`

## Generated Templates

### Functional Component (App)
```typescript
import { FC } from "react";

interface ComponentNameProps {
  // Props here
}

export const ComponentName: FC<ComponentNameProps> = (props) => {
  return <div>{/* Component JSX */}</div>;
};
```

### Functional Component (Package)
```typescript
import { FC } from "react";
import "./ComponentName.scss";

interface ComponentNameProps {
  // Props here
}

export const ComponentName: FC<ComponentNameProps> = (props) => {
  return <div className="component-name">{/* Component JSX */}</div>;
};
```

### Custom Hook
```typescript
import { useState } from "react";

export const useComponentName = () => {
  // Hook implementation
  return {};
};
```

### Test File
```typescript
import { render } from "@testing-library/react";
import { ComponentName } from "./ComponentName";

describe("ComponentName", () => {
  it("renders correctly", () => {
    const { container } = render(<ComponentName />);
    expect(container.firstChild).toBeInTheDocument();
  });
});
```

## Conventions

- **Naming:** PascalCase for components (e.g., `Button`, `Modal`)
- **Hooks:** Prefix with `use` (e.g., `useLocalStorage`, `useTheme`)
- **Props Interface:** Named as `ComponentNameProps`
- **Exports:** Named exports only (no default exports)
- **CSS:** Co-located in same directory for package components (e.g., `Button.scss`)
- **Location:** App components → `excalidraw-app/components/`, package components → `packages/excalidraw/components/`

## Post-Generation

After generating a component:

1. **Implement component logic** in the generated `.tsx` file
2. **Define props interface** with proper TypeScript types
3. **Add component styles** (if applicable)
4. **Write tests** if `--with-tests` was used
5. **Update barrel exports** if needed (e.g., `index.ts` files)
6. **Run validation:**
   ```bash
   yarn test:typecheck  # Verify TypeScript
   yarn test:update     # Run tests
   ```

## Related

- Security standards: See `.cursor/rules/security.mdc`
- Architecture patterns: See `.cursor/rules/architecture.mdc`
- Coding conventions: See `.cursor/rules/conventions.mdc`
