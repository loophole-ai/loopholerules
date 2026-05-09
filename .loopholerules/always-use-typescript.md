# Always Use TypeScript

All new files must be written in TypeScript. No plain `.js` files.

## Rules

- Use `.ts` for logic files and `.tsx` for React components.
- Always define types for function parameters and return values.
- Avoid using `any` — use `unknown` if the type is truly unknown, then narrow it.
- Enable strict mode in `tsconfig.json`.

## Example

```ts
// ❌ Bad
function getUser(id) {
  return fetch(`/api/users/${id}`);
}

// ✅ Good
async function getUser(id: string): Promise<User> {
  const res = await fetch(`/api/users/${id}`);
  return res.json();
}
```
