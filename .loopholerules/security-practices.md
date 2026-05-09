# Security Practices

Security is not optional. These rules apply to every feature that touches user data, authentication, or external input.

## Input Validation

- Validate and sanitize ALL input from users, APIs, or query params — never trust it blindly.
- Use a schema validation library (e.g., `zod`, `joi`) for API request bodies.
- Never pass raw user input into SQL queries, shell commands, or file paths.

## Authentication & Authorization

- Never store passwords in plain text — always use `bcrypt` or `argon2`.
- Use short-lived JWTs (15–60 min) and refresh tokens stored in `httpOnly` cookies.
- Check authorization on every protected route — don't assume the frontend handles it.
- Use the principle of least privilege: users and services should only access what they need.

## Secrets & Environment Variables

- Never hardcode API keys, secrets, or credentials in source code.
- All secrets go in `.env` files and must be listed in `.gitignore`.
- Use a secrets manager (e.g., AWS Secrets Manager, Doppler) in production.

## Dependencies

- Regularly run `npm audit` or `pnpm audit` and fix high/critical vulnerabilities.
- Don't install packages you don't understand — check download counts and last publish date.
- Pin dependency versions in production.

## HTTP Security

- Always use HTTPS in production.
- Set security headers: `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options`.
- Rate-limit all public-facing endpoints to prevent abuse.

## Example — Input Validation with Zod

```ts
import { z } from "zod";

const CreateUserSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8).max(100),
  name: z.string().min(1).max(50),
});

// In your route handler
const result = CreateUserSchema.safeParse(req.body);
if (!result.success) {
  return res.status(400).json({ errors: result.error.flatten() });
}
```
