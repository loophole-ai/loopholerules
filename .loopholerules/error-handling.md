# Error Handling Standards

All errors must be handled explicitly. Silent failures and swallowed exceptions are not allowed.

## General Rules

- Never use an empty `catch` block.
- Always log the error with context before re-throwing or recovering.
- Use custom error classes for domain-specific errors so they can be caught precisely.
- Differentiate between **operational errors** (expected, recoverable) and **programmer errors** (bugs, should crash loud).

## API / Async Code

- Wrap all `async/await` calls in try-catch or use a result wrapper pattern.
- Never let a rejected promise go unhandled.
- Return meaningful HTTP status codes — don't send `500` for a validation error.

## Custom Error Classes

```ts
// Define domain errors
class NotFoundError extends Error {
  constructor(resource: string) {
    super(`${resource} not found`);
    this.name = "NotFoundError";
  }
}

class ValidationError extends Error {
  constructor(message: string) {
    super(message);
    this.name = "ValidationError";
  }
}
```

## Usage Pattern

```ts
// ❌ Bad
try {
  await deleteUser(id);
} catch (e) {}

// ✅ Good
try {
  await deleteUser(id);
} catch (error) {
  if (error instanceof NotFoundError) {
    return res.status(404).json({ message: error.message });
  }
  logger.error("Unexpected error deleting user", { error, userId: id });
  throw error;
}
```

## Frontend

- Always show user-friendly error messages — never expose raw error strings from the server.
- Use an error boundary at the top level of your React tree to catch uncaught UI errors.
