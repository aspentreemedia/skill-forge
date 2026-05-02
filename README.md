# skill-forge

A collection of open-source skills for [Claude](https://claude.ai) [Antigravity](https://antigravity.ai) — reusable workflows that teach Agents how to handle specific tasks automatically.
 
## What are Skills?
 
Skills are modular instruction sets you upload to Claude once. After that, Claude reads them automatically whenever a task matches what the skill is designed for — no need to re-explain your workflow in every conversation.
 
## Available Skills
 
| Skill | Description |
|-------|-------------|
| [gamasutra-post-mortem](./skills/gamasutra-post-mortem/) | Generates a candid, technical post-mortem by mining git history and dev logs — produces both an internal and public/business variant as Markdown files. |
 
## Installation

### For Claude.ai

1. Download the skill folder you want (or clone this repo)
2. In Claude, go to **Settings → Customize → Skills**
3. Click **"+"** or **"Upload a skill"**
4. Select the skill folder (e.g. `gamasutra-post-mortem/`)
5. Toggle it **on**

That's it — Claude will automatically apply the skill when relevant, or you can invoke it explicitly by describing your task.

### For Antigravity

Antigravity automatically detects skills in specific directories. To install a skill, move or symlink the skill folder into one of the following locations:

*   **Project-Level:** Create a `.agent/skills/` directory in your project root and place the skill folder inside.
    ```bash
    mkdir -p .agent/skills
    ln -s /path/to/skill-forge/skills/gamasutra-post-mortem .agent/skills/
    ```
*   **Global:** Place the skill folder in your global Antigravity skills directory:
    `~/.gemini/antigravity/skills/`

Antigravity will index the skill automatically. You can verify it's active by checking the **Skills** tab in the sidebar.

 
> **Note:** Skills require a Pro, Max, Team, or Enterprise plan and Code Execution enabled in Settings → Capabilities.
 
## Contributing
 
Contributions are welcome! If you have a skill you'd like to share, please read [CONTRIBUTING.md](./CONTRIBUTING.md) before submitting a pull request.
 
## License
 
MIT
 