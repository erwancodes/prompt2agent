# Prompt2Agent

> A universal skill for AI IDEs that turns `/Prompt2Agent <prompt>` into a complete, deploy-ready agent.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Site](https://img.shields.io/badge/site-prompt2agent.dev-black)](https://prompt2agent.dev)

Prompt2Agent is an open-source skill installable in one command for AI IDEs (Claude Code, Cursor, Codex). Once installed, type `/Prompt2Agent <description>` directly in your IDE and instantly get a complete AI agent: optimized system prompt, tuned config, and integration code for OpenAI, Anthropic, and LangChain.

No external API keys. No backend. Your IDE's AI does the work using the skill's instructions.

---

## Install

```bash
npx skills add https://github.com/erwancodes/prompt2agent
```

Powered by [`vercel-labs/skills`](https://github.com/vercel-labs/skills) — auto-detects your installed agents (Claude Code, Cursor, Codex, Windsurf, Copilot…) and symlinks the skill in the right folder. Use `-g` for global install.

## Use

```
/Prompt2Agent An assistant that helps developers review their Python code
```

The IDE's AI reads the skill, designs the agent, and writes a complete `agent.md` at the root of your project — system prompt, config per provider, and ready-to-paste integration code.

## What you get

- A structured **system prompt** with role, context, constraints, and tone.
- A **config block** per provider (OpenAI, Anthropic, LangChain) with model, temperature, and max_tokens.
- **Integration code** in TypeScript and Python.
- A **first-message example** to test the agent.

See [`examples/`](./examples) for sample outputs.

## Repo layout

```
prompt2agent/
├── skills/
│   └── prompt2agent/
│       └── SKILL.md           # The skill (loaded by `npx skills add`)
├── web/                       # Landing page (Vite + React + shadcn/ui) — NOT shipped
├── examples/                  # Sample agents
├── README.md
├── LICENSE
└── package.json
```

## Roadmap

- v0.1 — Skill + landing live at `prompt2agent.dev`
- v0.2 — CrewAI, AutoGen, prompt templates, `--framework` flag

## License

MIT — see [LICENSE](./LICENSE).

---

Built under [Helionis Labs](https://github.com/erwancodes) by [@erwancodes](https://github.com/erwancodes).
