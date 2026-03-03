# Enhance Prompt Workflow

> **Workflow:** `/enhance-prompt`
> **Description:** Enhance and refine prompts to professional-grade instructions before executing them.

## 1. Intake and Scoring (`enhance-prompt/SKILL.md`)
- Ask user for the raw prompt they want to enhance (or use the one provided after the command).
- Score the prompt across 7 dimensions: Clarity, Specificity, Context, Structure, Constraints, Output Format, Verification.
- Identify the gaps based on the `prompt-patterns.md` criteria.

## 2. Codebase Scan (`enhance-prompt/references/codebase-analysis.md`)
- Execute the Level 1 Project Overview scan (directories, package.json).
- If monorepo indicator exists, execute the Level 2.5 Monorepo Detection scan.
- If the prompt touches existing components, execute the Level 3 Deep Scan.
- Collect the context output for the next step.

## 3. Ambiguity Check
- Based on the codebase scan and the raw prompt, are there any *critical* ambiguities?
- If yes, ASK the user 1-2 targeted questions before proceeding. Do NOT ask more than 2 questions.
- If no, or after user response, proceed to enhancement.

## 4. Enhancement (`enhance-prompt/references/prompt-patterns.md`)
- Apply the 7-Layer Enhancement framework.
- Inject the context gathered from step 2.
- Choose an appropriate template from `prompt-library.md` or `prompt-library-extended.md` based on the intent.

## 5. Formatting and Presentation (`enhance-prompt/references/output-format.md`)
- Format the final output strictly matching the Enhanced Prompt Output Format.
- Generate the Before/After scoring table.
- Include the Risk Assessment and Difficulty Estimate.
- Provide the Copy-Ready Prompt at the bottom.
- Conclude by asking if the user wants this prompt to be directly executed.
