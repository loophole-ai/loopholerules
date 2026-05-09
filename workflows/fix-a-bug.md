# Workflow: Fix a Bug

A simple, repeatable process for investigating and resolving bugs without making things worse.

---

## Steps

### 1. Reproduce It First
Before touching any code, make sure you can reliably reproduce the bug.
- What are the exact steps to trigger it?
- Does it happen every time or only sometimes?
- What environment — local, staging, production?

### 2. Understand the Expected vs Actual Behavior
Write it out clearly:
- **Expected:** What should happen?
- **Actual:** What is happening instead?

### 3. Find the Root Cause
- Read the error message and stack trace carefully.
- Search the codebase for the function or component involved.
- Add temporary logs if needed to trace the data flow.
- Don't fix symptoms — find why it's broken.

### 4. Write a Failing Test (if possible)
Before fixing, write a test that reproduces the bug. This confirms you've found the root cause and prevents regressions.

### 5. Fix It
Make the smallest change possible that fixes the root cause. Avoid refactoring unrelated code in the same PR.

### 6. Verify
- Run the failing test — it should now pass.
- Manually retest the original steps to reproduce.
- Check that nothing nearby broke.

---

## Checklist

- [ ] Bug is reproducible
- [ ] Root cause identified (not just the symptom)
- [ ] Fix is minimal and targeted
- [ ] Test added or updated
- [ ] Manually verified
