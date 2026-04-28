# Prompt2Agent

[![Website](https://img.shields.io/badge/site-prompt2agent.dev-black?style=flat-square)](https://prompt2agent.dev)
[![Agent Skills Compatible](https://img.shields.io/badge/agent--skills-compatible-22c55e?style=flat-square)](https://github.com/vercel-labs/skills)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg?style=flat-square)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/erwancodes/prompt2agent?style=flat-square)](https://github.com/erwancodes/prompt2agent/stargazers)

> One prompt. One `agent.md`. Three runtimes.

A universal skill for AI IDEs that turns `/Prompt2Agent <description>` into a complete, deploy-ready agent — system prompt, provider config, and integration code for **OpenAI**, **Anthropic** and **LangChain** — all written to a single reviewable file at the root of your repo.

No backend. No keys to configure. Your IDE's model reads the skill, asks itself the right questions, and emits the file.

---

## Feedback & Contributions

- Open an [issue](https://github.com/erwancodes/prompt2agent/issues) or a [PR](https://github.com/erwancodes/prompt2agent/pulls)
- DM [@erwancodes](https://github.com/erwancodes) on GitHub
- Email: `pro.erwantv@gmail.com`

---

## Installing

```bash
npx skills add erwancodes/prompt2agent
```

Works for every major AI coding agent — **Claude Code**, **Cursor**, **Codex**, **Windsurf**, **Copilot**, **Antigravity**, and 40+ more — via the [Agent Skills](https://github.com/vercel-labs/skills) standard. The CLI auto-detects your installed agents and symlinks the skill to the right folder.

For a **global install** across every project on your machine:

```bash
npx skills add erwancodes/prompt2agent -g
```

---

## Skills

| Skill | What it does |
|---|---|
| **prompt2agent** | Takes one line of natural language, asks itself the right questions about scope, persona, model choice and guardrails, then writes a complete `agent.md` you can commit and ship. |

> Coming in v0.2: `prompt2crew` (multi-agent CrewAI scaffolds), `prompt2eval` (auto-generated test sets for the agent you just built).

---

## How to use it

In your IDE, anywhere — chat, sidebar, command palette:

```
/Prompt2Agent A senior Python reviewer for pull requests in a Django monolith
```

The skill walks the model through **scope → persona → model → guardrails**, then writes `./agent.md` containing:

- A **system prompt** tuned to the task.
- **Provider config** (model, temperature, max_tokens) for OpenAI, Anthropic, LangChain.
- **Copy-paste integration code** in TypeScript and Python.
- A **first-message example** to test the agent.

Commit it. Version it. Ship it like any other source file.

---

## Settings

Open `skills/prompt2agent/SKILL.md` and tune these knobs at the top of the file. Each takes a value from `1` to `10`.

| Setting | What it controls | Default |
|---|---|---|
| `STRICTNESS` | How aggressively the agent enforces guardrails. Higher = more refusals, fewer hallucinations. | `7` |
| `DEPTH` | How deep the system prompt goes — short and punchy vs. long and exhaustive. | `5` |
| `OPINIONATION` | How much the skill picks for you (model, temperature, tools) vs. asks. | `8` |

> Sensible defaults work for 90% of cases. Touch these only if the generated agents feel off.

---

## Examples

Real prompts. Real `agent.md` files. Browse [`examples/`](./examples) for the full output.

| Prompt | Output |
|---|---|
| `/Prompt2Agent A friendly first-line support assistant for a SaaS product` | [`support-agent.md`](./examples/support-agent.md) |
| `/Prompt2Agent An assistant that reviews Python pull requests` | [`code-review-agent.md`](./examples/code-review-agent.md) |
| `/Prompt2Agent An SEO writer that drafts blog posts from a keyword list` | [`seo-agent.md`](./examples/seo-agent.md) |

---

## Manual install

If you don't want to use the `skills` CLI, drop `SKILL.md` directly into your IDE's skills folder:

```bash
# Claude Code (project-scoped)
curl -o .claude/skills/prompt2agent/SKILL.md \
  https://raw.githubusercontent.com/erwancodes/prompt2agent/main/skills/prompt2agent/SKILL.md

# Cursor
curl -o .cursor/rules/prompt2agent.md \
  https://raw.githubusercontent.com/erwancodes/prompt2agent/main/skills/prompt2agent/SKILL.md
```

Or paste the contents of `SKILL.md` straight into your ChatGPT / Claude system prompt — the skill works as a self-contained instruction set.

---

## Support the Project

If Prompt2Agent saved you an afternoon of prompt engineering, the easiest way to give back is to **star the repo** and tell one friend.

For sponsorship: [github.com/sponsors/erwancodes](https://github.com/sponsors/erwancodes) (coming soon).

---

## Common Questions

**How is this different from a snippet library or a ChatGPT prompt?**
A snippet hands you a generic system prompt. Prompt2Agent inspects your project (language, SDKs, framework), picks a model and temperature for the task, writes guardrails specific to the use case, and ships ready-to-paste code for three providers in one file you can commit.

**Does it work outside the official Agent Skills CLI?**
Yes — `SKILL.md` is plain Markdown. Manual install instructions above. You can also paste it into ChatGPT, Claude.ai, or any system-prompt field.

**Why a `SKILL.md` file?**
[Agent Skills](https://github.com/vercel-labs/skills) is the open standard for sharing reusable agent capabilities across IDEs. One file, every agent — no per-IDE bookkeeping.

**What providers are supported?**
OpenAI, Anthropic, LangChain in v0.1. CrewAI and AutoGen are on the v0.2 roadmap.

**Can I customise the generated agent?**
Yes — every section of `agent.md` is plain Markdown. Edit, version, refactor like any other source file.

---

## Roadmap

- **v0.1** — Skill + landing live at [prompt2agent.dev](https://prompt2agent.dev) ✅
- **v0.2** — CrewAI, AutoGen, prompt templates by category, `--framework` flag
- **v0.3** — `prompt2crew` (multi-agent), `prompt2eval` (auto test sets)

---

## License

MIT — see [LICENSE](./LICENSE).

---

*Built under [Helionis Labs](https://github.com/erwancodes) by [@erwancodes](https://github.com/erwancodes).*
