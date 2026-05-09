# Workflow: Refactor a Module

Use this workflow when a module has grown too large, is hard to understand, or is violating separation of concerns. Refactoring without a plan causes more bugs than it fixes — follow these steps.

---

## Golden Rule
> Never refactor and add features at the same time. Do one or the other in a PR.

---

## Steps

### 1. Understand Before You Change
Read the entire module before touching a single line.
- What does it do?
- What does it depend on?
- What depends on it? (Check all importers with a global search)

### 2. Make Sure Tests Exist
If the module has no tests, **write them first** before refactoring. This is non-negotiable — tests are your safety net.

```bash
# Find test coverage for the file
npx jest --coverage --collectCoverageFrom="src/module-name.ts"
```

### 3. Identify the Problems
Write down what's wrong before fixing it. Common issues:
- Function is doing too many things (violates single responsibility)
- Module is too large (300+ lines is a smell)
- Business logic mixed with I/O or HTTP concerns
- Repeated code that should be extracted
- Poor naming that makes intent unclear

### 4. Plan the Refactor
Sketch out the new structure:
- What files will exist after?
- What are the new boundaries?
- What stays, what moves, what gets deleted?

Share the plan with your team before starting on large refactors.

### 5. Refactor in Small Steps
Make one change at a time, run tests after each step. Don't do a big-bang rewrite.

Typical order:
1. Extract pure utility functions first (easiest, lowest risk)
2. Extract types and interfaces
3. Split large functions into smaller named ones
4. Move groups of related functions into separate files
5. Update imports everywhere

### 6. Keep the Public API Stable
If other code depends on this module's exports, don't change the public interface unless that's the goal. Use internal refactoring that leaves exports intact.

### 7. Run the Full Test Suite
```bash
npx jest
```
All tests must pass. If something broke, fix it now — don't move on.

### 8. Review the Diff
Before opening a PR, read your own diff top to bottom. Ask yourself:
- Is every change justified?
- Did I accidentally change any behavior?
- Is the code clearly better than before?

---

## Checklist

- [ ] Read and understood the module before starting
- [ ] Tests exist before refactoring began
- [ ] Problems clearly identified and written down
- [ ] Plan reviewed (for large refactors)
- [ ] Refactored in small, incremental steps
- [ ] Public API preserved (or change is intentional)
- [ ] All tests pass
- [ ] Diff reviewed before opening PR
