# Workflow: Build a REST API Endpoint

Follow this workflow when adding a new API route to ensure consistency, validation, and proper error handling every time.

---

## Steps

### 1. Define the Contract First
Before writing code, define:
- **Method:** GET / POST / PUT / PATCH / DELETE
- **Path:** e.g., `POST /api/users/:id/follow`
- **Request body / params / query:** What does it accept?
- **Response:** What does it return on success? On failure?

### 2. Create the Route File
Place it under `src/routes/` or `src/api/` depending on your structure.
Name it after the resource (e.g., `users.ts`, `posts.ts`).

### 3. Validate the Input
Use `zod` to validate the request body, params, and query before doing anything else.

```ts
const ParamsSchema = z.object({ id: z.string().uuid() });
const BodySchema = z.object({ reason: z.string().optional() });
```

### 4. Write the Controller Logic
Keep the route handler thin — move business logic into a service file.

```ts
// ✅ Thin controller
router.post("/users/:id/follow", async (req, res) => {
  const params = ParamsSchema.parse(req.params);
  const result = await userService.followUser(params.id, req.user.id);
  res.status(200).json(result);
});
```

### 5. Handle Errors
Wrap logic in try-catch and return appropriate HTTP status codes:
- `400` — Validation error
- `401` — Not authenticated
- `403` — Not authorized
- `404` — Resource not found
- `409` — Conflict (e.g., already following)
- `500` — Unexpected server error

### 6. Write the Service Function
Put business logic in `src/services/userService.ts`. Keep it testable and free of HTTP concerns.

### 7. Add to Router
Register the route in the main router file.

### 8. Test It
Write integration tests for:
- The happy path (valid input, expected response)
- Validation errors (missing/invalid fields)
- Auth errors (unauthenticated, unauthorized)
- Edge cases (resource not found, conflict)

---

## Checklist

- [ ] Contract defined before coding
- [ ] Input validated with zod
- [ ] Business logic in a service, not the route
- [ ] All error cases handled with correct status codes
- [ ] Integration tests written
