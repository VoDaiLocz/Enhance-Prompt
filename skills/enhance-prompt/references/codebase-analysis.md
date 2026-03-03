# Codebase Analysis for Prompt Enhancement

> Non-negotiable. Every enhanced prompt MUST include codebase context.

<HARD-GATE>
Do NOT skip any scan level. If Level 1 finds a monorepo, Level 2.5 is MANDATORY.
If the prompt references specific files, Level 3 is MANDATORY.
</HARD-GATE>

---

## The Scanning Process

```dot
digraph scan {
    rankdir=TB;
    l1 [label="Level 1\nProject Overview", shape=box, style=filled, fillcolor="#ccffcc"];
    mono [label="Monorepo?", shape=diamond];
    l25 [label="Level 2.5\nMonorepo Detection", shape=box, style=filled, fillcolor="#ffffcc"];
    l2 [label="Level 2\nArchitecture Scan", shape=box];
    specific [label="Touches\nspecific files?", shape=diamond];
    l3 [label="Level 3\nDeep Scan", shape=box, style=filled, fillcolor="#ffcccc"];
    inject [label="Inject Context\ninto Prompt", shape=doublecircle];

    l1 -> mono;
    mono -> l25 [label="yes"];
    mono -> l2 [label="no"];
    l25 -> l2;
    l2 -> specific;
    specific -> l3 [label="yes"];
    specific -> inject [label="no"];
    l3 -> inject;
}
```

---

## Level 1: Project Overview (ALWAYS)

**Run these commands FIRST:**

```bash
# 1. Understand structure
list_dir → project root

# 2. Extract tech stack
view_file → package.json / pyproject.toml / Cargo.toml / go.mod

# 3. Check code style
view_file → tsconfig.json / .eslintrc / prettier.config (if exists)

# 4. Check services
view_file → .env.example / docker-compose.yml (if exists)
```

**Extract:**

| File | What to Extract |
|------|-----------------|
| `package.json` | Framework, dependencies, scripts |
| `tsconfig.json` | TypeScript config, module resolution |
| `README.md` | Project purpose, setup instructions |
| `.env.example` | External services, API keys needed |
| `docker-compose.yml` | Infrastructure, databases, services |

---

## Level 2: Architecture Scan

| What to Find | How | Why It Matters |
|-------------|-----|----------------|
| **Directory structure** | `list_dir` on `src/` | WHERE to create/modify files |
| **Import patterns** | `grep_search` for `import` | Module resolution style |
| **Naming conventions** | `find_by_name` for components | camelCase vs kebab-case vs PascalCase |
| **State management** | `grep_search` for store/context/redux | Which state solution |
| **Routing** | Scan `pages/` or `app/` dirs | File-based vs config-based |

---

## Level 2.5: Monorepo & Framework Detection

**Monorepo Indicators:**

| File | Monorepo Type | Action |
|------|--------------|--------|
| `turbo.json` | Turborepo | Scan `apps/`, `packages/` — identify target workspace |
| `nx.json` | Nx | Scan `libs/`, `apps/` — check project graph |
| `lerna.json` | Lerna | Scan `packages/` — check hoisting |
| `pnpm-workspace.yaml` | PNPM Workspaces | Read workspace config |
| Multiple `package.json` | Any monorepo | Root vs package-level config |

**Framework-Specific Scanning:**

| Framework | Detection | Key Files to Scan |
|-----------|-----------|-------------------|
| **Next.js App Router** | `app/` dir + `next.config` | `layout.tsx`, `page.tsx`, server actions |
| **Next.js Pages Router** | `pages/` dir | `_app.tsx`, `getServerSideProps` |
| **FastAPI** | `from fastapi` imports | Routers, Pydantic models |
| **Django** | `settings.py` + `urls.py` | Models, views, serializers |
| **Express/NestJS** | `express` / `@nestjs` in deps | Middleware, controllers |

**Workspace boundary detection:**
```
1. Find nearest package.json to the prompt's target
2. Check if monorepo → identify which workspace
3. Scope context to THAT workspace only
4. Include shared packages only if imported
```

---

## Level 3: Deep Scan (Specific files)

| What | How | Context Value |
|------|-----|---------------|
| **Function signatures** | `view_code_item` on target file | Exact params, return types |
| **Related tests** | `find_by_name` for `*.test.*` | Existing test patterns |
| **Type definitions** | `grep_search` for `interface` / `type` | Data shapes |
| **Error handling** | `grep_search` for `catch` / `throw` | Error strategy |
| **Similar implementations** | `grep_search` for similar features | Patterns to follow |

---

## Context Injection Template

After scanning, inject into the enhanced prompt:

```markdown
## Context

### Project
- **Type:** [Next.js 14 App Router / FastAPI / Express]
- **Language:** [TypeScript 5.3 / Python 3.12]
- **Package Manager:** [pnpm / npm / poetry]

### Relevant Files
- `[file-path]` — [purpose]

### Existing Patterns
- [Pattern found in codebase]

### Dependencies (relevant only)
- `[package]` v[version] — [what it does]

### Constraints from Codebase
- [e.g., "All routes use `authGuard` middleware"]
```

---

## Anti-Patterns — STOP If You Catch Yourself

| Anti-Pattern | Why It Fails | Fix |
|-------------|-------------|-----|
| Dumping entire file tree | Noise overwhelms signal | List relevant dirs only |
| Including all dependencies | Most are irrelevant | Only project-specific deps |
| Copying full file contents | Token waste | Extract relevant functions only |
| Guessing the tech stack | Wrong context = wrong output | ALWAYS verify from config |
| Skipping .env.example | Missing service dependencies | Always check env vars |
