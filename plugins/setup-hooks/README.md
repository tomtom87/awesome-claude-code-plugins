# setup-hooks

A Claude Code plugin that walks you through setting up hooks and a read-only subagent in your own project, one step at a time. Before each step it explains what the hook does, adapts it to your stack, then tests it with you by piping sample JSON into the script and showing the exit code.

## Install

In Claude Code:

```text
/plugin install setup-hooks --marketplace tomtom87/blog
```

On Claude Code older than 2.1.275, add the marketplace first:

```text
/plugin marketplace add tomtom87/blog
/plugin install setup-hooks@tomtom87-blog
```

Then, in the project you want hooks in:

```text
/setup-hooks
```

The scripts need [`jq`](https://jqlang.org) (`brew install jq`). The notification sounds use `afplay` and `osascript` on macOS; on Linux or Windows it rewrites them for your OS.

## What it sets up

1. Notifications: a different sound for "needs you", "finished" and "subagent finished".
2. Exit codes: why only exit 2 blocks.
3. The bouncer: a `PreToolUse` hook that blocks `.env` files, `rm -rf` and `--no-verify`, plus matching deny rules.
4. The instant check: format and lint the file Claude just edited.
5. The finish line: run your tests and build when Claude says it's done.
6. Context injection: a session-start briefing, and rules re-injected after compaction.
7. A read-only code-reviewer subagent.
8. Optional extras: a prompt hook, subagent briefings and checks, a gitleaks pre-commit hook, a GitHub required check.

It merges into your existing `.claude/settings.json` and never overwrites hooks or permissions you already have.

The full guide, with every script, is [HOOKS.md](https://github.com/tomtom87/blog/blob/v3.1/HOOKS.md).
