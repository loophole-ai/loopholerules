# Workflow: Ship a Full Feature

End-to-end workflow for building and shipping a complete feature — from idea to production. Use this as your checklist every time you pick up a feature ticket.

---

## Phase 1 — Understand the Feature

Before writing a single line of code:

- [ ] Read the spec or ticket fully. If anything is unclear, ask now — not after building.
- [ ] Identify all user-facing surfaces (UI, API, notifications, etc.)
- [ ] Identify all system-side concerns (DB schema, background jobs, caching, etc.)
- [ ] Check if this touches any existing features that could break.
- [ ] Estimate complexity — if it's too big, break it into smaller tickets.

---

## Phase 2 — Design

- [ ] Sketch the data model changes needed (new tables, columns, relations)
- [ ] Design the API contract (routes, request/response shapes)
- [ ] Sketch the UI flow (rough wireframe or written description is fine)
- [ ] Identify edge cases upfront: what can go wrong? What states exist?
- [ ] Share the design with a teammate before building if it's complex

---

## Phase 3 — Build (Back to Front)

Build in this order to avoid blocking yourself:

#### 3a. Database / Data Layer
- Write and run migrations
- Update or create model types

#### 3b. Service Layer
- Write the core business logic
- No HTTP, no UI concerns here — pure logic that can be unit tested

#### 3c. API Layer
- Add routes with input validation
- Wire to service layer
- Handle all error cases with correct status codes

#### 3d. Frontend
- Build the UI components
- Connect to the API
- Handle loading, error, and empty states — not just the happy path

---

## Phase 4 — Test

- [ ] Unit tests for service/business logic
- [ ] Integration tests for API routes (happy path + error cases)
- [ ] Manual end-to-end test of the full user flow
- [ ] Test on mobile / different screen sizes if it's a UI feature
- [ ] Test with edge case data (empty lists, very long strings, special characters)

---

## Phase 5 — Polish

- [ ] Remove all debug logs and commented-out code
- [ ] Check for any hardcoded values that should be config or constants
- [ ] Make sure error messages shown to users are friendly and helpful
- [ ] Double-check loading and error states in the UI

---

## Phase 6 — Ship

- [ ] Open a PR with a clear description: what it does, how to test it, any tradeoffs
- [ ] Link the PR to the ticket
- [ ] Address all review comments before merging
- [ ] Merge to main, deploy to staging, verify on staging
- [ ] Deploy to production
- [ ] Monitor logs and error tracking for the first 30 minutes after deploy
- [ ] Close the ticket and notify stakeholders

---

## Notes

- If anything in Phase 1 or 2 is unclear, **stop and align** — building the wrong thing is the most expensive mistake.
- Small PRs ship faster and get better reviews. Break a large feature into 2–3 PRs if possible.
- Done means working in production, not just passing tests locally.
