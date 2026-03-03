# Enhance Prompt Release Notes

## v1.0.1 (2026-03-03)

### Fixed

- **Symlink double-nesting** — Codex and OpenCode install guides now symlink to `skills/enhance-prompt/` instead of `skills/`, fixing unresolvable paths
- **Windows junction path** — PowerShell junction in Codex install guide corrected to point to `skills\enhance-prompt`
- **Claude plugin manifest** — Added missing `skills` and `commands` path references to `.claude-plugin/plugin.json`
- **Phantom file structure** — Removed non-existent `docs/INSTALL.md` from README file tree
- **Command file references** — `prompt-library.md` and `prompt-library-extended.md` now use full `enhance-prompt/references/` prefix in the workflow file
- **Platform-specific tool names** — Replaced Cursor-specific tool names (`list_dir`, `view_file`, `grep_search`, `find_by_name`, `view_code_item`) with platform-agnostic descriptions in codebase analysis

### Improved

- **Output efficiency rules** — Added token budget guidelines (150-700 words based on complexity) and anti-redundancy rules
- **Scoring accuracy gates** — Added gates to prevent inflated "After" scores (every 4-5 must be justified)
- **Mid-range scoring guidance** — Scoring table now includes score 3 (Adequate) descriptions to prevent score inflation
- **Conditional section rules** — Risk Assessment and Alternative Approaches are now skipped when not applicable
- **Enhanced example** — Complete example in output format now includes Enhancement Notes and Copy-Ready Prompt sections
- **Copy-Ready Prompt definition** — Clarified as clean extraction of Context/Task/Constraints/Output/Verification only
- **New red flags** — Added checks for redundancy across sections, inflated scores, subjective verification, over-verbose output, non-actionable constraints
- **Key principles** — Added "Score honestly" and "Output efficiency" to SKILL.md principles

## v1.0.0 (2026-03-03)

### Added

- **7-Layer Enhancement Framework** — systematic prompt improvement across 7 dimensions (Clarity, Specificity, Context, Structure, Constraints, Output Format, Verification)
- **Multi-level Codebase Scanning** — L1 (overview), L2 (architecture), L2.5 (monorepo + framework detection), L3 (deep scan)
- **HARD-GATE enforcement** — mandatory codebase scan before every enhancement
- **Iron Law** — "No enhanced prompt without codebase context"
- **Process Flow diagrams** — graphviz-style flow for enhancement and scanning workflows
- **Quality Scorecard** — Before/After scoring table (7 dimensions, /35 total)
- **Difficulty Estimate** — complexity, time, risk, and files-affected per enhancement
- **Risk Assessment** — High/Medium/Low risks with mitigation strategies
- **Alternative Approaches** — comparison table with pros/cons and recommended scenarios
- **13 Professional Templates** — Bug Fix, New Feature, Performance, Refactor, Security, Documentation, Testing, UI/Styling, API Integration, DevOps, Database, Deep Scan / Root Cause Analysis, Code Review
- **Multilingual Support** — detects non-English prompts, outputs bilingual enhanced prompt
- **Monorepo Detection** — Turborepo, Nx, Lerna, PNPM Workspaces
- **Framework Detection** — Next.js App Router/Pages, FastAPI, Django, Express, NestJS, React
- **Copy-Ready Output** — clean version ready to paste into any AI tool
- **Red Flags** — checklist to detect and fix incomplete enhancements
- **Common Rationalizations** — rebuttals to excuses for skipping the process
- **`/enhance-prompt` slash command** — works with Claude Code, Cursor, Codex, OpenCode
- **Plugin manifests** — Claude Code (`.claude-plugin/`), Cursor (`.cursor-plugin/`)
- **Install guides** — Codex (`.codex/INSTALL.md`), OpenCode (`.opencode/INSTALL.md`)
