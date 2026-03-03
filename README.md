# Enhance Prompt ⚡

> An agentic AI skill that transforms raw, vague prompts into professional-grade, context-rich instructions — like having a prompt engineer on your team.

## How It Works

The moment you invoke `/enhance-prompt`, it doesn't just rewrite your words. It steps back and scans your codebase to understand what you're actually building.

It pulls your tech stack, dependencies, file structure, patterns, and constraints — then injects that real context into a structured, professional prompt.

Every enhanced prompt includes a before/after quality score (out of 35), risk assessment, difficulty estimate, and a clean copy-ready version.

## Installation

> Install once. Works across Claude Code, Cursor, Codex, and OpenCode.

### Claude Code (via Plugin Marketplace)

```
/plugin marketplace add VoDaiLocz/enhance-prompt
/plugin install enhance-prompt@enhance-prompt
```

### Cursor (via Plugin Marketplace)

In a Cursor Agent conversation:

```
/plugin-add enhance-prompt
```

### Codex

Tell Codex:

```
Fetch and follow instructions from https://raw.githubusercontent.com/VoDaiLocz/Enhance-Prompt/main/.codex/INSTALL.md
```

### OpenCode

Tell OpenCode:

```
Fetch and follow instructions from https://raw.githubusercontent.com/VoDaiLocz/Enhance-Prompt/main/.opencode/INSTALL.md
```

### Manual (Antigravity / Gemini)

```bash
cp -r skills/enhance-prompt/ ~/.gemini/antigravity/skills/enhance-prompt/
```

## Verify Installation

Start a new session and type:

```
/enhance-prompt Fix the login page
```

The agent will automatically invoke the skill, scan your codebase, and produce a professional enhanced prompt.

## Usage

```
/enhance-prompt <your raw prompt>
```

**Examples:**
```
/enhance-prompt Fix the bug in auth
/enhance-prompt Add caching to the API
/enhance-prompt Refactor the user service
/enhance-prompt optimize the database
```

## Example Output

**Raw prompt:** `Fix the bug in auth`

**Enhanced:**

```markdown
## Context
Next.js 14 App Router + TypeScript. Auth via `next-auth` v5 in `src/lib/auth.ts`.
Prisma adapter. Session breaks after form submit in `src/app/(auth)/login/page.tsx`.

## Task
1. Debug `signIn()` callback at `auth.config.ts:25`
2. Fix session persistence in `SessionProvider` wrapper
3. Verify redirect logic in `middleware.ts` callbacks

## Constraints
- ✅ Follow existing patterns in `src/middleware.ts`
- ✅ TDD: write failing test first
- ❌ Don't modify Prisma schema

## Verification
- [ ] Valid login → redirects to `/dashboard`
- [ ] Invalid login → shows error toast
- [ ] Session persists after page refresh
```

**Score: 6/35 → 34/35**

## What's Inside

### Enhancement Framework

- **7-Layer Enhancement** — Clarity → Specificity → Context → Structure → Constraints → Output Format → Verification
- **HARD-GATE** — codebase scan is mandatory, no exceptions
- **Iron Law** — No enhanced prompt without codebase context
- **RED FLAG guards** — per-layer checklist to catch incomplete enhancements

### Codebase Analysis

- **L1** — Project overview (package.json, tsconfig, .env.example)
- **L2** — Architecture scan (imports, naming, routing patterns)
- **L2.5** — Monorepo detection (Turborepo, Nx, Lerna, PNPM workspaces)
- **L2.5** — Framework detection (Next.js App/Pages Router, FastAPI, Django, Express, NestJS)
- **L3** — Deep scan (function signatures, types, test patterns)

### Output Format

Every enhanced prompt includes:

| Section | Description |
|---------|-------------|
| 📊 Enhancement Summary | Before/After score table (7 dimensions, /35) |
| 🔴 Original Prompt | The raw input |
| 🟢 Enhanced Prompt | Context + Task + Constraints + Output + Verification |
| ⏱️ Difficulty Estimate | Complexity, time, risk, files affected |
| ⚠️ Risk Assessment | High/Medium/Low risks with mitigation |
| 🔀 Alternative Approaches | Options with pros/cons |
| 📋 Copy-Ready Prompt | Clean version, paste anywhere |

### Prompt Library — 12 Templates

| # | Template | Use Case |
|---|----------|----------|
| 1 | 🐛 Bug Fix | Debugging with root cause investigation |
| 2 | ✨ New Feature | Adding functionality with TDD |
| 3 | ⚡ Performance | Optimization with measurable targets |
| 4 | 🔄 Refactor | Structural improvements, zero behavior change |
| 5 | 🔒 Security Audit | OWASP Top 10 scanning |
| 6 | 📝 Documentation | JSDoc, README, inline comments |
| 7 | 🧪 Testing | Unit, integration, coverage targets |
| 8 | 🎨 UI/Styling | Components, responsive, WCAG accessible |
| 9 | 🔌 API Integration | External services with retry/backoff |
| 10 | 🚀 DevOps | CI/CD, deployment, health checks |
| 11 | 🗃️ Database | Migrations, reversible, indexed |
| 12 | 🔍 Deep Scan | Root cause analysis, null/async/security bug hunting |

## Philosophy

- **Evidence over guessing** — scan the codebase, don't assume the tech stack
- **Specificity beats length** — `src/auth/login.ts:42` > paragraph of description
- **Systematic over ad-hoc** — 7-layer framework, not feel-good rewrites
- **Prove improvement** — scoring table shows the enhancement worked

## File Structure

```
.claude-plugin/
├── plugin.json              # Claude Code plugin manifest
└── marketplace.json         # Claude Code marketplace config

.cursor-plugin/
└── plugin.json              # Cursor plugin manifest

.codex/
└── INSTALL.md               # Codex installation guide

.opencode/
└── INSTALL.md               # OpenCode installation guide

commands/
└── enhance-prompt.md        # /enhance-prompt slash command

skills/enhance-prompt/
├── SKILL.md                 # Main skill orchestrator
└── references/
    ├── prompt-patterns.md   # 7-Layer Enhancement Framework
    ├── codebase-analysis.md # Multi-level codebase scanning
    ├── output-format.md     # Structured output template
    ├── prompt-library.md    # 6 core prompt templates
    └── prompt-library-extended.md  # 5 extended templates

docs/
└── INSTALL.md               # Platform-specific install guide

RELEASE-NOTES.md
```

## Contributing

1. Fork this repository
2. Create a branch for your improvement
3. Follow the skill format in `skills/enhance-prompt/SKILL.md`
4. Submit a PR

## License

MIT
