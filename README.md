# skills

A collection of agent skills I've built for **Claude Code** and **Codex** — each lives in its own
repository and is indexed here as a git submodule. They share the same `SKILL.md` format, so any
SKILL.md-aware runtime (Claude Code, Codex, custom harnesses) picks them up once they're in its
skills directory.

## Skills

| Skill | What it does | Repo |
| ----- | ------------ | ---- |
| **explanimate** | Animated, React-based visual explainers — SVG + Tailwind diagram scenes and motion-graphics videos as real code (Motion + Remotion). | [notpritam/explanimate](https://github.com/notpritam/explanimate) |
| **claude-canvas** | Interactive diagrams on a real tldraw canvas in your browser via `/visualize`. Ships a pre-built bundle. | [notpritam/claude-canvas](https://github.com/notpritam/claude-canvas) |
| **daylog** | Mirrors the current Claude session into your Obsidian vault — daily note, project rollup, full session record, weekly one-liner. | [notpritam/daylog](https://github.com/notpritam/daylog) |

## Install the whole collection

```bash
git clone --recurse-submodules https://github.com/notpritam/skills.git
cd skills
# already cloned without --recurse-submodules?
git submodule update --init --recursive
```

Then link the skills you want into your agent's skills directory:

```bash
# Claude Code (user scope — all projects)
ln -s "$PWD/explanimate"   ~/.claude/skills/explanimate
ln -s "$PWD/claude-canvas" ~/.claude/skills/claude-canvas
ln -s "$PWD/daylog"        ~/.claude/skills/daylog

# Codex — same SKILL.md format, just a different directory
ln -s "$PWD/explanimate"   ~/.codex/skills/explanimate
```

Symlinks keep the skills updatable in place (`git submodule update --remote`). Prefer copies? Use
`cp -R` instead of `ln -s`.

## Or install one skill directly

Each skill is a standalone repo — you don't need this index to use just one:

```bash
git clone https://github.com/notpritam/explanimate.git ~/.claude/skills/explanimate
```

## Per-skill setup

- **explanimate** — docs + a Vite / React 19 / Remotion studio template. On first use the agent
  scaffolds a studio (`node explanimate/scripts/init.mjs`), then `pnpm install && pnpm exec
  playwright install chromium`. Requires Node ≥ 22, pnpm ≥ 9.
- **claude-canvas** — ships a pre-built bundle; nothing to install to use it. Requires Node 20+.
- **daylog** — pure skill scripts, no build. Needs the Obsidian MCP configured.

## Updating

```bash
git submodule update --remote --merge   # pull latest of every skill
git add -A && git commit -m "chore: bump skills"
```
