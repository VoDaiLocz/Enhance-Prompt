# Prompt Library — Extended Templates

> Templates 7-11. Core templates (1-6): see `prompt-library.md`

---

## 7. 🧪 Testing

```markdown
## Context
[Framework] using [Jest / Vitest / pytest / Go test]. Coverage: [X%].
Target: `[file]` with [N] exported functions. Mocking: [library].
Existing test patterns: `[test directory / reference test file]`.

## Task
1. RED: Write failing test for `[function()]` — happy path
2. GREEN: Verify test fails with expected error
3. Add edge case tests: `[null / empty / overflow / concurrent]`
4. Add integration test: [workflow: login → dashboard → action]
5. Mock `[external service]` using `[mocking library/approach]`

## Constraints
- ✅ Follow test patterns in `[reference test file]`
- ✅ Each test: Arrange → Act → Assert (one assertion per test)
- ✅ Test BEHAVIOR, not implementation details
- ❌ Don't test private methods directly
- ❌ Don't use `any` type in test assertions

## Verification
- [ ] All new tests pass: `[test command]`
- [ ] Coverage increased from [X%] to [Y%]: `[coverage command]`
- [ ] No flaky tests — run 3x consecutively
- [ ] Each test name describes the behavior being tested
```

---

## 8. 🎨 UI / Styling

```markdown
## Context
[Framework] using [Tailwind / CSS Modules / styled-components / vanilla CSS].
Design system: `[theme file / tokens]`. Target component: `[path]`.
Reference: [Figma link / screenshot / description]. Breakpoints: [values].

## Task
1. Implement `[component]` matching [reference] exactly
2. Responsive: mobile [X]px → tablet [Y]px → desktop [Z]px+
3. States: [hover / focus / active / disabled / loading / error]
4. Animation: [describe transition/animation] with `prefers-reduced-motion`

## Constraints
- ✅ Use design tokens from `[theme file]` — no hardcoded colors/spacing
- ✅ WCAG 2.1 AA: 4.5:1 contrast, keyboard navigable, focus ring visible
- ✅ Semantic HTML: correct heading levels, ARIA labels where needed
- ❌ No inline styles, no `!important`
- ❌ No layout shifts on load (CLS = 0)

## Verification
- [ ] Visual match with reference at 3 breakpoints
- [ ] Tab through all interactive elements — focus order logical
- [ ] Screen reader announces all interactive elements
- [ ] `prefers-reduced-motion: reduce` → animations disabled
```

---

## 9. 🔌 API Integration

```markdown
## Context
[Framework] app. Integrating: [Service] API v[version].
Docs: [URL]. Auth: [API key / OAuth / JWT]. Rate limit: [X/min].
Base URL: `[url]`. SDK available: [yes/no — package name].

## Task
1. Create API client: `[file path]` using [fetch / axios / SDK]
2. Implement endpoints:
   - `[METHOD] [path]` → [what it does]
   - `[METHOD] [path]` → [what it does]
3. Error handling: retry [N]x with exponential backoff for 429/5xx
4. Timeout: [X]s per request, [Y]s total
5. Type definitions: create `[types file]` for all request/response shapes

## Constraints
- ✅ API keys in env vars ONLY — never in source code
- ✅ Handle ALL error codes: 400/401/403/404/429/500
- ✅ Log requests with correlation IDs for debugging
- ❌ Don't expose API keys to client-side bundles
- ❌ Don't ignore rate limits — implement backoff

## Verification
- [ ] `[endpoint]` returns expected data shape
- [ ] 429 response → backs off and retries successfully
- [ ] 500 response → retries [N]x then fails gracefully
- [ ] `grep -r "[API_KEY_VALUE]" src/` returns 0 results
- [ ] TypeScript: no `any` types in API responses
```

---

## 10. 🚀 Deployment / DevOps

```markdown
## Context
[Framework] app. Platform: [Vercel / AWS / Docker / GCP / Cloudflare].
Current: [manual deploy / basic CI]. Environment: [dev / staging / prod].
Infrastructure: [describe: database, cache, CDN, etc.].

## Task
1. Create [Dockerfile / CI config / deployment script] at `[path]`
2. Configure env vars: `[list: DATABASE_URL, API_KEY, NODE_ENV]`
3. Add health check: `GET [path]` → 200 + `{"status": "ok"}`
4. Set up [staging / production] pipeline with approval gate

## Constraints
- ✅ Zero-downtime deployment (rolling update / blue-green)
- ✅ Environment-specific configs — no shared secrets
- ✅ Rollback plan: revert to previous version within [X] minutes
- ❌ Don't commit `.env` or secrets to git
- ❌ Don't deploy without passing CI checks

## Verification
- [ ] `docker build .` succeeds (if Docker)
- [ ] CI pipeline: push → build → test → deploy completes
- [ ] Health check returns 200 after deploy
- [ ] Rollback tested: deploy bad version → rollback → healthy
- [ ] No secrets in git: `git log --all -p | grep -i "password\|secret"` = 0
```

---

## 11. 🗃️ Database / Migration

```markdown
## Context
ORM: [Prisma / TypeORM / SQLAlchemy / Drizzle] with [PostgreSQL / MongoDB / MySQL].
Schema: `[path]`. Models affected: [list]. Current data: ~[N] rows.
Last migration: [date]. Production database: [yes/no].

## Task
1. Create migration: [describe change: add column / new table / add index]
2. Write migration script: `[exact command to generate]`
3. Update ORM models/types to reflect new schema
4. Data migration: [transform existing data if needed]
5. Test migration: run up AND down (reversible)

## Constraints
- ✅ Migration MUST be reversible (up + down)
- ✅ Add indexes for columns used in WHERE/JOIN/ORDER BY
- ✅ Test on copy of production data before deploying
- ❌ Don't DROP columns without backup verification
- ❌ Don't run migrations during peak traffic hours
- ❌ Don't add NOT NULL without DEFAULT on existing columns with data

## Verification
- [ ] Migration up: `[command]` → succeeds
- [ ] Migration down: `[command]` → succeeds (reversible)
- [ ] Application code works with new schema
- [ ] Existing queries return same results
- [ ] `[ORM command]` shows no pending migrations
```
