---
name: prompt2agent
description: Transform a short description into a complete, production-ready AI agent (system prompt, config, integration code for OpenAI, Anthropic and LangChain). Triggered by /Prompt2Agent <description>.
---

# Prompt2Agent Skill

Universal skill for AI IDEs (Claude Code, Cursor, Codex). Generates a complete AI agent from a single line: optimized system prompt, tuned config, and ready-to-paste integration code.

---

## Trigger

When the user types:

```
/Prompt2Agent <description of the agent>
```

…run the full procedure below and write the result to `agent.md` in the current working directory.

If `<description>` is empty, ask the user one short question to clarify the agent's role, then proceed.

---

## Procedure

You are an expert in AI agent architecture. From the user's description, produce a single `agent.md` file containing the sections defined below — in this exact order, with these exact headings.

### Step 1 — Detect project context

Before generating, quickly inspect the working directory:

- **Language:** look for `package.json` (JS/TS), `pyproject.toml` / `requirements.txt` (Python), `go.mod` (Go), etc.
- **Existing AI SDKs:** check dependencies for `openai`, `@anthropic-ai/sdk`, `anthropic`, `langchain`.
- **TypeScript vs JavaScript:** check `tsconfig.json`.

Use this to choose the most relevant code samples (e.g., TypeScript over JavaScript when `tsconfig.json` exists). When in doubt, default to **Python** for LangChain and **TypeScript** for OpenAI / Anthropic.

### Step 2 — Design the agent

Decide:

1. **Role** — one sentence, precise, action-oriented.
2. **Audience & context** — who talks to it, in what setting.
3. **Constraints** — what it must never do, scope limits, safety rules.
4. **Tone & style** — formal, casual, technical, concise, etc.
5. **Recommended tools** — only those that genuinely help the task (web search, code execution, file I/O, retrieval, etc.). If none, say "None".
6. **Model & sampling** — pick sensible defaults per provider:
   - Reasoning / coding heavy → larger model, `temperature: 0.2`.
   - Creative / writing → `temperature: 0.7–0.9`.
   - Customer-facing assistant → `temperature: 0.3–0.5`.
   - `max_tokens`: 1024 for short replies, 2048–4096 for long-form.

### Step 3 — Generate `agent.md`

Create (or overwrite) `agent.md` in the current working directory with the following structure. Fill every section. Keep code blocks copy-paste runnable.

````markdown
# <Agent Name>

> <One-line summary>

Generated with [Prompt2Agent](https://prompt2agent.dev).

---

## System Prompt

```
You are <role>.

<Context paragraph: who you serve, what environment you operate in.>

Responsibilities:
- <bullet 1>
- <bullet 2>
- <bullet 3>

Constraints:
- <hard rule 1>
- <hard rule 2>

Tone: <tone description>.
Output format: <format description>.
```

---

## Recommended Tools

- `<tool_name>` — <why it matters>
- …

(Or: "None — this agent works on text only.")

---

## Configuration

### OpenAI

```json
{
  "model": "gpt-4.1",
  "temperature": 0.3,
  "max_tokens": 2048,
  "top_p": 1
}
```

### Anthropic

```json
{
  "model": "claude-opus-4-7",
  "temperature": 0.3,
  "max_tokens": 2048
}
```

### LangChain

```json
{
  "provider": "anthropic",
  "model": "claude-opus-4-7",
  "temperature": 0.3,
  "max_tokens": 2048
}
```

---

## Integration Code

### OpenAI (TypeScript)

```ts
import OpenAI from "openai";

const client = new OpenAI();

const SYSTEM_PROMPT = `<paste the system prompt above>`;

export async function ask(userMessage: string) {
  const res = await client.chat.completions.create({
    model: "gpt-4.1",
    temperature: 0.3,
    max_tokens: 2048,
    messages: [
      { role: "system", content: SYSTEM_PROMPT },
      { role: "user", content: userMessage },
    ],
  });
  return res.choices[0].message.content;
}
```

### Anthropic (TypeScript)

```ts
import Anthropic from "@anthropic-ai/sdk";

const client = new Anthropic();

const SYSTEM_PROMPT = `<paste the system prompt above>`;

export async function ask(userMessage: string) {
  const res = await client.messages.create({
    model: "claude-opus-4-7",
    max_tokens: 2048,
    temperature: 0.3,
    system: SYSTEM_PROMPT,
    messages: [{ role: "user", content: userMessage }],
  });
  return res.content[0].type === "text" ? res.content[0].text : "";
}
```

### LangChain (Python)

```python
from langchain_anthropic import ChatAnthropic
from langchain_core.messages import SystemMessage, HumanMessage

SYSTEM_PROMPT = """<paste the system prompt above>"""

llm = ChatAnthropic(
    model="claude-opus-4-7",
    temperature=0.3,
    max_tokens=2048,
)

def ask(user_message: str) -> str:
    response = llm.invoke([
        SystemMessage(content=SYSTEM_PROMPT),
        HumanMessage(content=user_message),
    ])
    return response.content
```

---

## Example First Message

> <A realistic first user message that exercises the agent>

**Expected response shape:** <one sentence>.

---

## Notes

- Adjust `temperature` and `max_tokens` based on observed quality.
- Consider adding caching, retries, and observability before shipping.
- For tool use, see provider docs:
  - OpenAI: https://platform.openai.com/docs/guides/function-calling
  - Anthropic: https://docs.anthropic.com/en/docs/build-with-claude/tool-use
  - LangChain: https://python.langchain.com/docs/concepts/tools/
````

---

## Rules

- **Always create `agent.md`** at the project root, even if a file with that name exists (overwrite).
- **Pick concrete model names** — never write `<model>` placeholder. Defaults: `gpt-4.1`, `claude-opus-4-7`.
- **Match the project language** when offered a choice between TS and JS.
- **Keep the system prompt under ~200 words** unless the agent's complexity demands more.
- **Do not invent tools.** Only suggest ones whose purpose is obvious from the description.
- After writing the file, print one short confirmation message with the agent's name and the path to `agent.md`. Nothing else.
