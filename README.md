# Enhance Prompt ⚡

> An agentic AI skill that transforms raw, vague prompts into professional-grade, context-rich instructions — like having a prompt engineer on your team.

## What It Does

Takes any prompt (even a single word like "optimize") and enhances it through:

1. **7-Layer Enhancement Framework** — Clarity → Specificity → Context → Structure → Constraints → Output Format → Verification
2. **Codebase Analysis** — Auto-scans your project (tech stack, patterns, files) to inject real context
3. **Structured Output** — Every enhanced prompt follows the 4-section format: Context, Task, Constraints, Output
4. **Quality Scoring** — Before/after comparison with 7-dimension scorecard (score out of 35)
5. **Prompt Library** — 11 ready-to-use professional templates for common scenarios

## Quick Start

### Usage

Type `/enhance-prompt` followed by your raw prompt:

```
/enhance-prompt Fix the login page
/enhance-prompt Add caching to the API
/enhance-prompt Refactor the user service
```

### Example

**Before:**
> Fix the bug in auth

**After:**
> **Context:** Next.js 14 App Router + TypeScript. Auth via `next-auth` v5 in `src/lib/auth.ts`.
>
> **Task:**
> 1. Debug `signIn()` callback in `auth.config.ts:25`
> 2. Fix session persistence in `SessionProvider` wrapper
> 3. Verify redirect logic after login
>
> **Constraints:**
> - ✅ Follow existing patterns in `src/middleware.ts`
> - ❌ Don't modify Prisma schema
>
> **Verification:**
> - [ ] Valid login → redirects to `/dashboard`
> - [ ] Invalid login → shows error message
> - [ ] Session persists after refresh

## Installation

### For Antigravity / Gemini

Copy the `enhance-prompt/` folder to your skills directory:

```bash
cp -r enhance-prompt/ ~/.gemini/antigravity/skills/enhance-prompt/
```

### For Claude Code

Copy the `enhance-prompt/` folder to your project's `.claude/skills/`:

```bash
cp -r enhance-prompt/ .claude/skills/enhance-prompt/
```

### Slash Command (Optional)

Copy the workflow file so `/enhance-prompt` works as a slash command:

```bash
cp -r .agents/workflows/ your-project/.agents/workflows/
```

## File Structure

```
enhance-prompt/
├── SKILL.md                                    # Main skill (orchestrator)
└── references/
    ├── prompt-patterns.md                      # 7-Layer Enhancement Framework
    ├── codebase-analysis.md                    # Multi-level codebase scanning guide
    ├── output-format.md                        # Structured output template
    ├── prompt-library.md                       # 6 core prompt templates
    └── prompt-library-extended.md              # 5 extended prompt templates

.agents/workflows/
└── enhance-prompt.md                           # Slash command workflow
```

## Features

| Feature | Description |
|---------|-------------|
| **7-Layer Enhancement** | Systematic framework ensuring every prompt dimension is covered |
| **Codebase-Aware** | Auto-scans project structure, dependencies, and patterns |
| **Interactive Mode** | Asks 1-2 targeted questions when prompt is critically ambiguous |
| **Quality Scoring** | 7-dimension scorecard (Clarity, Specificity, Context, Structure, Constraints, Output, Verification) |
| **Multilingual** | Detects non-English prompts and produces bilingual output with English technical terms |
| **Monorepo Detection** | Recognizes Turborepo, Nx, Lerna, PNPM workspaces |
| **Framework Detection** | Auto-identifies Next.js, FastAPI, Django, Express, NestJS, React |
| **Difficulty Estimate** | Provides complexity, time, and risk estimates |
| **Risk Assessment** | Highlights potential risks with mitigation strategies |
| **Alternative Approaches** | Suggests multiple implementation paths with trade-offs |
| **Prompt Library** | 11 professional templates for common scenarios |
| **Copy-Ready Output** | Clean version ready to paste into any AI tool |

## Prompt Library Templates

| # | Template | Use Case |
|---|----------|----------|
| 1 | 🐛 Bug Fix | Debugging specific errors |
| 2 | ✨ New Feature | Adding functionality |
| 3 | ⚡ Performance | Optimization with metrics |
| 4 | 🔄 Refactor | Structural improvements |
| 5 | 🔒 Security Audit | OWASP vulnerability scanning |
| 6 | 📝 Documentation | API docs, inline comments |
| 7 | 🧪 Testing | Unit/integration tests |
| 8 | 🎨 UI/Styling | Components, responsive design |
| 9 | 🔌 API Integration | External service connections |
| 10 | 🚀 DevOps | CI/CD, deployment configs |
| 11 | 🗃️ Database | Migrations, schema changes |

## Built With

Inspired by [obra/superpowers](https://github.com/obra/superpowers) — an agentic skills framework & software development methodology.

## License

MIT
