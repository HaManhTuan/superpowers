---
name: writing-plans
description: Use when you have a spec or requirements for a multi-step task, before touching code
---

# Writing Plans

## Overview

Turn requirements into clear, executable task lists. Scale the plan to the scope — don't write a novel for a simple feature.

**Announce at start:** "I'm using the writing-plans skill to create the implementation plan."

---

## Quick Mode (Quick/Standard scope)

For Quick and Standard tasks, skip the plan file. Instead:

1. Create a `TodoWrite` with the implementation steps
2. List the files you'll touch
3. Proceed directly to execution

Example TodoWrite for a Standard task:
```
- [ ] Write failing test for X
- [ ] Implement X in src/foo.ts
- [ ] Run tests, verify pass
- [ ] Commit
```

That's all you need. No file, no commit, no handoff ceremony.

---

## Full Mode (Complex scope only)

For Complex tasks, write a proper plan document.

**Save plans to:** `docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md`

### Plan Document Header

Every plan MUST start with this header:

```markdown
# [Feature Name] Implementation Plan

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

### File Structure

Before defining tasks, map which files will be created or modified and what each is responsible for:
- Each file should have one clear responsibility
- Files that change together should live together
- Follow existing codebase patterns

### Task Structure

````markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.ts`
- Modify: `exact/path/to/existing.ts`
- Test: `tests/exact/path/to/test.ts`

- [ ] **Step 1: Write the failing test**

```typescript
test('specific behavior', () => {
  const result = fn(input)
  expect(result).toBe(expected)
})
```

- [ ] **Step 2: Run test to verify it fails**

Run: `npm test path/to/test`
Expected: FAIL

- [ ] **Step 3: Write minimal implementation**

```typescript
function fn(input) {
  return expected
}
```

- [ ] **Step 4: Run test to verify it passes**

Run: `npm test path/to/test`
Expected: PASS

- [ ] **Step 5: Commit**

```bash
git add <files>
git commit -m "feat: add specific feature"
```
````

### Bite-Sized Granularity

Each step is one action (2-5 minutes):
- "Write the failing test" — step
- "Run it to verify it fails" — step
- "Implement minimal code" — step
- "Run tests and verify pass" — step
- "Commit" — step

### No Placeholders

Every step must contain what an engineer actually needs. These are plan failures:
- "TBD", "TODO", "implement later"
- "Add appropriate error handling"
- "Write tests for the above" (without actual test code)
- Steps that describe what to do without showing how

### Scope Check

If the spec covers multiple independent subsystems, suggest breaking into separate plans. Each plan should produce working, testable software on its own.

### Self-Review

After writing the complete plan, check:
1. **Spec coverage:** Can you point to a task for each requirement?
2. **Placeholder scan:** Any TBDs or vague steps? Fix them.
3. **Type consistency:** Do types/method names match across tasks?

Fix issues inline. Then proceed to execution using `superpowers:executing-plans`.

---

## Remember

- Quick task → TodoWrite items, no file
- Complex task → Full plan doc with code in every step
- Always TDD — test first, implementation second
- Exact file paths, exact commands, exact expected output
