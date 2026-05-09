# Workflow: Create a New Component

Use this workflow whenever you need to create a new UI component from scratch.

---

## Steps

### 1. Define the Component
Describe what this component does in one sentence before writing any code.

> Example: "A button that triggers a form submission and shows a loading spinner while waiting."

### 2. Create the File
- Place it in the right folder (e.g., `src/components/ui/` for shared UI, `src/features/xyz/` for feature-specific).
- Name it in `PascalCase` (e.g., `SubmitButton.tsx`).

### 3. Define Props
Write the TypeScript interface for props first, before writing JSX.

```ts
interface SubmitButtonProps {
  label: string;
  isLoading?: boolean;
  onClick: () => void;
}
```

### 4. Write the Component

```tsx
export function SubmitButton({ label, isLoading = false, onClick }: SubmitButtonProps) {
  return (
    <button onClick={onClick} disabled={isLoading}>
      {isLoading ? "Loading..." : label}
    </button>
  );
}
```

### 5. Export It
- Use named exports, not default exports.
- Add it to the folder's `index.ts` barrel file if one exists.

### 6. Test It
Write at least one test covering the default render and one edge case (e.g., loading state).

---

## Checklist

- [ ] Props typed with an interface
- [ ] Component is in the right folder
- [ ] Named export used
- [ ] At least one test written
