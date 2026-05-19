# Hakfa Agent Skills

This repository contains a specialized suite of agent skills for Hakfa (Hak-fa / 客家話) language processing and Roman Orthography conversion. These skills transform general AI agents (Claude, Gemini, etc.) into Hakfa-expert assistants.

## Skills Included

### Language & Orthography

*   **hakfa-roman-orthography-converter**: Expertise in converting Hakfa Roman Orthography across four systems — FHL dict (POJ-style 1–8 numeric), 長老教會 PFS (1–6 numeric + Unicode diacritics), KPPY / 教育部客家語拼音方案 (numeric + modifier-letter diacritics), and IPA (with Chao tone letters). Handles all Input ↔ Unicode and cross-system conversions, including PFS ↔ KPPY orthographic mapping.

### Reference

*   **hakfa-terminology-guide**: Enforces correct terminology for the Hakfa language and its writing systems — language naming (Hakfa / Hak-fa), Roman Orthography vs. "Romanization", PFS vs. KPPY distinctions, and the traditional 長老教會 PFS 1–6 tone numbering.

## Installation

### Claude (Claude Code)

#### Option 1: Plugin Install (Recommended)

Install the entire skill suite as a plugin directly from the repository:
```bash
/plugin install https://github.com/ThoivanHakfa/hakfa-agent-skills
```

Skills are namespaced automatically (e.g., `/hakfa-agent-skills:hakfa-roman-orthography-converter`). To update:
```bash
/plugin update hakfa-agent-skills
```

#### Option 2: User-Level (Global)

Install individual skills for all projects by copying them into your home directory:
```bash
cp -r hakfa-roman-orthography-converter/ ~/.claude/skills/hakfa-roman-orthography-converter/
```

#### Option 3: Project-Level

Install individual skills for a specific project by copying them into the project directory:
```bash
cp -r hakfa-roman-orthography-converter/ .claude/skills/hakfa-roman-orthography-converter/
```

#### Option 4: CLI Flags (Development / Testing)

Load the plugin from a local directory or remote archive without installing:
```bash
claude --plugin-dir ./hakfa-agent-skills
claude --plugin-url https://example.com/hakfa-agent-skills.zip
```

For Options 2 and 3, you can optionally reference the skills in your `CLAUDE.md`:
```markdown
I have Hakfa language skills in `.claude/skills/`.
Always refer to these for Roman Orthography conversion or Hakfa terminology tasks.
```

### Gemini CLI

#### Option 1: Install from Git (Recommended)

Install the entire skill suite directly from the repository:
```bash
gemini skills install https://github.com/ThoivanHakfa/hakfa-agent-skills.git --scope user
```

Install a single skill from the repo using `--path`:
```bash
gemini skills install https://github.com/ThoivanHakfa/hakfa-agent-skills.git --path hakfa-roman-orthography-converter --scope user
```

Use `--scope workspace` instead of `--scope user` to install for the current project only (stored in `.gemini/skills/`).

#### Option 2: Install from Local Directory

After cloning the repository:
```bash
gemini skills install ./hakfa-roman-orthography-converter --scope user
```

#### Option 3: Symlink for Development

For active skill development, use `link` so changes are reflected immediately:
```bash
gemini skills link ./hakfa-roman-orthography-converter --scope user
```

#### Option 4: Manual Placement

Copy skill directories directly to the Gemini skills directory:
```bash
cp -r hakfa-roman-orthography-converter/ ~/.gemini/skills/hakfa-roman-orthography-converter/
```

After any installation method, reload skills in your session:
```
/skills reload
```

### Cross-Agent Install

This project follows the open [Agent Skills](https://agentskills.io) standard (`SKILL.md`). You can use the cross-agent skills CLI to install for multiple agents at once.

**Global** (available in all projects — installs to `~/.agents/skills/` with symlinks to each agent):
```bash
cd ~ && npx skills install github.com/ThoivanHakfa/hakfa-agent-skills
```

**Project-level** (available only in the current project — installs to `.agents/skills/`):
```bash
npx skills install github.com/ThoivanHakfa/hakfa-agent-skills
```

This works with Claude Code, Gemini CLI, Codex CLI, and other compatible agents.

## Contributing

We welcome contributions! Please submit a pull request or open an issue to suggest improvements or add new skills.
