# Enhanced Prompt Output Format

> Every enhanced prompt MUST follow this structure. No exceptions.

<HARD-GATE>
Do NOT present an enhanced prompt without a before/after scoring table.
The user must SEE the improvement quantified. "Better" is not a metric.
</HARD-GATE>

---

## The Complete Output Structure

```markdown
## 🏷️ Detected Category
**[emoji] [Category Name]** — Confidence: [High/Medium/Low]
[If chain: "Multi-intent detected → See Prompt Chain below"]

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
[Bullet list: what was improved and WHY — not just what changed]
- **Layer X:** [What changed] → [Why it matters for output quality]

---

## 📋 Copy-Ready Prompt
[Clean version of the Enhanced Prompt section ONLY (Context + Task + Constraints + Output Format + Verification). No scoring table, no enhancement notes, no risk assessment, no alternative approaches. Ready to paste into any AI tool.]
```

---

## Conditional Sections

Not every prompt needs every section. Apply these rules:

| Section | Include When | Skip When |
|---------|-------------|-----------|
| 🏷️ Detected Category | Always | Never — always show detected category and confidence |
| ⏱️ Difficulty Estimate | Always | Never — always include |
| ⚠️ Risk Assessment | Task touches production, data, security, or infrastructure | Pure UI, documentation, or low-risk refactors |
| 🔀 Alternative Approaches | Multiple valid strategies exist AND choice impacts architecture | Single obvious solution OR user specified the approach |
| 💡 Enhancement Notes | Always | Never — user must understand what changed |
| 🔗 Prompt Chain | Multi-intent detected (2+ categories) | Single-intent prompt |
| 🔄 Iteration Delta | User requested refinement (v2+) | First enhancement (v1) |

**Rule:** When skipping a section, do NOT include the header. A missing section is cleaner than an empty one.

---

## Output Efficiency Rules

<HARD-GATE>
The enhanced prompt must be MORE EFFICIENT than the original, not just longer. Length ≠ quality.
</HARD-GATE>

| Rule | Why |
|------|-----|
| **No filler sentences** | "This is a complex task that requires careful attention" adds zero value |
| **No redundant context** | If tech stack is in Context, don't repeat it in Task |
| **Constraints must be actionable** | "Write good code" is not a constraint — "Follow existing patterns in `src/utils/`" is |
| **Verification must be testable** | "Works correctly" → fails. "`npm run test` passes with 0 failures` → passes |
| **Copy-Ready = Enhanced Prompt minus metadata** | Don't rewrite — extract the Context/Task/Constraints/Output/Verification sections cleanly |

**Token Budget Guideline:**
- Simple prompts (score < 15): Enhanced output should be 150-300 words
- Medium prompts (score 15-25): Enhanced output should be 200-500 words
- Complex prompts (score 25-35): Enhanced output should be 300-700 words

If the enhanced prompt exceeds these ranges, check for redundancy.

---

## Scoring Accuracy Gates

| Gate | Rule |
|------|------|
| **No inflated "After" scores** | Every score of 4-5 must be justified by specific content in the enhanced prompt |
| **Clarity = 5** requires single unambiguous interpretation | If two devs could read it differently, max score is 3 |
| **Specificity = 5** requires file paths + function names | No paths = max score is 2 |
| **Context = 5** requires codebase-specific details | Generic tech stack mention = max score is 3 |
| **Before ≠ always 1** | A well-structured but incomplete prompt might score 3 on Structure. Be honest. |
| **Total improvement > 20 points is suspicious** | Verify each dimension — inflation helps no one |

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

## 💡 Enhancement Notes
- **Clarity:** "optimize the database" → 4 specific, actionable tasks with exact table/column names
- **Context:** Injected Prisma ORM + PostgreSQL details from codebase scan, identified the 2 slowest queries from logs
- **Constraints:** Added backward-compatibility requirement (no API response shape changes) — critical for production
- **Verification:** Replaced subjective "faster" with measurable thresholds (< 500ms, < 300ms)

## 📋 Copy-Ready Prompt
Express.js + TypeScript API using Prisma ORM with PostgreSQL 15. Schema at `prisma/schema.prisma` (23 models, 47 relations). Slowest queries: `GET /api/orders` (2.3s, joins 4 tables), `GET /api/users/:id/activity` (1.8s, full table scan).

1. Add composite index on `orders` table: `(userId, createdAt DESC)`
2. Add `@@index([userId])` to `Activity` model in `schema.prisma`
3. Rewrite `GET /api/orders` query to use `select` instead of `include`
4. Add connection pooling via `pgbouncer` in `DATABASE_URL`

Constraints:
- Create Prisma migration for each schema change
- Benchmark before and after with `EXPLAIN ANALYZE`
- Don't modify existing data or drop columns
- Don't change API response shapes (backward compatible)

Return modified files as diffs with `EXPLAIN ANALYZE` output showing improvement.

Verify: `GET /api/orders` < 500ms, `GET /api/users/:id/activity` < 300ms, `npx prisma migrate dev` succeeds, all existing API tests pass.
```

---

## Red Flags — STOP and Redo

- No scoring table → Output is incomplete
- "After" scores not higher than "Before" → Enhancement failed
- "After" scores all 5/5 without justification → Score inflation, re-evaluate honestly
- Copy-Ready section missing → User can't use the output
- Copy-Ready section is a rewrite instead of a clean extraction → Redundant work, extract don't rewrite
- No codebase-specific details in Context → Generic prompt, redo scan
- Verification criteria are subjective ("works well") → Redo Layer 7
- Enhanced prompt is longer than 700 words for a simple task → Over-verbose, trim redundancy
- Same information appears in multiple sections → Consolidate to single location
- Constraints contain non-actionable statements ("write clean code") → Replace with specific rules
- Multi-intent prompt forced into single template → Use Prompt Chain Decomposition
- Auto-detected category doesn't match actual intent → Re-check signals, ask user
- Iteration makes scores worse (delta ≤ -2) → Revert iteration, try different approach
