---
name: gamasutra-post-mortem
description: Use this skill whenever the user wants to write a post-mortem, sprint retrospective, or project wrap-up document. Generates a candid, technical, Gamasutra-style post-mortem by mining git history and dev logs — producing both an internal (raw, commit-level detail) and public/business variant as Markdown files.
---

# Gamasutra-Style Post-Mortem Generator

This skill defines the structure and tone for creating a project post-mortem document. The goal is to produce a candid, highly technical reflection on the development process, focusing heavily on what was learned, what broke, and architectural decisions.

## Background: Gamasutra Post-Mortems

Gamasutra (now Game Developer Magazine) popularized the game development post-mortem format — a candid, structured retrospective written by developers immediately after shipping. The format is notable for its brutal honesty: developers publicly admit what went wrong, not just celebrate what went right. Classic examples include the post-mortems for Ultima Online, Myth, and Diablo. The tone is technical, first-person, and unapologetic.

This skill replicates that format for any software project — not just games.

## Workflow

When asked to generate a post-mortem, follow these steps:

1. **Source Context**: Ask the user for the path to their `DEV_LOG.md`, or look for any existing dev notes, changelogs, or README files in the project directory. Use whatever is available — the more raw material, the better.

2. **Mine the Git History**: Proactively run the following terminal commands in order to parse recent commit history. Commit messages often contain the most accurate, unfiltered reality of what broke, what was refactored, and what took the most effort.
   - `git log --oneline -n 50` — broad commit overview
   - `git diff HEAD~10` — recent change detail
   - `git log --all --grep="fix\|broke\|revert\|hack"` — surface pain points and workarounds
   
   If git is unavailable or the directory is not a repository, fall back to any changelog, README, or dev notes provided by the user. If none exist, ask the user to describe the major events of the sprint before continuing.

3. **Determine the Narrative**: Identify the primary "theme" of the sprint (e.g., "The Multi-Repo Rewrite", "The Migration to V6", "Infrastructure Modernization") based on the logs and notes.

4. **Draft the Documents (Dual Variants)**: You must explicitly generate **TWO** distinct versions of the post-mortem:
   - **The Internal Variant**: Rich with specific Git commit hashes, internal repository names, and exposing deeply technical workarounds. Intended for the engineering team.
   - **The Public/Business Variant**: Stripped of internal commit hashes, proprietary codebase nomenclature, repo names, internal tool names, and employee names. Replace specifics with generalizations (e.g., "our CI pipeline" not "Jenkins job XYZ"). Focuses on grand engineering concepts, pain points, and high-level architecture — suitable for an external magazine (like Gamasutra) or social media.

5. **Output Destination**: ALWAYS write the generated Markdown files to the `Documents/` directory **inside the current project workspace**. Create the `Documents/` directory if it does not already exist. Name files using the pattern `{project-name}-post-mortem-{variant}.md` (e.g., `my-app-post-mortem-internal.md`, `my-app-post-mortem-public.md`). **DO NOT** output to the global `~/Documents/` folder.

## Required Structure

Both variants must be Markdown files containing the following sections:

### 1. The Narrative Hook
A 2-3 paragraph introduction that sets the stage. It should include historical context, the initial brief (which usually sounds deceptively simple), and the reality of what the project actually became.

### 2. Data Box
A bulleted mechanical breakdown of the sprint. Infer these values from git history and logs where possible. Ask the user only for what cannot be determined programmatically (e.g., team size, platform targets).

* **Developer(s):** (e.g., 1 Person, Solo)
* **Development Time:** (e.g., < 1 Month)
* **Platforms/Targets:**
* **Repositories:**
* **Tools & Technologies:**

### 3. What Went Right (Top 3-5)
Focus on architectural wins, timesavers, brilliant pivots, or "restraint" (choosing *not* to do something). Titles should be catchy (e.g., "The Shared Infrastructure Win", "Owning the Marketing Engine"). Explain *why* it was a win.

### 4. What Went Wrong (Top 3-5)
This must be incredibly candid and technical. Do not sugarcoat failures. Focus on framework friction, "Integration Hell", cognitive overload, missing documentation, or UI regressions. Titles should reflect the pain (e.g., "The Serialization Trap", "The CSS Encapsulation Wars").

### 5. Conclusion
A brief summary of the value of the sprint, focusing on "future-proofing" and lessons learned for the next iteration.

### 6. If We Did It Again (Top 3 Recommendations)
Concrete, numbered action items for the next sprint. These should not be vague lessons — specify actual tooling, process, or architectural changes that would have prevented the problems identified in "What Went Wrong."

## Tone Guidelines
* **Candid & Gritty**: Speak from the perspective of a developer in the trenches.
* **Technicality**: Do not shy away from deep technical jargon (e.g., `display: inline` blockages, NGINX routing, serialization state mapping).
* **Self-Aware**: Acknowledge mistakes, miscalculations in scope, and "lazy" or brilliant workarounds.
* **Public Variant Restraint**: Strip repo names, internal tool names, commit hashes, and employee names. Replace with generalizations that preserve the engineering insight without exposing proprietary internals.