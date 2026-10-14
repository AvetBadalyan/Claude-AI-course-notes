[⬅ Back to course index](../README.md)

# 📚 Claude Code 101 — Course Notes

> Builds on [Claude 101](../claude-101/README.md) (Chapter 4 "Building software with Claude Code" and Chapter 12 "Other ways to work with Claude").

---

## Chapter 1: What is Claude Code?

> Claude Code is an **agentic coding tool** that understands your codebase, edits your files, runs commands, and integrates with your existing developer tools to help you get things done faster.

### 🧠 Key Takeaways

- **Claude Code is an agentic coding tool** — it reads your codebase, edits your files, runs commands, and connects to external tools to help you ship faster
- **The key differentiator is that it works as an AI Agent** — unlike Claude.ai, it has direct access to your files, your terminal, and your entire codebase, so instead of copy-pasting code back and forth, it goes in and does the work itself
- **An agent = an LLM operating in a loop in real time**, with access to tools, external services, or even other AI agents
- **Three concepts for using it effectively:** the **context window** (working memory), **permissions** (it asks before acting), and **mistakes** (it isn't perfect — stay in the loop)

### 💻 Where You Can Use Claude Code

Claude Code is available in:

| Surface | Notes |
|---------|-------|
| ⌨️ **Terminal** | The command-line experience (the screenshots in this chapter are from the terminal) |
| 🟦 **Visual Studio Code** | Inside the VS Code editor |
| 🧠 **JetBrains IDEs** | Inside JetBrains IDEs |
| 🖥️ **Claude Desktop app** | The **Code tab** — see [Claude 101, Chapter 4](../claude-101/README.md) |
| 🌐 **Web** | claude.ai/code |

> 💡 [Claude 101, Chapter 12](../claude-101/README.md) also lists browser and Slack (via **Claude Tag**) as places Claude Code can work.

### 🆚 What Separates Claude Code from Claude?

| | 🌐 **Claude.ai** | 💻 **Claude Code** |
|---|---|---|
| **Access** | Only what you paste or upload into the chat | **Direct access** to your files, terminal, and entire codebase |
| **Workflow** | You copy and paste code back and forth | It goes in and **does the work itself** |
| **Nature** | Conversational assistant | **AI Agent** |

### 🤖 What is an Agent?

> An **AI Agent** is software that can **interact with its environment** and **perform actions** to complete a defined goal.

At its core, an agent is a **large language model operating in a loop in real time**. Agents can have access to:
- 🛠️ **Tools**
- 🔌 **External services**
- 🤝 **Other AI agents**

#### 🔁 The Agent Loop

The lesson video shows the loop as simple pseudocode:

![The agent loop — while True: think, check if done, act, observe](assets/L1-what-is-claude-code/agent-loop-code.png)

```python
messages = [{"role": "user", "content": "What is (42 * 17) + (99 / 3)?"}]

while True:
    response = think(messages)                                      # 1. Think
    if done(response):                                              # 2. Done?
        print(get_text(response))
        break                                                       #    → Stop
    messages.append({"role": "assistant", "content": response.content})   # 3. Act
    messages.append({"role": "user", "content": act(response)})           # 4. Observe
```

| Step | What happens |
|------|---------------|
| 1️⃣ **Think** | The model looks at the conversation so far (`messages`) and decides what to do next |
| 2️⃣ **Done?** | If the goal is complete → print the answer and **stop** |
| 3️⃣ **Act** | If not, the model's response (e.g. a request to use a tool) is recorded and the action is carried out via `act(response)` |
| 4️⃣ **Observe** | The **result** of the action is added back into the conversation, and the loop starts again with that new information |

> 📌 **Illustrative walk-through** (my example, based on the screenshot's question): to answer *"(42 × 17) + (99 ÷ 3)"*, the agent might **think** it needs to calculate → **act** by running a tool → **observe** the result (747) → loop → **done**, print the answer.

#### 🤝 Agents Can Use Other Agents

The lesson says agents can have access to **other AI agents**. In the demo below, Claude Code is asked to *"Spawn the code reviewer subagent to review the code we last created"* — a separate `code-reviewer` agent is started to do that job.

![Claude Code spawning a code-reviewer subagent from the terminal](assets/L1-what-is-claude-code/subagent-code-reviewer.png)

> 📌 *Seen in the demo, not explained in this lesson:* `/remote-control` is shown as active (the session is reachable in the CLI or at a claude.ai/code session URL), and the footer shows `esc to interrupt`.

### 🛠️ What Can Claude Code Actually Do?

| Capability | What it means | Example |
|------------|---------------|---------|
| 📖 **Read and understand your codebase** | Explain a feature or trace a bug throughout your code | *"Explain how authentication works"* |
| ✏️ **Edit files across your project** | Refactor a function **and update every file that references it** | Rename a function everywhere it's used |
| ⌨️ **Run terminal commands** | Execute your build script, run tests, install packages — and **use the output to decide what to do next** | Run the test suite, read the failures, fix them |
| 🔎 **Search the web** | Look up documentation or the latest API references when needed | Check a library's current API |

#### 📖 Example: Reading & Understanding a Codebase

In this demo the user asks: *"I need to add webp conversion to our image upload pipeline. Figure out where in the pipeline it should happen, whether we need new dependencies and how to approach it."*

![Claude Code in plan mode running an Explore step — listing directories, grepping, and reading files](assets/L1-what-is-claude-code/explore-codebase-plan-mode.png)

What the screenshot shows:
- An **Explore** task (`Explore image upload pipeline`) runs a series of small, targeted tool calls:
  - `Bash(ls -la …/src/middleware/)` — list a folder
  - `Bash(ls -la … | grep -E "(uploads|data)")` — search for relevant folders
  - `Read(src/middleware/errorHandler.ts)` — read one specific file
  - `+13 more tool uses (ctrl+o to expand)`
- Claude is **locating answers strategically** instead of loading the whole project — this is the "agentic" behavior described under the context window below
- Footer: `plan mode on (shift+tab to cycle)`, `esc to interrupt`, `ctrl+b to run in background`, and `medium · /effort`

> 📌 *Plan mode and `/effort` appear in the demo but aren't explained in this lesson.*

### 🧭 Using Claude Code Effectively

Keep these **three concepts** in mind:

| # | Concept | What it means |
|---|---------|---------------|
| 1 | 🧠 **The context window** | Claude's **working memory** — it can hold a lot, but not everything at once |
| 2 | 🔐 **It asks for permission** | By default, Claude Code asks **before running commands or making changes**. You're always in control, hands-on or hands-off |
| 3 | ⚠️ **It can make mistakes** | It might misunderstand your intent, introduce a bug, or over-engineer a solution. **Staying in the loop** helps you catch these early |

#### 1️⃣ The Context Window

Think of it as Claude's working memory. This is where the "agentic" aspect comes in — Claude finds **strategic ways to locate answers** within your codebase **without loading the entire thing into context** (as in the Explore example above).

The `/context` command shows how the window is being used:

![The /context command — a grid showing system prompt, system tools, messages, free space, and autocompact buffer](assets/L1-what-is-claude-code/context-usage.png)

| Category (from the screenshot) | Tokens | % of window |
|--------------------------------|--------|-------------|
| **System prompt** | 2.9k | 1.4% |
| **System tools** | 14.6k | 7.3% |
| **Messages** | 1.3k | 0.7% |
| **Free space** | 136k | 68.1% |
| **Autocompact buffer** | 45.0k | 22.5% |
| **Total used** (model: `claude-haiku-4-5-20251001`) | **64k / 200k** | **32%** |

- The 64k total ≈ 2.9k + 14.6k + 1.3k + **45.0k** — so the autocompact buffer is counted in the used total
- Notice that **before you've typed much, tools and the system prompt already use space** — the window is a finite budget
- The tool also lists `SlashCommand Tool · 0 commands · Total: 864 tokens`

> 📌 *`/context` and the autocompact buffer are shown in the video but not explained in this lesson.*

#### 2️⃣ It Asks for Permission

By default, Claude Code **asks you before running commands or making changes**:

![Claude Code asking for approval before running an npx tsc --init command](assets/L1-what-is-claude-code/permission-prompt.png)

What the screenshot shows:
- Claude wants to run `npx tsc --init --rootDir src --outDir dist --esModuleInterop --strict` (description: *"Initialize TypeScript config"*)
- Message: **"This command requires approval"** — *"Do you want to proceed?"*

| Option | Meaning |
|--------|---------|
| **1. Yes** | Allow this one command |
| **2. Yes, and don't ask again for: `npx tsc:*`** | Allow it and similar commands going forward |
| **3. No** | Deny it |

Shortcuts shown: `Esc` to cancel · `Tab` to amend · `ctrl+e` to explain

> 🔗 Compare with the desktop Code tab settings from [Claude 101, Chapter 4](../claude-101/README.md): **Manually approve**, **Accept edits**, **Plan**.

#### 3️⃣ It Can Make Mistakes

Just like any tool, Claude Code isn't perfect. Watch for:
- ❌ Misunderstanding your intent
- 🐛 Introducing a bug
- 🏗️ Over-engineering a solution

> 💡 **Staying in the loop** — reviewing what it proposes and runs — helps you catch these early.

### 🔁 Recap

Claude Code is an **agentic coding tool**. It reads your codebase, edits your files, runs commands, and connects to external tools to help you ship faster. You can use it today in your **terminal, VS Code, JetBrains, and the Claude Desktop app**.

### 📝 Quick Reference: Claude Code Basics (for exam prep)

| Concept | Key point |
|---------|-----------|
| 💻 **Claude Code** | Agentic coding tool — reads codebase, edits files, runs commands, integrates with dev tools |
| 🤖 **AI Agent** | Software that interacts with its environment and performs actions to reach a goal |
| 🔁 **Agent core** | An **LLM operating in a loop** in real time (Think → Done? → Act → Observe) |
| 🧰 **Agents can access** | Tools · external services · other AI agents |
| 🧠 **Context window** | Claude's working memory — holds a lot, **not everything**; Claude searches strategically instead of loading the whole codebase |
| 🔐 **Permissions** | Asks **by default** before running commands or making changes |
| ⚠️ **Mistakes** | Can misunderstand intent, introduce bugs, or over-engineer — stay in the loop |

> 🎓 **Memory tip:** Claude Code = **Claude + hands** — an LLM in a **loop** (Think → Act → Observe) with access to your **files and terminal**

**Key features for exam:**
- **Key differentiator vs Claude.ai** = it works as an **AI Agent** with direct access to files, terminal, and codebase (no copy-paste)
- **Four capabilities:** read & understand code · edit files across the project · run terminal commands · search the web
- **Available in:** terminal, VS Code, Claude Desktop app, web, JetBrains IDEs
- **Three concepts:** context window · permission prompts (by default) · it can make mistakes

---

## Chapter 2: How Claude Code Works

> Claude Code is different from typical chat applications. Understanding how it works under the hood will help you use it more effectively.

### 🧠 Key Takeaways

- **The agentic loop** is the core of Claude Code: **gather context → take action → verify results**, repeated until the result is complete and verifiable
- **You stay in the loop** — you can add context, interrupt, or steer at any point
- **Context window** = how much conversation, file content, and command output Claude can hold; when the limit is reached, Claude Code **compacts** the conversation automatically
- **Tools** are the backbone of agents — they let Claude Code decide *when to execute code* instead of just returning text
- **Permission modes:** Default (asks for edits *and* commands) · Auto-accept (edits without asking, commands still need approval) · Plan mode (read-only, builds a plan first)

### 🔁 The Agentic Loop

![Agentic loop diagram — Your prompt flows into Gather context → Take action → Verify results, which loops back and ends in Done; you can interrupt, steer, or add context at any point](assets/L2-how-claude-code-works/agentic-loop-diagram.png)

| Step | What happens |
|------|---------------|
| 1️⃣ **You enter a prompt** | The loop starts with your request |
| 2️⃣ **Gather context** | Claude gets what it needs by interacting with the model, which returns **text or a tool call** that Claude Code can execute |
| 3️⃣ **Take action** | For example, **editing a file** or **running a command** |
| 4️⃣ **Verify results** | Claude checks whether the results achieve what your prompt set out to do |
| 5️⃣ **Done or repeat** | ✅ If yes → Claude **finishes and waits for the next prompt**. ❌ If no → it **loops back and tries again** until the results are complete and verifiable |

> 🙋 **Throughout the loop, you can add context, interrupt, or steer the model** to help guide it toward your goal (the orange box in the diagram).

> 🔗 **Same loop as Chapter 1, different labels** (my mapping): *Think* ≈ gather context (the model returns text or a tool call) · *Act* ≈ take action · *Done? / Observe* ≈ verify results.

#### 🔎 Example: One Pass Through the Loop

The user types: *"Can we create a simple test api with typescript?"*

![Claude Code reading a file, deciding the project is empty, and asking approval to run npm init -y](assets/L2-how-claude-code-works/permission-prompt-npm-init.png)

| Loop step | What the screenshot shows |
|-----------|----------------------------|
| **Prompt** | *"Can we create a simple test api with typescript?"* |
| **Gather context** | `Read 1 file (ctrl+o to expand)` — then Claude concludes: *"Empty project. I'll set up a simple Express API with TypeScript."* |
| **Take action** | `Bash(npm init -y)` — *"Initialize npm project"* |
| **Permission check** | *"This command requires approval"* — the loop **pauses until you decide** |

The approval options:

| Option | Meaning |
|--------|---------|
| **1. Yes** | Allow this one command |
| **2. Yes, and don't ask again for: `npm init:*`** | Allow it and matching commands going forward |
| **3. No** | Deny it |

Shortcuts shown: `Esc` to cancel · `Tab` to amend · `ctrl+e` to explain

> 🔗 Same prompt style as the `npx tsc --init` approval in Chapter 1 — this time for `npm init:*`.

### 🧠 Context

Claude has a **context window** that determines how much of your **conversation, file contents, command outputs, and more** it can store and reference.

**What happens at the limit:**
- Once you reach it, Claude Code **compacts** your conversation
- It **automatically determines what it can remove or summarize** to bring the context window back down to a usable size

> 🔗 In the `/context` screenshot from [Chapter 1](#chapter-1-what-is-claude-code), the **Autocompact buffer** row is most likely this mechanism (my inference — the lesson doesn't connect them explicitly).

### 🛠️ Tools

> **Tools are the backbone of how agents work.**

| | 💬 **Typical AI assistant** | 💻 **Claude Code** |
|---|---|---|
| **Input → Output** | Text in → text out | Can decide **when to execute code** to get closer to completing a task |
| **Capabilities** | Generates responses | Uses tools like a **file-reading tool**, a **web search tool**, or any number of other capabilities |

- Claude Code uses **semantic understanding** to determine **when to call a tool** and **how to use the output**

![A tools list from the course demo — Bash, Glob, Grep, Read, WebFetch, TodoWrite, WebSearch, BashOutput, Skill, SlashCommand, and mcp__ide__ tools](assets/L2-how-claude-code-works/agent-tools-list.png)

What the screenshot shows (a `tools:` line, apparently from an agent's configuration, next to a description about proactively suggesting a `code-quality-reviewer` agent after major code changes):

| Tool name | What the name suggests |
|-----------|-------------------------|
| `Read` | Read files |
| `Glob`, `Grep` | Find files / search inside files |
| `Bash`, `BashOutput` | Run shell commands / read their output |
| `WebFetch`, `WebSearch` | Fetch a web page / search the web |
| `TodoWrite` | Keep a task list |
| `Skill`, `SlashCommand` | Invoke skills / slash commands |
| `mcp__ide__getDiagnostics`, `mcp__ide__executeCode` | Tools exposed through an IDE connection (the `mcp__` prefix) |

> 📌 *This screenshot isn't explained in the lesson — the "what the name suggests" column is my reading of the tool names, not lesson content.*

### 🔐 Permissions

Claude Code has several **permission modes**:

| Mode | Behavior |
|------|----------|
| 🟡 **Default** | Claude asks for **explicit permission before editing a file or running a shell command** |
| 🟢 **Auto-accept** | **Files are edited without asking**, but **commands still require approval** |
| 🔵 **Plan mode** | Uses **read-only tools** to compile a **plan of action before starting any work** |

- All of this can be **configured in your settings file**

> 🔗 Related: [Claude 101, Chapter 4](../claude-101/README.md) lists the desktop Code tab settings *Manually approve / Accept edits / Plan* — they line up with Default / Auto-accept / Plan mode (my mapping).
> 🔗 The Chapter 1 plan-mode screenshot showed `plan mode on (shift+tab to cycle)` — that footer hint is how the demo switches modes.

> ⚠️ **Be cautious when skipping permissions.** Giving Claude Code free rein to run commands means **a mistake could be harder to catch before it happens.**

### 🔁 Recap

Claude Code combines several agentic concepts: an **agentic loop**, a **managed context window**, **tools**, and **configurable permissions** — all inside your terminal. It can **read your codebase, take action, and verify its own work**. That's what makes it fundamentally different from a chat window.

### 📝 Quick Reference: How Claude Code Works (for exam prep)

| Concept | Key point |
|---------|-----------|
| 🔁 **Agentic loop** | Gather context → Take action → Verify results → (repeat until complete and verifiable) |
| 🙋 **Your role** | Add context, interrupt, or steer at any point in the loop |
| 🧠 **Context window** | Holds conversation, file contents, command outputs; **auto-compacts** when full |
| 🛠️ **Tools** | Backbone of agents; Claude decides **when** to call a tool and **how** to use the output (semantic understanding) |
| 🟡 **Default mode** | Asks before editing files **and** running commands |
| 🟢 **Auto-accept** | Edits files without asking; **commands still need approval** |
| 🔵 **Plan mode** | **Read-only** tools to build a plan before any work |
| ⚙️ **Config** | Permissions are configurable in the **settings file** |

> 🎓 **Memory tip:** **L-C-T-P** — **L**oop · **C**ontext · **T**ools · **P**ermissions (the four agentic concepts of Claude Code)

**Key features for exam:**
- Loop ends only when results are **complete and verifiable**; failures **loop back and retry**
- **Context compaction** is automatic — Claude Code decides what to remove or summarize
- **Typical assistants:** text in → text out · **Claude Code:** can execute code via tools
- **Auto-accept ≠ fully autonomous** — commands still need approval
- **Plan mode = read-only** until the plan is made
- Skipping permissions makes mistakes **harder to catch before they happen**

---
<!-- Add new chapters below this line -->