# Professional Prompt Engineering Patterns

> The 7-Layer Enhancement framework. Each layer is mandatory.

---

## The Scoring System

Rate the raw prompt (1-5) on each dimension before and after enhancement:

| Dimension | 1 (Poor) | 5 (Excellent) |
|-----------|----------|---------------|
| **Clarity** | Ambiguous, multiple interpretations | Single clear meaning |
| **Specificity** | No file names, no details | Exact files, lines, functions |
| **Context** | Zero background info | Full tech stack + patterns |
| **Structure** | Wall of text | Clean sections |
| **Constraints** | No boundaries | Clear DO/DON'T rules |
| **Output** | No format specified | Exact expected format |
| **Verification** | No success criteria | Testable conditions |

**Score < 15:** Heavy enhancement — full rewrite + codebase scan + interactive Q&A
**Score 15-25:** Medium enhancement — structured rewrite with context injection
**Score 25-35:** Light enhancement — polish + add missing layers

---

## Layer 1: Clarity — Kill Ambiguity

**Technique:** Replace every vague noun/verb with a concrete noun/verb.

```
❌ "Fix the bug"
✅ "Fix the null reference error in `handleSubmit()` at `src/forms/ContactForm.tsx:42`"

❌ "Make it faster"
✅ "Reduce initial page load time from 3.2s to under 1.5s by lazy-loading images"

❌ "Update the API"
✅ "Add `GET /api/users/:id/preferences` endpoint returning `{ theme, language }` JSON"
```

**RED FLAG:** If the enhanced prompt can be interpreted two different ways, Layer 1 failed.

---

## Layer 2: Specificity — Concrete Details

**Pattern:** `[Action] + [Target] + [Location] + [Expected Result]`

```
❌ "Add authentication"
✅ "Implement JWT-based authentication in `src/middleware/auth.ts`:
    - Extract token from `Authorization: Bearer <token>` header
    - Verify against `JWT_SECRET` env variable
    - Attach decoded payload to `req.user`
    - Return 401 if token invalid/expired"
```

**RED FLAG:** If the prompt has no file paths or function names, Layer 2 failed.

---

## Layer 3: Context Injection

**Always extract from codebase scan:**

| Context Type | Example |
|-------------|---------|
| **Tech Stack** | "Next.js 14 App Router with TypeScript, Prisma ORM, PostgreSQL" |
| **File Structure** | "Components in `src/components/`, API routes in `src/app/api/`" |
| **Existing Patterns** | "Repository pattern: `src/repositories/UserRepository.ts`" |
| **Dependencies** | "Using `zod` for validation, `tanstack-query` for data fetching" |
| **Constraints** | "Must be backward-compatible with existing v1 API clients" |

**RED FLAG:** If you could paste the same prompt into any project, Layer 3 failed.

---

## Layer 4: Structure — The 4-Section Format

```markdown
## Context
[Project info, tech stack, relevant files, current state]

## Task
[Specific numbered action items, ordered by priority]

## Constraints
[DO/DON'T rules, boundaries, anti-patterns, edge cases]

## Output Format
[Expected format: code, diff, step-by-step, documentation]
```

**RED FLAG:** If the prompt is a wall of text without headers, Layer 4 failed.

---

## Layer 5: Constraints — Define Boundaries

| Type | Example |
|------|---------|
| **Technical** | "Must work with Node.js 18+, no native modules" |
| **Style** | "Follow existing code style: functional components, no class components" |
| **Performance** | "Response time < 200ms, bundle size < 50KB" |
| **Security** | "Sanitize all user inputs, parameterize SQL queries" |
| **Negative** | "Do NOT modify `src/core/` files, do NOT add new dependencies" |

**RED FLAG:** If you can't answer "what should I NOT do?", Layer 5 failed.

---

## Layer 6: Output Format

| Format | When to Use |
|--------|-------------|
| **Complete file** | "Return the complete modified file content" |
| **Diff only** | "Show only the changed lines" |
| **Step-by-step** | "Numbered steps with verification at each step" |
| **Comparison table** | "Compare options with pros/cons" |
| **Documentation** | "Create docs with code examples" |

**RED FLAG:** If the AI could respond in any format, Layer 6 failed.

---

## Layer 7: Verification — Success Criteria

```markdown
## Verification
- [ ] `npm run test` passes with 0 failures
- [ ] `GET /api/users/1` returns 200 with user JSON
- [ ] No TypeScript errors (`npx tsc --noEmit`)
- [ ] Bundle size under 50KB
```

**RED FLAG:** If "done" is subjective, Layer 7 failed.

---

## Multilingual Handling

When a non-English prompt is detected:

1. **Detect language** — identify input language automatically
2. **Preserve intent** — translate meaning, not word-by-word
3. **Standardize terms** — use English for all technical terms
4. **Bilingual output** — enhanced prompt in user's language with English technical terms
5. **Include mapping** — show original term → standardized English term
