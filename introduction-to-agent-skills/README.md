[⬅ Back to course index](../README.md)

# 📚 Introduction to Agent Skills — Course Notes

> Builds on [Claude Code 101](../claude-code-101/README.md) (Ch 10 "Skills") and [Claude Code in Action](../claude-code-in-action/README.md) (Ch 3 "Verification Skills"). This course is the dedicated deep dive: what skills are, creating one, multi-file skills, how they compare to other features, sharing, and troubleshooting.

### 🗺️ Course Map

| Unit | Chapters | Status |
|------|----------|:------:|
| 🗂️ **Course Overview** | [Ch 1: What Are Skills?](#chapter-1-what-are-skills) · [Ch 2: Creating Your First Skill](#chapter-2-creating-your-first-skill) · [Ch 3: Configuration and Multi-File Skills](#chapter-3-configuration-and-multi-file-skills) · Ch 4: Skills vs. Other Claude Code Features · Ch 5: Sharing Skills · Ch 6: Troubleshooting Skills | 🚧 |
| 🗂️ **Quiz** | Course quiz | 🔲 |

> **Annotation guide for these notes:** 📌 = my own reading from screenshots/context — **not stated in the lesson text itself**. 🔗 = my cross-reference between chapters — **my mapping, not the lesson's wording**. For exam prep, focus on the **📝 Quick Reference** tables and **Key features for exam** bullet lists at the end of each chapter.

---

> 🗂️ **Course Overview** · Chapter 1

## Chapter 1: What Are Skills?

> 🎬 **Video: What are skills? (3 min).** Skills are **reusable markdown files that teach Claude Code how to handle specific tasks automatically.** Instead of repeating instructions every time you ask Claude to review a PR or write a commit message, you **write a skill once** and Claude applies it whenever the task comes up.

### 🎯 Learning Objectives

- **Define** what Claude Code skills are and how they work
- **Explain** where skills live (personal vs. project directories)
- **Distinguish** between skills, CLAUDE.md, and slash commands
- **Identify** scenarios where skills are the right customization tool

### 🧠 Key Takeaways

- Skills are **folders of instructions, scripts, and resources** Claude Code can **discover and use**. Each skill lives in a **`SKILL.md`** file with a **`name`** and **`description`** in its frontmatter
- Claude uses the **`description` to match** skills to requests — it compares your request against available skill descriptions and **activates the ones that match**
- **Personal skills** → `~/.claude/skills` (follow you across all projects). **Project skills** → `.claude/skills` inside a repo (shared with anyone who clones it)
- Skills **load on demand** — unlike **CLAUDE.md** (loads into *every* conversation) or **slash commands** (require *explicit* invocation), skills **activate automatically** when Claude recognizes the situation
- **Rule of thumb:** if you find yourself **explaining the same thing repeatedly**, that's a skill waiting to be written

---

### 📦 What Skills Are

Skills are **folders of instructions, scripts, and resources** that Claude Code can discover and use to handle tasks **more accurately and efficiently.** Each skill lives in a **`SKILL.md`** file with a **`name` and `description`** in its frontmatter.

- **The `description` is how Claude decides whether to use the skill.** When you ask Claude to review a PR, it **reads your request, compares it to all available skill descriptions, and activates the ones that match.**

Example frontmatter:

```yaml
---
name: pr-review
description: Reviews pull requests for code quality. Use when reviewing PRs or checking code changes.
---
```

> Below the frontmatter, you write the **actual instructions** — your review checklist, formatting preferences, or whatever Claude needs for that task.

![VS Code showing .claude/skills/pr-review/SKILL.md with name "pr-review" and a description, then instructions ("When reviewing code in this FastAPI project, check for: Code Quality, FastAPI Specific…"); the explorer shows .claude/skills with commit-message and pr-review skills](assets/L1-what-are-skills/skill-md-frontmatter.png)

> 📌 *From the screenshot:* the skill lives at **`.claude/skills/pr-review/SKILL.md`** (one folder per skill), and the body is a structured checklist (`## Code Quality`, `## FastAPI Specific`) with items like *readability, consistent patterns, no hardcoded secrets, Pydantic schemas* — i.e. the "actual instructions" below the frontmatter. A sibling **`commit-message`** skill shows multiple skills coexisting (my reading).

#### 🔎 Matching in action

When Claude matches a skill to your request, **you'll see it load in the terminal.**

![Claude Code terminal: user asks "Can you review the pull request on branch sg-221?"; Claude shows "Skill(pr-review) Successfully loaded skill", then "I'll review the pull request on branch sg-221. Let me first gather information about the changes."](assets/L1-what-are-skills/skill-loading-terminal.png)

> 📌 *From the screenshot:* a plain request — *"Can you review the pull request on branch sg-221?"* — triggers **`Skill(pr-review) · Successfully loaded skill`** with **no slash command typed.** That's the automatic, description-based matching in action (my reading).

---

### 📍 Where Skills Live

| Scope | Location | Who gets it |
|-------|----------|-------------|
| 👤 **Personal** | **`~/.claude/skills`** (home directory) | **Follows you across all your projects** — e.g. your commit-message style, documentation format, how you like code explained |
| 📁 **Project** | **`.claude/skills`** inside the repo root | **Anyone who clones the repo gets them automatically** — team standards like brand guidelines, preferred fonts/colors |

- On **Windows**, personal skills live in **`C:/Users/<your-user>/.claude/skills`**.
- **Project skills get committed to version control** alongside your code, so the whole team shares them.

> 🔗 Same locations as [Claude Code 101, Ch 10](../claude-code-101/README.md) and the `.claude/skills` sharing point from [Claude Code in Action, Ch 3](../claude-code-in-action/README.md) (my mapping).

---

### 🆚 Skills vs. CLAUDE.md vs. Slash Commands

Skills are unique because they're **automatic and task-specific.**

| Feature | When it loads | Invocation |
|---------|---------------|------------|
| 📋 **CLAUDE.md** | Into **every conversation** | Always on (e.g. "always use TypeScript strict mode" goes here) |
| 🧰 **Skill** | **On demand, when it matches your request** | **Automatic** — Claude loads only the **name + description** initially, so it **doesn't fill the context window**; the body loads when you actually ask |
| ⌨️ **Slash command** | When you **type it** | **Explicit** — you invoke it yourself |

> 💡 **Why on-demand matters:** your PR-review checklist doesn't need to be in context when you're debugging — **it loads only when you actually ask for a review.**

![Illustration: a crab between two documents, SKILL.md (with a colored frontmatter line) on the left and CLAUDE.md on the right](assets/L1-what-are-skills/skill-vs-claude-md.png)

> 🔗 This is the three-surfaces idea from [Claude Code in Action, Ch 3](../claude-code-in-action/README.md) (CLAUDE.md = always-on conventions · Skills = task procedures · Hooks = can't-be-skipped) — here focused on the **loading difference** (my mapping).

---

### 🎯 When to Use Skills

Skills work best for **specialized knowledge that applies to specific tasks:**

| Use case |
|----------|
| 🔍 **Code review standards** your team follows |
| ✍️ **Commit message formats** you prefer |
| 🎨 **Brand guidelines** for your organization |
| 📄 **Documentation templates** for specific types of docs |
| 🐛 **Debugging checklists** for particular frameworks |

> 📏 **The rule of thumb:** if you find yourself **explaining the same thing to Claude repeatedly**, that's a skill waiting to be written.

> 🔗 Same "typed it twice → make it a skill" rule as [Claude Code in Action, Ch 3](../claude-code-in-action/README.md).

---

### 🔁 Recap

A **skill is a markdown file (`SKILL.md`) that teaches Claude how to do something once**, and Claude **applies that knowledge automatically whenever it's relevant.** Skills live **personally** (`~/.claude/skills`) or **per-project** (`.claude/skills`), match by **description**, and **load on demand** — keeping your context window free until the task comes up.

### 📝 Quick Reference: What Are Skills? (for exam prep)

| Concept | Key point |
|---------|-----------|
| 📦 **Skill** | A **folder** with a **`SKILL.md`** (frontmatter: **`name`** + **`description`**) + instructions |
| 🎯 **Matching** | Claude compares your request to each skill's **`description`** and activates matches |
| 👤 **Personal** | `~/.claude/skills` — follows you across all projects (Windows: `C:/Users/<user>/.claude/skills`) |
| 📁 **Project** | `.claude/skills` in the repo — committed to version control, shared with everyone who clones |
| ⏳ **Load on demand** | Only **name + description** load up front; the **body loads when it matches** → no context bloat |
| 🆚 **vs CLAUDE.md** | CLAUDE.md loads into **every** conversation; skills load **only when relevant** |
| 🆚 **vs slash commands** | Slash commands need **explicit typing**; skills activate **automatically** |
| 📏 **When to use** | Task-specific specialized knowledge — review standards, commit formats, brand guidelines, doc templates, debug checklists |

> 🎓 **Memory tip:** **"Write once, match by description, load on demand."** Locations: **`~/.claude/skills` = personal (travels with you)**, **`.claude/skills` = project (travels with the repo)**. The three surfaces by *loading*: **CLAUDE.md = always · Skill = auto-when-relevant · Slash command = explicit.**

**Key features for exam:**
- A skill = a **folder with a `SKILL.md`** whose frontmatter has a **`name`** and **`description`**; the body holds the instructions.
- Claude **matches skills by their `description`** against your request and **activates automatically** — no slash command needed.
- **Personal skills** → `~/.claude/skills` (all projects); **project skills** → `.claude/skills` (committed, shared with the repo).
- Skills **load on demand** (only name + description up front), unlike **CLAUDE.md** (every conversation) and **slash commands** (explicit invocation).
- **Rule of thumb:** repeating the same explanation → write a skill. Best for review standards, commit formats, brand guidelines, doc templates, debug checklists.

---

> 🗂️ **Course Overview** · Chapter 2

## Chapter 2: Creating Your First Skill

> 🎬 **Video: Creating your first skill (4 min).** Build a skill **from scratch** — a **personal PR-description skill** that works across all your projects. See how to structure the `SKILL.md`, test it, and understand how Claude Code **discovers and matches** skills behind the scenes, plus the **priority hierarchy** that decides which skill wins when names conflict.

### 🎯 Learning Objectives

- **Create** a skill from scratch with proper frontmatter structure
- **Test and verify** that a skill loads correctly in Claude Code
- **Explain** how Claude Code matches incoming requests to available skills
- **Describe** the skill **priority hierarchy** (Enterprise → Personal → Project → Plugins)

### 🧠 Key Takeaways

- A skill is a **directory** containing a **`SKILL.md`** with **metadata (`name`, `description`) in frontmatter** and **instructions below**
- Claude loads **only names + descriptions at startup**, then matches requests against those descriptions using **semantic matching**
- You get a **confirmation prompt** before Claude loads the **full skill content** into context
- **Priority for name conflicts:** **Enterprise → Personal → Project → Plugins**
- To **update** a skill, edit its `SKILL.md`; to **remove** one, delete its directory. **Always restart Claude Code** for changes to take effect

---

### 🏗️ Creating a Skill

We'll build a **personal** skill that teaches Claude to write PR descriptions in a consistent format. Being personal, it **lives in your home directory** and works **across all your projects.**

**Step 1 — make a directory** inside the skills folder; **the directory name should match the skill name:**

```bash
mkdir -p ~/.claude/skills/pr-description
```

**Step 2 — create `SKILL.md`** inside it, with two parts separated by frontmatter dashes:

```markdown
---
name: pr-description
description: Writes pull request descriptions. Use when creating a PR, writing a PR, or when the user asks to summarize changes for a pull request.
---

When writing a PR description:

1. Run `git diff main...HEAD` to see all changes on this branch
2. Write a description following this format:

## What
One sentence explaining what this PR does.

## Why
Brief context on why this change is needed

## Changes
- Bullet points of specific changes made
- Group related changes together
- Mention any files deleted or renamed
```

| Part | Role |
|------|------|
| **`name`** | **Identifies** your skill |
| **`description`** | Tells Claude **when to use it** — this is the **matching criteria** |
| **Everything after the second `---`** | The **instructions** Claude follows when the skill is activated |

![VS Code editing ~/.claude/skills/pr-description/SKILL.md — the body below frontmatter with "When writing a PR description:", the git diff step, and the ## What / ## Why / ## Changes template; the Skills explorer shows commit-message, debugging, documentation, and pr-description](assets/L2-creating-your-first-skill/pr-description-skill-md.png)

> 📌 *From the screenshot:* the Skills sidebar shows this skill sitting alongside **commit-message, debugging, and documentation** skills, and the output panel reads *"Loading configuration… Done loading configuration"* (my reading).

---

### 🧪 Testing Your Skill

Claude Code **loads skills at startup**, so **restart your session** after creating one. Verify it's available by checking the **available skills list** — you should see `pr-description` listed.

![An "Available Skills" terminal panel listing Skill: documentation / debugging / pr-description ("Write pull request descriptions and summarize changes") / commit-message, with a note "You can invoke these with a slash command like /commit or /debugging, or ask me to use them directly"; footer shows "IDE disconnected"](assets/L2-creating-your-first-skill/available-skills-list.png)

- To test: make some changes on a branch and say *"write a PR description for my changes."* Claude **indicates it's using the pr-description skill**, checks your diff, and writes a description following your template — **same format every time.**

> 📌 *From the screenshot:* the panel confirms skills can be invoked **either** by a slash command (`/commit`, `/debugging`) **or** by asking Claude directly — matching the automatic-vs-explicit distinction from [Chapter 1](#chapter-1-what-are-skills). It also shows each skill's description is what's loaded at this stage, not the body (my reading).

---

### 🔎 How Skill Matching Works

When Claude Code **starts**, it scans **four locations** for skills but loads **only the name and description — not the full content.** (This matters for the priority rules below.)

| Step | What happens |
|------|--------------|
| 1️⃣ **Startup scan** | Scans four locations, loads **only name + description** of each skill |
| 2️⃣ **Request** | Claude compares your message against **all available skill descriptions** (semantic matching) |
| 3️⃣ **Match** | e.g. *"explain what this function does"* matches a skill described as *"explain code with visual diagrams"* — the **intent overlaps** |
| 4️⃣ **Confirm** | Claude **asks you to confirm loading** the skill (keeps you aware of what context it's pulling in) |
| 5️⃣ **Execute** | After you confirm, Claude **reads the complete `SKILL.md`** and follows its instructions |

![A hand-drawn crab beside a SKILL.md frontmatter (name: backend-review, description: "Reviews backend code for security issues and compliance mishaps.") with a prompt "Use backend-review Skill?"](assets/L2-creating-your-first-skill/skill-confirmation-prompt.png)

> 📌 *From the screenshot:* the confirmation reads **"Use backend-review Skill?"** — the step 4 prompt in action, shown with a `backend-review` skill whose descriptive name avoids conflicts (the naming tip below) (my reading).

---

### 🏆 Skill Priority

If you clone a repo with a skill named the same as one of your personal skills — **which wins?** There's a clear order:

| # | Scope | Location | Priority |
|---|-------|----------|:--------:|
| 1 | 🏢 **Enterprise** | Managed settings | **Highest** |
| 2 | 👤 **Personal** | `~/.claude/skills` (home directory) | ↓ |
| 3 | 📁 **Project** | `.claude/skills` inside a repo | ↓ |
| 4 | 🧩 **Plugins** | Installed plugins | **Lowest** |

- This lets organizations **enforce standards** via enterprise skills while still allowing **individual customization.** If your company has an enterprise `code-review` and you make a personal `code-review` with the same name, **the enterprise version takes precedence.**
- ✅ **To avoid conflicts, use descriptive names** — instead of `review`, use `frontend-review` or `backend-review`.

> 🎓 **Order mnemonic:** **E-P-P-P** → **E**nterprise > **P**ersonal > **P**roject > **P**lugins (enterprise always wins; plugins always lose).

> 📌 **Beyond the course (not on the exam):** the course teaches **Enterprise → Personal → Project → Plugins**, and the [Claude Academy course page](https://academy.claude.com/courses/introduction-to-agent-skills/creating-your-first-skill) confirms this wording — **learn this order for the exam.** In the live product, the **Personal-vs-Project** relationship has since gained nuance (some docs describe project skills overriding personal ones, configurable via a `skillOverrides` setting). Ignore that for exam prep; just know the course's order.

---

### 🔄 Updating and Removing Skills

| Action | How |
|--------|-----|
| ✏️ **Update** | Edit its **`SKILL.md`** file |
| 🗑️ **Remove** | Delete its **directory** |
| 🔁 **Apply changes** | **Restart Claude Code** after any change |

> ⚠️ **Always restart Claude Code** — skills are loaded at startup, so edits and deletions don't take effect until you do.

---

### 🔁 Recap

Creating a skill means making a **directory with a `SKILL.md`** containing **metadata + instructions.** Claude loads **names and descriptions at startup**, **matches** incoming requests against those descriptions, and **asks for confirmation** before loading the full content. **Priority rules** handle name conflicts — **Enterprise overrides Personal overrides Project overrides Plugins** — and you **restart Claude Code** for any change to take effect.

### 📝 Quick Reference: Creating Your First Skill (for exam prep)

| Concept | Key point |
|---------|-----------|
| 🏗️ **Create** | `mkdir -p ~/.claude/skills/<name>` (dir name = skill name), then add a **`SKILL.md`** |
| 📄 **Structure** | Frontmatter (`name`, `description`) between `---` dashes · instructions below the second `---` |
| 🎯 **`description`** | The **matching criteria** — how Claude decides when to use the skill |
| 🧪 **Test** | **Restart** → check the **available skills list** → make a request that matches |
| 🔎 **Matching** | Startup loads **only name + description** (4 locations) → semantic match → **confirm** → read full `SKILL.md` |
| 🏆 **Priority** | **Enterprise → Personal → Project → Plugins** (enterprise wins, plugins lose) |
| 🏷️ **Avoid conflicts** | Use **descriptive names** (`frontend-review`, not `review`) |
| 🔄 **Update / remove** | Edit `SKILL.md` / delete the directory — **restart Claude Code** either way |

> 🎓 **Memory tip:** **"Make a dir, write SKILL.md, restart."** Matching = **scan names+descriptions → match → confirm → load body.** Conflicts = **E-P-P-P** (Enterprise > Personal > Project > Plugins).

**Key features for exam:**
- A skill = a **directory with a `SKILL.md`** (frontmatter `name` + `description`, instructions below); create via `mkdir -p ~/.claude/skills/<name>`.
- Claude loads **only name + description at startup** from **four locations**, then **semantically matches** requests to descriptions.
- Claude shows a **confirmation prompt** before loading the **full skill body** into context.
- **Priority for name conflicts: Enterprise → Personal → Project → Plugins** (enterprise highest, plugins lowest).
- **Avoid conflicts** with descriptive names (`backend-review`, not `review`).
- **Update** = edit `SKILL.md`; **remove** = delete the directory; **always restart Claude Code** for changes to take effect.

---

> 🗂️ **Course Overview** · Chapter 3

## Chapter 3: Configuration and Multi-File Skills

> 🎬 **Video: Configuration and multi-file skills (4 min).** The advanced techniques that make skills more powerful: the full set of **metadata fields**, how to write **descriptions that trigger reliably**, **restricting tool access** for security-sensitive workflows, and **organizing larger skills** across multiple files using **progressive disclosure.**

### 🎯 Learning Objectives

- Configure advanced skill metadata — **`allowed-tools`** and **`model`**
- Write effective **descriptions** that reliably trigger on the right requests
- Use **`allowed-tools`** to restrict what Claude can do when a skill is active
- Organize complex skills with **progressive disclosure** and **multi-file structures**

### 🧠 Key Takeaways

- **`name`** and **`description`** are **required**; **`allowed-tools`** and **`model`** are **optional** but powerful
- A good **description** answers two questions: **What does the skill do?** and **When should Claude use it?**
- **`allowed-tools`** restricts which tools Claude can use while the skill is active — useful for **read-only / security-sensitive** workflows
- **Progressive disclosure:** keep `SKILL.md` **under 500 lines** and link to supporting files (**references, scripts, assets**) that Claude reads **only when needed**
- **Scripts execute without loading their contents** into context — only the **output** consumes tokens

---

### 🏷️ Skill Metadata Fields

The **agent skills open standard** supports several frontmatter fields. **Two are required, the rest optional:**

| Field | Required? | Purpose | Limits / notes |
|-------|:---------:|---------|----------------|
| **`name`** | ✅ | Identifies the skill | **Lowercase letters, numbers, hyphens only · max 64 chars · should match the directory name** |
| **`description`** | ✅ | Tells Claude **when to use it** (matching) | **Max 1,024 chars** · the **most important field** |
| **`allowed-tools`** | ⬜ | **Restricts** which tools Claude can use when the skill is active | Omit = no restriction |
| **`model`** | ⬜ | Specifies **which Claude model** the skill uses | e.g. `sonnet` |

> 📌 **Beyond the course (not on the exam):** the course says *"two are required."* The live [Claude Academy course page](https://academy.claude.com/courses/introduction-to-agent-skills/configuration-and-multi-file-skills) now notes that in **Claude Code specifically, all fields are technically optional and only `description` is *recommended*** (and Claude Code adds its own fields like `model`). For the exam, go with the course's rule: **`name` + `description` required.**

---

### ✍️ Writing Effective Descriptions

**Be explicit.** If someone told you *"your job is to help with docs,"* you wouldn't know what to do — Claude thinks the same way.

A good description answers **two questions:**

| Question |
|----------|
| ❓ **What does the skill do?** |
| ❓ **When should Claude use it?** |

> 💡 **If your skill isn't triggering** when you expect, **add more keywords that match how you actually phrase your requests.** The description is what Claude uses to decide relevance, so the **language matters.**

---

### 🔒 Restricting Tools with `allowed-tools`

Sometimes you want a skill that can **only read files, not modify them** — for **security-sensitive workflows, read-only tasks, or guardrails.**

```yaml
---
name: codebase-onboarding
description: Helps new developers understand how the system works.
allowed-tools: Read, Grep, Glob, Bash
model: sonnet
---
```

![VS Code showing .claude/skills/codebase-onboarding/SKILL.md frontmatter — name, description, allowed-tools: Read, Grep, Glob, Bash, model: sonnet — then "# Codebase Guide"](assets/L3-configuration-multi-file/allowed-tools-frontmatter.png)

| Behavior | |
|----------|--|
| ✅ **With `allowed-tools: Read, Grep, Glob, Bash`** | While the skill is active, Claude can **only use those tools, without asking permission** — **no editing, no writing** |
| ⬜ **Omit `allowed-tools` entirely** | **No restriction** — Claude uses its normal permission model |

> 🔗 This is a skill-level version of the tool-restriction idea — compare the `allowedTools` option in the Agent SDK and GitHub Action ([Claude Code in Action, Ch 6 & 7](../claude-code-in-action/README.md)) (my mapping).

---

### 🪜 Progressive Disclosure

Skills **share Claude's context window** with your conversation. When Claude activates a skill, it **loads the `SKILL.md` into context.** But sometimes you need references, examples, or utility scripts.

⚠️ **Cramming everything into one 2,000-line file** has two problems: it **eats context window space** and it's **not fun to maintain.**

**Progressive disclosure solves this:** keep **essential instructions in `SKILL.md`** and put **detailed reference material in separate files** Claude reads **only when needed.**

The open standard suggests organizing the skill directory with:

| Folder | Holds |
|--------|-------|
| 📜 **`scripts/`** | Executable code |
| 📚 **`references/`** | Additional documentation |
| 🎨 **`assets/`** | Images, templates, or other data files |

Then in `SKILL.md`, **link to the supporting files** with clear instructions about **when to load them:**

![VS Code SKILL.md for codebase-onboarding showing "## Progressive Disclosure Levels" — Level 2: Architecture Overview with "Only load when user requests more detail. See architecture-guide.md (references/…)" and Level 3: Deep Dives with "Only load when user requests a specific topic. See deep-dive-guide.md"; explorer shows assets, references, scripts folders](assets/L3-configuration-multi-file/progressive-disclosure-levels.png)

> In this example Claude reads **`architecture-guide.md` only when someone asks about system design.** If they're asking *where to add a component*, it **never loads** that file. It's like having a **table of contents in the context window** rather than the entire document.

> 📏 **Rule of thumb:** keep **`SKILL.md` under 500 lines.** Exceeding that → consider splitting into reference files.

> 📌 *From the screenshot:* the body uses explicit **"Level 2 / Level 3"** headings each gated by **"Only load when user requests…"**, with the `references/`, `scripts/`, and `assets/` folders in the explorer — the multi-file layout in practice (my reading).

---

### ⚙️ Using Scripts Efficiently

**Scripts in your skill directory can run without loading their contents into context.** The script **executes and only the output consumes tokens.**

> 🔑 **The key instruction to include in `SKILL.md`: tell Claude to *run* the script, not *read* it.**

Particularly useful for:

| Use case |
|----------|
| ✅ **Environment validation** |
| 🔄 **Data transformations** that need to be consistent |
| 🧪 **Operations more reliable as tested code** than generated code |

> 🔗 Same "scripts are executed, not loaded" point as [Claude Code in Action, Ch 3](../claude-code-in-action/README.md) — here framed as a token-efficiency technique (my mapping).

---

### 🔁 Recap

Skills support metadata fields: **`name`** and **`description`** (required), **`allowed-tools`** (restricts available tools), and **`model`** (which Claude to use). Descriptions need **specific actions and trigger phrases** to match reliably. For larger skills, use **progressive disclosure** — keep `SKILL.md` **under 500 lines** and link to supporting files that **load only when needed**. **Scripts execute without loading their contents**, keeping context efficient.

### 📝 Quick Reference: Configuration and Multi-File Skills (for exam prep)

| Field / concept | Key point |
|-----------------|-----------|
| 🏷️ **`name`** (required) | Lowercase + numbers + hyphens · **max 64 chars** · matches directory name |
| 📝 **`description`** (required) | **Max 1,024 chars** · the matching criteria · answer **what + when** |
| 🔒 **`allowed-tools`** (optional) | Restricts tools while active (e.g. `Read, Grep, Glob, Bash`) — read-only/security; **omit = no restriction** |
| 🧠 **`model`** (optional) | Which Claude model the skill uses (e.g. `sonnet`) |
| ✍️ **Good description** | Specific actions + **trigger keywords** matching how you phrase requests |
| 🪜 **Progressive disclosure** | `SKILL.md` **< 500 lines**; link to **`references/` · `scripts/` · `assets/`** loaded only when needed |
| ⚙️ **Scripts** | **Run, don't read** — only the **output** uses tokens (env validation, consistent transforms, tested code) |

> 🎓 **Memory tip:** required = **N-D** (**N**ame, **D**escription), optional = **A-M** (**A**llowed-tools, **M**odel). Limits: **name ≤ 64, description ≤ 1024.** Big skills: **< 500 lines + progressive disclosure**; scripts = **run, don't read.**

**Key features for exam:**
- Frontmatter fields: **`name`** + **`description`** required; **`allowed-tools`** + **`model`** optional.
- **`name`** ≤ 64 chars (lowercase/numbers/hyphens, matches dir); **`description`** ≤ 1,024 chars and is the **matching criteria**.
- A good **description** answers **what the skill does** and **when to use it**; add **trigger keywords** if it under-triggers.
- **`allowed-tools`** restricts tools while the skill is active (read-only/security); **omit = normal permission model**.
- **Progressive disclosure:** keep `SKILL.md` **under 500 lines**, split depth into **`references/`, `scripts/`, `assets/`** loaded only when needed.
- **Scripts execute without loading their contents** — only output uses tokens; tell Claude to **run, not read** them.
