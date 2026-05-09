# Naming Conventions

Consistent naming makes the codebase easier to read and navigate. Follow these rules across all files.

## Variables & Functions

- Use `camelCase` for variables and functions.
- Use descriptive names — avoid single letters except in short loops (`i`, `j`).
- Boolean variables should start with `is`, `has`, or `can` (e.g., `isLoading`, `hasError`).

## Components

- Use `PascalCase` for React components and their files.
- Component file name must match the component name exactly.

## Constants

- Use `SCREAMING_SNAKE_CASE` for top-level constants and env variables.

## Files & Folders

- Use `kebab-case` for all file and folder names (e.g., `user-profile.ts`, `auth-utils/`).
- Group related files in folders rather than using prefixes (e.g., `auth/login.ts` not `auth-login.ts`).

## Examples

```ts
// ❌ Bad
const x = true;
const userloggedin = false;
function FetchData() {}

// ✅ Good
const isLoggedIn = false;
const MAX_RETRY_COUNT = 3;
function fetchUserData(userId: string) {}
```
