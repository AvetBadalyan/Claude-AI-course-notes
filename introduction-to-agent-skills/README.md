[⬅ Back to course index](../README.md)

# 📚 Introduction to Agent Skills — Course Notes

> Builds on [Claude Code 101](../claude-code-101/README.md) (Ch 10 "Skills") and [Claude Code in Action](../claude-code-in-action/README.md) (Ch 3 "Verification Skills"). This course is the dedicated deep dive: what skills are, creating one, multi-file skills, how they compare to other features, sharing, and troubleshooting.

### 🗺️ Course Map

| Unit | Chapters | Status |
|------|----------|:------:|
| 🗂️ **Course Overview** | [Ch 1: What Are Skills?](#chapter-1-what-are-skills) · Ch 2: Creating Your First Skill · Ch 3: Configuration and Multi-File Skills · Ch 4: Skills vs. Other Claude Code Features · Ch 5: Sharing Skills · Ch 6: Troubleshooting Skills | 🚧 |
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
