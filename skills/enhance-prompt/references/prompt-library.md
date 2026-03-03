# Prompt Library — Core Templates

> 6 battle-tested templates. Copy → fill `[brackets]` → use.
> Extended templates (Testing, UI, API, DevOps, Database, Deep Scan, Code Review): see `prompt-library-extended.md`

---

## 1. 🐛 Bug Fix

```markdown
## Context
[Framework] project. Error: `[exact error message]` in `[file:line]`.
Triggered when: [user action]. Stack trace points to `[function()]`.
Related files: `[list affected files]`.

## Task
1. Reproduce: [exact steps to trigger]
2. Root cause: trace `[function()]` → identify why `[bad value/state]` occurs
3. Fix: [specific change] in `[file:line]` while preserving [existing behavior]
4. Edge case: handle `[null/empty/overflow/concurrent]` scenario

## Constraints
- ✅ Follow existing error handling in `[reference file]`
- ✅ Add regression test before fixing (TDD: RED → GREEN)
- ❌ Don't modify `[protected files]`
- ❌ Don't change public API signatures

## Verification
- [ ] Bug no longer reproduces with exact trigger steps
- [ ] Edge case handled gracefully → [expected fallback]
- [ ] All existing tests pass: `[test command]`
- [ ] New regression test added and passing
```

---

## 2. ✨ New Feature

```markdown
## Context
[Framework] project. Feature location: `[directory]`.
Similar existing feature: `[reference file]` — follow same patterns.
Dependencies available: `[relevant packages]`.

## Task
1. Create `[new file]` implementing [feature] following `[reference pattern]`
2. Integrate with `[existing module]` via [method: import/hook/middleware]
3. Add [UI component / API endpoint / service method] for [user action]
4. Write tests following patterns in `[test directory]`

## Constraints
- ✅ Follow patterns from `[reference file]` exactly
- ✅ Use existing dependencies — no new packages
- ✅ TDD: write failing test first, then implement
- ❌ Don't modify `[core files]`

## Verification
- [ ] [User action] → [expected result]
- [ ] Integration with `[module]` works: [how to verify]
- [ ] Tests pass: `[test command]`
- [ ] No regressions in `[related features]`
```

---

## 3. ⚡ Performance

```markdown
## Context
[Framework] app. Current: [metric] = [value]. Target: < [value].
Bottleneck: `[file:function]`. Profiling shows: [evidence/data].
Measured with: [tool: Lighthouse / Chrome DevTools / ab / k6].

## Task
1. Benchmark current state: `[exact command]` → record baseline
2. Optimize `[function()]`: apply [strategy: lazy-load/cache/memo/split]
3. Benchmark after: same command → compare
4. Document improvement in commit message

## Constraints
- ✅ Measure BEFORE and AFTER — no "feels faster"
- ✅ Smallest change that achieves target
- ❌ Don't sacrifice readability for micro-optimizations
- ❌ Don't introduce new dependencies for < 20% improvement

## Verification
- [ ] [Metric] reduced from [X] to [Y] (below target [Z])
- [ ] No functional regressions: `[test command]`
- [ ] Benchmark data saved/committed
```

---

## 4. 🔄 Refactor

```markdown
## Context
[Framework] project. `[file/module]` grew to [X] lines.
Code smells: [list: god class / long method / duplication / tight coupling].
Used by [N] other files: `[list import sites]`.

## Task
1. Extract `[responsibility]` from `[file]` into new `[new-file]`
2. Apply [pattern: Repository / Strategy / Factory / Facade]
3. Update all [N] import sites to point to new location
4. Verify zero behavior change with existing tests

## Constraints
- ✅ PURE structural refactor — zero behavior changes
- ✅ Update ALL import paths — grep for old imports
- ✅ Run full test suite after each extraction
- ❌ Don't change public API or interfaces
- ❌ Don't "improve" logic while refactoring — separate PR

## Verification
- [ ] All existing tests pass UNCHANGED: `[test command]`
- [ ] `grep -r "[old import]" src/` returns 0 results
- [ ] `[file]` reduced from [X] to [Y] lines
- [ ] No unused imports or dead code
```

---

## 5. 🔒 Security Audit

```markdown
## Context
[Framework] app handling [data type: PII / payment / auth tokens].
Auth method: [JWT / session / OAuth]. Attack surface: [endpoints / forms / uploads].
Dependencies: [N] packages, last audited: [date or never].

## Task
1. Run `[npm audit / pip audit / cargo audit]` — document findings
2. Check OWASP Top 10 in `[scope/files]`:
   - A01: Broken Access Control → check `[auth middleware]`
   - A03: Injection → check `[database query files]`
   - A07: XSS → check `[template/render files]`
3. Review secrets management — verify no hardcoded keys
4. Check dependency CVEs — upgrade critical/high severity

## Constraints
- ✅ Prioritize: Critical > High > Medium > Low
- ✅ Include CVE IDs for known vulnerabilities
- ✅ Provide fix for each finding, not just the problem
- 🔒 Test with safe payloads only — no destructive testing

## Output Format
| # | Severity | Location | Issue | Fix | CVE |
|---|----------|----------|-------|-----|-----|

## Verification
- [ ] `[audit command]` shows 0 critical/high vulnerabilities
- [ ] All user inputs validated and sanitized
- [ ] No secrets in source code: `grep -r "password\|secret\|api_key" src/`
```

---

## 6. 📝 Documentation

```markdown
## Context
[Framework] project. Undocumented: `[module/API/component]` at `[path]`.
[N] public functions, [N] exported types. Target audience: [devs / users / both].
Existing docs: [location or "none"]. Doc style: [JSDoc / Google / NumPy].

## Task
1. Add [JSDoc/docstring] to all public functions in `[file]`
2. Create usage examples for top [N] use cases — examples MUST run
3. Add inline comments for non-obvious logic at `[file:lines]`
4. Update README with quick-start section

## Constraints
- ✅ Follow existing doc style: `[reference doc file]`
- ✅ Every example must compile/run without modification
- ❌ Don't document obvious getters/setters/constructors
- ❌ Don't duplicate information — single source of truth

## Verification
- [ ] Every public function has documentation
- [ ] All examples run: `[run command]`
- [ ] README has working quick-start section
```

---

## Usage

1. **Pick a template** that matches your scenario
2. **Scan codebase** using `codebase-analysis.md` to fill `[brackets]`
3. **Combine templates** when needed — Feature + Testing = complete prompt
4. **Adapt** — every project is unique, templates are starting points
