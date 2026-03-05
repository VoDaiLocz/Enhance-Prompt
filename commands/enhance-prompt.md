# Enhance Prompt Workflow

> **Workflow:** `/enhance-prompt`
> **Description:** Enhance and refine prompts to professional-grade instructions before executing them.

## 1. Intake and Scoring (`enhance-prompt/SKILL.md`)
- Ask user for the raw prompt they want to enhance (or use the one provided after the command).
- Score the prompt across 7 dimensions: Clarity, Specificity, Context, Structure, Constraints, Output Format, Verification.
- Identify the gaps based on the `prompt-patterns.md` criteria.

## 2. Auto-Category Detection (`enhance-prompt/references/auto-detection.md`)
- Extract keywords and intent signals from the raw prompt.
- Match against the signal table to identify the primary category.
- If confidence is low, ask 1 clarifying question about the intent.
- If multi-intent detected (2+ categories), proceed to Prompt Chain Decomposition.

## 3. Prompt Chain Decomposition (`enhance-prompt/references/prompt-chain.md`)
- If multi-intent detected: decompose into focused sub-prompts (max 4).
- Order sub-prompts by dependency priority (investigate → fix → secure → build → optimize → test → document → deploy).
- Link context forward between sub-prompts.
- If single-intent: skip this step and proceed to Codebase Scan.

## 4. Codebase Scan (`enhance-prompt/references/codebase-analysis.md`)
- Execute the Level 1 Project Overview scan (directories, package.json).
- If monorepo indicator exists, execute the Level 2.5 Monorepo Detection scan.
- If the prompt touches existing components, execute the Level 3 Deep Scan.
- Collect the context output for the next step.

## 5. Ambiguity Check
- Based on the codebase scan and the raw prompt, are there any *critical* ambiguities?
- If yes, ASK the user 1-2 targeted questions before proceeding. Do NOT ask more than 2 questions.
- If no, or after user response, proceed to enhancement.

## 6. Enhancement (`enhance-prompt/references/prompt-patterns.md`)
- Apply the 7-Layer Enhancement framework.
- Inject the context gathered from step 4.
- Use the auto-detected template from step 2 (or chain templates from step 3).
- Choose from `enhance-prompt/references/prompt-library.md` or `enhance-prompt/references/prompt-library-extended.md`.

## 7. Formatting and Presentation (`enhance-prompt/references/output-format.md`)
- Format the final output strictly matching the Enhanced Prompt Output Format.
- Generate the Before/After scoring table.
- Include the Risk Assessment and Difficulty Estimate.
- Provide the Copy-Ready Prompt at the bottom.
- Conclude by asking if the user wants this prompt to be directly executed.

## 8. Iteration (`enhance-prompt/references/iteration-mode.md`)
- If the user requests refinement, apply targeted changes (not full rewrite).
- Re-score after each iteration, showing delta from previous version.
- Max 3 iterations — if not converged, re-analyze from scratch.
- Track version history: v1 → v2 → v3.
