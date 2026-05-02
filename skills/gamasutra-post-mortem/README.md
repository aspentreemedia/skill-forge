# gamasutra-post-mortem

A Claude skill that generates a candid, technical project post-mortem in the style of [Game Developer Magazine](https://www.gamedeveloper.com) — the publication that popularized brutally honest retrospectives in the games industry. Works for any software project, not just games.

## What it does

Point this skill at a project after a sprint or milestone and it will:

- **Mine your git history** automatically using `git log` and `git diff` to surface what actually happened — not just what you remember
- **Generate two variants** from a single run:
  - **Internal** — includes commit hashes, repo names, and raw technical detail for your engineering team
  - **Public** — scrubbed of proprietary internals, suitable for a blog post, social media, or a magazine submission
- **Write both files** to a `Documents/` folder inside your project workspace

## Output structure

Each generated document contains:

1. **The Narrative Hook** — Historical context and how the scope evolved from the original brief
2. **Data Box** — Sprint stats (team size, duration, tools, repos)
3. **What Went Right** — Architectural wins, smart pivots, and well-timed restraint
4. **What Went Wrong** — Candid, technical failures — integration hell, regressions, scope creep
5. **Conclusion** — Future-proofing lessons and what this sprint unlocked
6. **If We Did It Again** — Concrete, numbered action items for the next sprint

## Usage

With the skill installed and enabled, just tell Claude:

> *"Write a post-mortem for this sprint"*  
> *"Generate a project retrospective"*  
> *"Wrap up this milestone with a post-mortem"*

Claude will ask for your `DEV_LOG.md` or any dev notes, then mine git history automatically before drafting both documents.

## Prerequisites

- A git repository (recommended — the skill mines commit history for raw material)
- A `DEV_LOG.md` or any dev notes / changelog (optional but improves output quality)
- Code Execution enabled in Claude Settings → Capabilities

## Example output

See [`examples/`](./examples/) for sample internal and public variants.

## Installation

### For Claude.ai

1. Download or clone this folder
2. In Claude, go to **Settings → Customize → Skills**
3. Click **"+"** or **"Upload a skill"** and select this folder
4. Toggle it **on**

### For Antigravity

Antigravity automatically detects skills in specific directories. To install this skill, move or symlink this folder into one of the following locations:

*   **Project-Level:** Create a `.agent/skills/` directory in your project root and place this folder inside.
    ```bash
    mkdir -p .agent/skills
    ln -s /path/to/gamasutra-post-mortem .agent/skills/
    ```
*   **Global:** Place this folder in your global Antigravity skills directory:
    `~/.gemini/antigravity/skills/`

Antigravity will index the skill automatically. You can verify it's active by checking the **Skills** tab in the sidebar.