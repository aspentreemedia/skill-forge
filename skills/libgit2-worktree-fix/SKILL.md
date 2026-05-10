---
name: libgit2-worktree-fix
description: Fix unresponsive agents or Git errors like "core.repositoryformatversion does not support extension: worktreeconfig" caused by libgit2 incompatibility with Claude worktrees.
---

# Libgit2 WorktreeConfig Fix

## The Problem
If the Antigravity agent becomes completely unresponsive in a specific workspace, or if you encounter errors like:
`Error generating commit message: [unknown] core.repositoryformatversion does not support extension: worktreeconfig`

This happens because another tool (such as Claude Code) has automatically configured Git worktrees in your repository (e.g., creating a `.claude/worktrees` directory) and set `extensions.worktreeConfig = true` in your `.git/config`. 

Antigravity (along with many standard IDE features, like VS Code's built-in Git integration) relies on a C library called `libgit2` to read the Git repository. Currently, **`libgit2` strictly does not support the `worktreeConfig` extension**. When it encounters this setting, it throws a fatal error, which silently breaks the agent's ability to read the workspace state, making it appear entirely unresponsive.

## The Solution
To fix this and restore agent responsiveness immediately, you need to remove the unsupported extension flag and reset the repository format version back to standard.

Run the following commands in the root of your unresponsive workspace:

```bash
# 1. Remove the unsupported worktree configuration extension
git config --unset extensions.worktreeConfig

# 2. Reset the repository format version back to standard (0)
git config core.repositoryformatversion 0
```

## Why This Works
By unsetting `extensions.worktreeConfig`, `libgit2` can successfully parse the `.git/config` file again. Claude's worktrees generally continue to function fine without this strict configuration, but removing it completely unblocks Antigravity and any other `libgit2`-dependent IDE plugins.

You do not need to restart the agent or IDE after running these commands. Once executed, functionality like "Generate commit message" and general agent responsiveness will immediately return.
