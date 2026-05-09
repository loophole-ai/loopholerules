# No Console Logs in Production Code

Never leave `console.log`, `console.warn`, or `console.error` statements in production code.

## Rules

- Remove all console statements before marking a task as done.
- If debugging is needed, use a proper logger (e.g., `winston`, `pino`) instead.
- The only exception is `console.error` inside a top-level error boundary or crash handler.

## Example

```js
// ❌ Bad
console.log("user data:", user);

// ✅ Good
logger.info("user data fetched", { userId: user.id });
```
