# Enhanced Prompt Output Format

> Every enhanced prompt MUST follow this structure. No exceptions.

<HARD-GATE>
Do NOT present an enhanced prompt without a before/after scoring table.
The user must SEE the improvement quantified. "Better" is not a metric.
</HARD-GATE>

---

## The Complete Output Structure

```markdown
## 📊 Enhancement Summary

| Metric | Before | After |
|--------|--------|-------|
| Clarity | [1-5] | [1-5] |
| Specificity | [1-5] | [1-5] |
| Context | [1-5] | [1-5] |
| Structure | [1-5] | [1-5] |
| Constraints | [1-5] | [1-5] |
| Output Format | [1-5] | [1-5] |
| Verification | [1-5] | [1-5] |
| **Total** | **[/35]** | **[/35]** |

---

## 🔴 Original Prompt
> [paste original prompt in blockquote]

---

## 🟢 Enhanced Prompt

### Context
[Project background, tech stack, relevant files from codebase scan]

### Task
1. [Primary action — most critical]
2. [Secondary action]
3. [Follow-up action]

### Constraints
- ✅ DO: [What to follow]
- ❌ DON'T: [What to avoid]
- ⚡ PERFORMANCE: [If applicable]
- 🔒 SECURITY: [If applicable]

### Output Format
[Exact expected output: complete file, diff, step-by-step, docs]

### Verification
- [ ] [Testable criterion 1]
- [ ] [Testable criterion 2]
- [ ] [Testable criterion 3]

### ⏱️ Difficulty Estimate
| Aspect | Estimate |
|--------|----------|
| Complexity | [Low / Medium / High] |
| Time | [~30 min / ~2 hours / ~1 day] |
| Risk | [Low / Medium / High] |
| Files Affected | [Count] |

### ⚠️ Risk Assessment
- [🔴 High] [Risk + mitigation strategy]
- [🟡 Medium] [Risk + mitigation strategy]
- [🟢 Low] [Risk + mitigation strategy]

### 🔀 Alternative Approaches
| Approach | Pros | Cons | Best When |
|----------|------|------|-----------|
| A: [Name] | [+] | [-] | [Scenario] |
| B: [Name] | [+] | [-] | [Scenario] |

---

## 💡 Enhancement Notes
[What was improved and WHY — not just what changed]

---

## 📋 Copy-Ready Prompt
[Clean version. No scoring, no commentary. Ready to paste into any AI tool.]
```

---

## Example: Complete Enhancement

### Input
> optimize the database

### Output

```markdown
## 📊 Enhancement Summary
| Metric | Before | After |
|--------|--------|-------|
| Clarity | 1 | 5 |
| Specificity | 1 | 5 |
| Context | 1 | 5 |
| Structure | 1 | 5 |
| Constraints | 1 | 4 |
| Output Format | 1 | 5 |
| Verification | 1 | 5 |
| **Total** | **7/35** | **34/35** |

## 🔴 Original Prompt
> optimize the database

## 🟢 Enhanced Prompt

### Context
Express.js + TypeScript API using Prisma ORM with PostgreSQL 15.
Schema at `prisma/schema.prisma` (23 models, 47 relations).
Slowest queries identified via `prisma.$queryRaw` logs:
- `GET /api/orders` — 2.3s (joins 4 tables)
- `GET /api/users/:id/activity` — 1.8s (full table scan)

### Task
1. Add composite index on `orders` table: `(userId, createdAt DESC)`
2. Add `@@index([userId])` to `Activity` model in `schema.prisma`
3. Rewrite `GET /api/orders` query to use `select` instead of `include`
4. Add connection pooling via `pgbouncer` in `DATABASE_URL`

### Constraints
- ✅ Create Prisma migration for each schema change
- ✅ Benchmark before and after with `EXPLAIN ANALYZE`
- ❌ Don't modify existing data or drop columns
- ❌ Don't change API response shapes (backward compatible)

### Output Format
Return modified files as diffs with `EXPLAIN ANALYZE` output showing improvement.

### Verification
- [ ] `GET /api/orders` response time < 500ms
- [ ] `GET /api/users/:id/activity` response time < 300ms
- [ ] `npx prisma migrate dev` runs without errors
- [ ] All existing API tests pass

### ⏱️ Difficulty Estimate
| Aspect | Estimate |
|--------|----------|
| Complexity | Medium |
| Time | ~2 hours |
| Risk | Medium |
| Files Affected | 4 |

### ⚠️ Risk Assessment
- [🟡 Medium] Migration on production — run during low traffic
- [🟢 Low] Index creation — non-blocking on PostgreSQL 15

### 🔀 Alternative Approaches
| Approach | Pros | Cons | Best When |
|----------|------|------|-----------|
| A: Prisma indexes | ORM-managed, type-safe | Limited control | Most cases |
| B: Raw SQL indexes | Full control | Manual migration | Complex indexes |
| C: Redis cache layer | Fastest reads | Stale data risk | Read-heavy APIs |
```

---

## Red Flags — STOP and Redo

- No scoring table → Output is incomplete
- "After" scores not higher than "Before" → Enhancement failed
- Copy-Ready section missing → User can't use the output
- No codebase-specific details in Context → Generic prompt, redo scan
- Verification criteria are subjective ("works well") → Redo Layer 7
