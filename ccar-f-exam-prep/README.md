[⬅ Back to course index](../README.md)

# 📚 CCAR-F Exam Prep — Scenario Notes

> **Source:** the 30 lessons at [aicertguides.com/learn](https://aicertguides.com/learn) (a third-party prep site, **not** Anthropic). It teaches the answers the **Exam Guide v1.0** expects. Where those differ from today's product, the notes give the **exam answer** and list the differences at the end.

> **Annotation guide:** 📌 = my own reading — **not stated in the lesson**. 🔗 = my cross-reference — **my mapping, not the lesson's wording**. For exam prep, focus on the **⚠️ Exam trap** lines and the closing cheat sheet.

## 🗺️ Exam at a Glance

**CCAR-F** · **60 questions** · **120 minutes** (about 2 min each) · pass mark **720 / 1000** · $125 · credential valid 12 months. Every question is a **scenario with 4 options**.

| Domain | Weight | Lessons |
|--------|:------:|:-------:|
| [D1: Agentic Architecture & Orchestration](#d1-agentic-architecture--orchestration-27) | **27%** | 7 |
| [D3: Claude Code Configuration & Workflows](#d3-claude-code-configuration--workflows-20) | **20%** | 6 |
| [D4: Prompt Engineering & Structured Output](#d4-prompt-engineering--structured-output-20) | **20%** | 6 |
| [D2: Tool Design & MCP Integration](#d2-tool-design--mcp-integration-18) | **18%** | 5 |
| [D5: Context Management & Reliability](#d5-context-management--reliability-15) | **15%** | 6 |

### 📖 Read This First: Every Lesson in One Plain Sentence

> 🔗 *My plain-English recap. If you remember only these, you still get most questions.*

| | Plain English |
|---|---|
| **1.1** | The loop keeps going while `stop_reason` says `tool_use`, and stops at `end_turn`. |
| **1.2** | One boss agent (coordinator) talks to all helpers. Helpers never talk to each other. |
| **1.3** | The boss must pass helpers **everything they need**, with sources attached. |
| **1.4** | Money, security or legal rules are enforced by **code**, because prompts sometimes fail. |
| **1.5** | **Pre**ToolUse can stop an action. **Post**ToolUse only tidies the result afterwards. |
| **1.6** | Too many items in one pass makes Claude sloppy. Do **one pass per item, then one pass across all**. |
| **1.7** | Files changed → start fresh with a summary. Nothing changed → resume. Comparing options → fork. |
| **2.1** | Wrong tool chosen? **Write better tool descriptions first.** |
| **2.2** | Errors need a **type** and a "can I retry?" flag. "Found nothing" is **not** an error. |
| **2.3** | Give each agent **4-5 tools** for its job, not 18. |
| **2.4** | Team servers go in `.mcp.json`, personal ones in `~/.claude.json`. Use existing servers before building. |
| **2.5** | **Grep** searches inside files, **Glob** searches file names. Don't read the whole codebase first. |
| **3.1** | Team rules go in the **project** CLAUDE.md. The user-level one isn't shared. |
| **3.2** | Always-on rules go in CLAUDE.md. Occasional workflows go in a **skill**. Noisy output → `context: fork`. |
| **3.3** | Rules for one file type across many folders → `.claude/rules/` with `paths:`. |
| **3.4** | Unclear task with several approaches → **plan mode** first. Clear task → just do it. |
| **3.5** | Claude keeps misreading you? Show **before/after examples**. |
| **3.6** | In CI always add **`-p`**, or the job hangs. The reviewer must be a separate session. |
| **4.1** | Say **exactly** what to flag. Vague words like "be careful" don't work. |
| **4.2** | Inconsistent output? Add **2-4 examples with the reason** behind each. |
| **4.3** | A JSON schema fixes **format** mistakes, not **wrong values**. Make fields nullable so Claude doesn't invent data. |
| **4.4** | Retry with the **error message** when the data exists. If it's missing from the source, **send it to a human**. |
| **4.5** | Batch = cheap but slow. Use it only when **nobody is waiting**. |
| **4.6** | A reviewer who wrote the code agrees with itself. Use a **fresh** reviewer. |
| **5.1** | Summaries lose exact numbers. Keep a **facts block** that is never summarised. |
| **5.2** | Escalate when the customer **asks for a human**, or when no rule covers the case. Not because of mood or "confidence". |
| **5.3** | When a helper fails, report **what failed, what was tried, what was found**. Never pretend "no results". |
| **5.4** | Claude getting vague in a big repo? **Save notes to files** and use helpers. |
| **5.5** | "97% accurate" can hide a bad document type. **Check each type** before trusting automation. |
| **5.6** | Two sources disagree? Show **both numbers with source and date**. |

### 🕵️ Fake-Option Detector

Some wrong options name things that **don't exist** (like your `file.scan()`). **If an option uses a name not on this list, treat it as a red flag.** 📌 *It's a warning sign, not proof: the exam could mention a real feature these lessons don't cover.*

| Area | Names that are **real** (all from the lessons) |
|---|---|
| Agent loop | `stop_reason` with `"tool_use"` / `"end_turn"` · **Task** (alias **Agent**) tool · `allowedTools` · `--resume` · `fork_session` |
| Hooks | **PreToolUse** · **PostToolUse** |
| Tools / MCP | `isError` · `isRetryable` · `tool_choice` (`auto` / `any` / a named tool) · `.mcp.json` · `~/.claude.json` · `${VAR}` · `"type": "http"` |
| Built-in tools | **Read · Write · Edit · Bash · Grep · Glob** |
| Claude Code files | `CLAUDE.md` · `CLAUDE.local.md` · `.claude/rules/` with `paths:` · `.claude/skills/<name>/SKILL.md` · `.claude/commands/` · `@path` imports |
| Skill settings | `context: fork` · `allowed-tools` · `argument-hint` |
| Commands / flags | `/memory` · `/compact` · `/plan` · `claude --permission-mode plan` · **`-p`** · `--output-format json` · `--json-schema` · `--append-system-prompt` · `--system-prompt` |
| Output / API | `tool_use` with a JSON schema · `strict: true` · Message Batches API with `custom_id` · `cache_control` |

**Confirmed fake in the lessons:** a `--batch` flag · `CLAUDE_HEADLESS=true` · "run `/memory` to load the config" (it only **shows** what loaded).

### 🧭 How the Exam Thinks (7 rules that decide most questions)

> 🔗 *My summary of patterns repeated across lessons.*

1. **Money, security, compliance → code** (gate or hook), never "a stronger prompt" (1.4, 1.5).
2. **Cheapest fix that hits the root cause first**: better tool descriptions before classifiers or few-shot (2.1).
3. **Structural problems need structural fixes**, not a bigger context window or a better prompt (1.6, 4.6, 5.4).
4. **A reviewer must be independent**: a fresh instance or session, not the one that wrote the code (3.6, 4.6).
5. **Never hide a failure, a gap or a conflict**: structured errors, both values with sources, coverage notes (2.2, 5.3, 5.6).
6. **Don't trust raw confidence or aggregate accuracy**: calibrate and segment first (4.6, 5.2, 5.5).
7. **Shared setup lives in the project, personal setup in the user folder** (2.4, 3.1, 3.2).

---

## D1: Agentic Architecture & Orchestration (27%)

### 1.1 Agentic Loops

- An **agent** = Claude + tools + **your code** that keeps the exchange going. The **agentic loop** is **deterministic code**, not a prompt trick.
- **Loop:** send request → check **`stop_reason`** → run the requested tools → **append the results to history** → repeat.
- **`stop_reason`** decides: **`"tool_use"` → continue**, **`"end_turn"` → stop**. If tool results aren't appended, Claude never sees them.

| ❌ Wrong stop signal | Why it fails |
|---|---|
| Parsing text like "I'm done" | Ambiguous ("I've finished file 1" while still working) |
| **Iteration cap as the main stop** | Caps only guard against **runaway** loops, not early exits |
| Checking `content[0].type == "text"` | A response can hold **text + tool_use** together |

⚠️ **Exam trap:** a cap is fine as a **safeguard**, wrong as the **primary** stop. 🎓 **Tip:** *`stop_reason` decides, nothing else.*

### 1.2 Multi-Agent Orchestration

- **Hub-and-spoke:** one **coordinator** in the middle; **all communication goes through it**. Subagents **never talk to each other**.
- **Isolation:** a subagent knows **only what the coordinator puts in its prompt** (no shared memory or history).
- **Coordinator's 4 jobs:** pick subagents dynamically · **split the scope** with no overlap · **re-delegate** when gaps appear · **route all messages** (for visibility and error handling).

⚠️ **Exam traps:** a report **missing whole areas** → blame the **coordinator's decomposition**, not the subagents. Poor subagent output → check **what the coordinator passed in**. Direct subagent-to-subagent messaging is **always wrong**, even "for efficiency".

### 1.3 Subagent Invocation & Context Passing

- The coordinator spawns subagents with the **Task tool** (renamed **Agent** in Claude Code v2.1.63). **`"Task"` (or `"Agent"`) must be in `allowedTools`**, or it can't spawn any.
- **3 rules for passing context:** include the **complete findings** of earlier agents · use **structured data** that separates **content from metadata** (source URL, page, document name) · give **goals, not step-by-step procedures**.
- **Parallel spawning:** several Task calls in **one** coordinator response (lower latency than one by one).

⚠️ **Exam trap:** a synthesis agent gives **unsourced claims** → the coordinator **dropped the metadata**. The fix is **pass structured metadata**, not "give the synthesis agent web access".

### 1.4 Workflow Enforcement & Handoff

- **Prompt guidance** is probabilistic (works about 90-95%, never 100%). **Programmatic enforcement** (hooks, **prerequisite gates**) is deterministic.
- **Decision rule:** if one failure means **financial loss, a security breach or a compliance violation** → **programmatic**.

| Operation | Use |
|---|---|
| Refunds, payments, transfers | **Gate / hook** |
| Identity checks, access control | **Gate / hook** |
| AML and regulatory checks | **Gate / hook** |
| Formatting, style, output order | Prompt is fine |

- **Prerequisite gate:** `process_refund` returns an error until `get_customer` has returned a **verified customer ID** this session. The model can't skip it.
- **Multi-concern request** (return + address change + loyalty question): **decompose → investigate in parallel → one combined answer**. Never sequential in separate chats, never only the first item.
- **Handoff to a human** (they get **no transcript**, so it must stand alone) needs **5 fields**: **customer ID · conversation summary · root cause · refund amount (exact figure) · recommended action**.

⚠️ **Exam trap:** "stronger system prompt" or "few-shot examples of the right workflow" is **wrong** for money/security/compliance. They raise the odds, not to 100%.

### 1.5 Agent SDK Hooks

| Hook | Runs | Can block? | Use for |
|---|---|:---:|---|
| **PreToolUse** | **before** the tool | ✅ | **Policy enforcement** |
| **PostToolUse** | **after** the tool | ❌ (already done) | **Normalising results** |

- **PreToolUse examples:** block `process_refund` over **$500** → human · block `transfer_funds` until `aml_check` passes · block discounts over **20%** → manager queue.
- **PostToolUse example:** convert Unix timestamps → ISO 8601, numeric status codes → readable text, so the model sees **one consistent format**.

⚠️ **Exam trap:** PostToolUse **can't stop** an action, because it has **already happened**. To block, use **PreToolUse**. 🎓 **Tip:** *Pre = Prevent. Post = too late.*

### 1.6 Task Decomposition Strategies

| Pattern | Use when | Examples |
|---|---|---|
| **Fixed pipeline** (prompt chaining) | Steps are **known**, input is structured | Multi-file code review, extracting known fields |
| **Dynamic adaptive** | Scope is **open-ended or unknown** | Exploring a legacy codebase, debugging an unfamiliar system |

- **Attention dilution:** with too many items in **one pass**, early items get more attention than later ones.
- **Fix = multi-pass:** (1) a **per-item pass** for each file or document, (2) a **cross-item pass** for data flow, inconsistent patterns and dependencies.

⚠️ **Exam trap:** a **bigger context window** or a **better prompt** does **not** fix attention dilution. It's structural.

### 1.7 Session State & Resumption

| Situation | Use |
|---|---|
| Continuing, **nothing changed** | **`--resume`** (continue a named session) |
| Comparing **two approaches** from one baseline | **`fork_session`** (independent branches) |
| **Core files changed**, or history is cluttered | **Fresh start + injected summary** |

- **Stale context:** after files change, a resumed agent reasons from **old cached tool results** and gives contradictory advice. When files change, **re-analyse only the changed files**.

⚠️ **Exam traps:** "resume and ask it to re-read the changed files" is **not best**: the stale results are still in history. `fork_session` is for **divergent exploration**, not for stale context. Fresh start and re-reading **everything** wastes effort when only some files changed.

---

## D2: Tool Design & MCP Integration (18%)

### 2.1 Tool Interface Design

- **Tool descriptions are the main way Claude picks a tool.** "Retrieves customer information" is too vague and causes misrouting.
- **A good description has 5 parts:** what it **does** · expected **inputs** (types, formats, required/optional) · **example queries** · **edge cases and limits** · **boundaries** (when to use it versus similar tools).
- **Fix order for misrouting:** **1) expand descriptions** (cheap, big effect) → few-shot (adds tokens, misses the cause) → routing classifier (over-built) → consolidating tools (long-term, costly).
- Other fixes: **split** a generic tool into purpose-specific ones, **rename** confusingly similar tools, and **re-read the system prompt**: keyword-heavy instructions ("always check customer details first") can **override** good descriptions.

⚠️ **Exam trap:** descriptions fix a **small toolkit** with two similar tools. For a **huge toolkit** (18 tools vs 4-5), the fix is fewer tools per agent (see 2.3).

### 2.2 Structured Error Responses

- **Two layers:** **protocol errors** (malformed request, unknown tool; the model rarely sees them) and **tool execution errors** (**`isError: true`**; the model reasons about recovery).
- **Four categories** (the exam guide names them, the MCP spec does not):

| Category | `isRetryable` | Recovery |
|---|:---:|---|
| **Transient** (timeout, rate limit) | ✅ true | Resend the same call after a delay |
| **Validation** (bad input) | ❌ false | **Fix the input**, send a new call |
| **Business** (policy violation) | ❌ false | **Alternative path or escalate** |
| **Permission** (access denied) | ❌ false | Escalate / different credentials |

- **`isRetryable: false` ≠ "give up".** It means *this exact call won't work*; do something different.
- **Access failure** = tool **couldn't reach** the data (timeout, auth) → may retry. **Valid empty result** = tool **reached** the data and found nothing → **don't retry, that's the answer.** The tool must make the two look **different**.

⚠️ **Exam trap (most tested in D2):** an agent retries 3 times on an empty lookup → the tool **doesn't distinguish access failure from a valid empty result**.
📌 *The guide gives no `isRetryable` value for validation; `false` is the common convention.*

### 2.3 Tool Distribution & Tool Choice

- **Tool overload:** about **18 tools** in one agent hurts selection. Give each agent **4-5 tools for its role**.
- **Consolidate near-duplicates:** 19 transform tools → **one `transform_data`** with an `operation` parameter.
- **Constrain tools** (least privilege): replace `fetch_url` with `load_document`, which accepts only document URLs.
- **Scoped cross-role tool:** give a subagent a **small version of another role's tool** for frequent simple cases.

| `tool_choice` | Use when |
|---|---|
| **`"auto"`** (default) | Model may answer in text **or** call a tool |
| **`"any"`** | **Must call some tool**: guaranteed structured output, e.g. **unknown document type** with several schemas |
| **`{"type":"tool","name":"…"}`** | **Force one specific tool** as a mandatory first step |

⚠️ **Exam traps:** 85% of fact-checks are simple lookups that all go through the coordinator → add a **scoped `verify_fact` tool** (don't remove verification, don't add a cache). **Splitting tools across two MCP servers doesn't reduce the count**: the client still sees one flat list. Sharper descriptions don't fix 18-tool overload.

### 2.4 MCP Server Integration

| File | Scope | Use for |
|---|---|---|
| **`.mcp.json`** (project root) | **Team**, version-controlled | Team-wide servers |
| **`~/.claude.json`** (home) | **Personal**, not shared | Experimental servers |

- **`${VAR_NAME}`** in `.mcp.json` expands environment variables, so **credentials stay out of git**.
- **Remote server** needs **`"type": "http"` + `url`**. Without `type`, Claude Code treats it as a **local stdio** server (config error).
- **Build vs use:** check **community servers first** (Jira, GitHub, Slack exist). Build custom only for **team-specific needs** they can't meet.
- **MCP resources** give a **content catalogue upfront**, so fewer exploratory tool calls.

### 2.5 Built-in Tools

Six tools: **Read, Write, Edit, Bash, Grep, Glob.**

| Tool | Does |
|---|---|
| **Grep** | Searches file **contents**: function callers, imports, error strings |
| **Glob** | Matches file **paths**: test files, `.ts` files, config files |
| **Edit** | Replaces exact text; the anchor must be **unique** |
| **Read + Write** | Fallback when Edit **can't find a unique anchor** |

- **Exam answer for a failed Edit:** Edit first → **Read + Write** as the fallback. Never Read + Write by default.
- **Never read all files upfront.** Explore incrementally: **Grep** for entry points → **Read** and follow imports → **Grep again** for renamed or re-exported names (wrappers, barrel files).
- **Deprecated function question:** **Grep** callers → **Glob** their sibling test files (e.g. `OrderProcessor.test.*`) → **Grep again** for wrapper names.

⚠️ **Exam traps:** Glob can't find function callers (a path says nothing about contents). Don't start with Glob.

---

## D3: Claude Code Configuration & Workflows (20%)

### 3.1 CLAUDE.md Hierarchy

| Level | Location | Shared? |
|---|---|:---:|
| **User** | `~/.claude/CLAUDE.md` | ❌ personal, not in git |
| **Project** | `.claude/CLAUDE.md` or root `CLAUDE.md` | ✅ via git |
| **Directory** | `subdir/CLAUDE.md` | ✅ applies in that folder |

- Files are **concatenated**, not overridden. There is **no guaranteed winner** in a conflict. CLAUDE.md is **guidance**; for a rule that must **always** hold, use **`settings.json` or a hook**.
- **`@path`** imports split a big file, but **everything still loads** (no context saved). To save context, use **`.claude/rules/` with `paths:`** (3.3).
- **`CLAUDE.local.md`:** personal notes beside a CLAUDE.md, usually gitignored.
- **`/memory`** shows which memory files loaded (exam answer). It **doesn't load** anything.

⚠️ **Exam trap (favourite):** Developer A follows the conventions, new Developer B doesn't → the conventions are in A's **user-level** file. **Move them to project level.** "Run `/memory` to load the config" is wrong.

### 3.2 Custom Slash Commands & Skills

- **Skills and commands are one system.** `.claude/skills/<name>/SKILL.md` (**recommended**) and `.claude/commands/<name>.md` (flat file, still works). Same name in both → **the skill wins**.
- **Scope:** `.claude/…` = **project, shared via git**. `~/.claude/…` = **personal**.
- **Skill vs CLAUDE.md:** CLAUDE.md = **always-on** standards. Skill = **on-demand** workflow (body loads only when invoked).

| Frontmatter | Exam answer |
|---|---|
| **`context: fork`** | Runs in an **isolated sub-agent**, so **verbose output stays out** of the main chat |
| **`allowed-tools`** | **Restricts** the skill's tools |
| **`argument-hint`** | **Prompts** for required parameters when none are given |

⚠️ **Exam traps:** verbose analysis in CLAUDE.md is wrong (loads every session). Naming conventions in a skill is wrong (absent until invoked). For noisy output use **`context: fork`**.

### 3.3 Path-Specific Rules

- Rule files in **`.claude/rules/`** with YAML frontmatter **`paths:`** load **only when editing matching files**: more **token-efficient** than a root CLAUDE.md.
- **`**/*.test.tsx`** matches test files in **every directory**.

| Need | Use |
|---|---|
| Standards for **all** code | Root CLAUDE.md |
| One **package's** conventions | Directory CLAUDE.md |
| One **file type spread across many folders** (tests, Terraform) | **Path-specific rules** |
| On-demand **workflow** | Skill |

⚠️ **Exam trap:** test files beside source in 50+ folders → **`.claude/rules/` with `paths:`**. Not root CLAUDE.md (loads always), not a CLAUDE.md in every folder (50+ copies).

### 3.4 Plan Mode vs Direct Execution

- **Plan mode** reads and proposes, with **no file changes until you approve**. **Direct execution** just does it.
- **Decide by ambiguity, not difficulty.** A hard but well-defined bug → direct. A simple-sounding feature with several approaches → plan.

| Plan mode | Direct execution |
|---|---|
| Large restructuring, multi-file migration | Single-file bug with a clear stack trace |
| Several valid approaches, architecture decisions | Known fix, known location |
| Need to explore first | One validation check, a config change |

- **Start plan mode:** `claude --permission-mode plan` · **Shift+Tab** until "plan mode on" · `/plan` before a prompt. Writing "in plan mode" in the prompt does **nothing**.
- **Hybrid:** plan, then switch to direct execution. An **Explore subagent** keeps verbose discovery out of the main chat.

⚠️ **Exam trap:** migrating a logging library across 30 files → **plan first, then execute**, not direct alone.

### 3.5 Iterative Refinement

| Situation | Technique |
|---|---|
| Prose is **interpreted differently** each time | **Concrete input/output examples** (2-3 before/after pairs) |
| Complex change with many **edge cases** | **Test-driven**: write tests first, share failures |
| **Unfamiliar domain** | **Interview pattern**: Claude asks questions before coding |
| Several issues that **interact** | **One message** with all feedback |
| Several **independent** issues | **One at a time** |

⚠️ **Exam trap:** interview = *you don't know the domain*. Examples = *you know what you want but results vary*.

### 3.6 CI/CD Integration

- **`-p`** (`--print`) = **non-interactive mode**: reads the prompt, writes to stdout, exits. **Without it the CI job hangs forever.** This is **the** D3 fact.
- **Separate calls for generate and review**: the same session keeps its reasoning bias.
- **Re-reviews:** include **earlier findings** so Claude reports only **new or unaddressed** issues.
- **CLAUDE.md** is read in CI exactly like interactive use.
- **Machine-readable output:** `--output-format json` + `--json-schema`; read the result from `structured_output` (`jq '.structured_output'`).
- **`--append-system-prompt`** = stay a coding assistant plus extra rules. **`--system-prompt`** = **replace** the identity completely.
- **Real-time vs Batch API:** see 4.5.

⚠️ **Exam traps:** `--batch` and `CLAUDE_HEADLESS=true` **don't exist**. Redirecting stdin from `/dev/null` isn't the fix. **The answer is `-p`.** 🎓 **Tip:** *CI = `-p` or hang.*

---

## D4: Prompt Engineering & Structured Output (20%)

### 4.1 System Prompts with Explicit Criteria

- **Vague rules fail:** "be conservative", "only report high-confidence findings", "use your judgement". Give **explicit categorical criteria**: exactly what to flag and what to skip.
- **False-positive trust problem:** a **40%** false-positive rate in one category destroys trust in **all** categories.
- **Fix:** **temporarily disable** the noisy category → rewrite its prompt with **explicit criteria + concrete code examples** → re-enable when precision improves.
- **Order:** explicit criteria **first**; confidence-based routing **second**.

⚠️ **Exam traps:** "report only high-confidence findings" is **wrong** (model confidence is poorly calibrated). A larger model is wrong.

### 4.2 Few-Shot Prompting

- The **most effective technique for consistent output**. Use **2-4 examples** (exam answer), each with **input + output + reasoning** (why this choice over the alternatives). Reasoning lets the model **generalise**.
- **Use it when:** detailed instructions still give **inconsistent formatting** · **ambiguous judgement calls** vary · extraction returns **empty fields for data that exists** (e.g. in narrative text).

| Problem | Right technique |
|---|---|
| Inconsistent formatting | **Few-shot** |
| Malformed JSON | **`tool_use` with a JSON schema** |
| Invented values for missing fields | **Optional / nullable fields** |
| Wrong tool picked | **Better tool descriptions first** |
| Misses info in narrative text | **Few-shot** showing narrative extraction |
| Extracted sum ≠ total | **Validation-retry loop** |

### 4.3 Structured Output with Tool Use

- **`tool_use` with a JSON schema** removes **syntax** errors (missing brackets, wrong types). Prompt-only JSON has **no guarantee**.
- It does **not** prevent **semantic** errors: wrong sums, values in the wrong field, **fabricated** values.
- **`tool_choice`:** see 2.3.

| Schema problem | Fix |
|---|---|
| Model **invents** values | Make fields **optional / nullable** |
| Source is genuinely unclear | Add an **`"unclear"`** enum value |
| Cases outside your categories | **`"other"` + a detail string** |

⚠️ **Exam traps:** "`tool_use` prevents all errors" is wrong. "Lower the temperature" is wrong for fabrication. The fix is **nullable fields**.

### 4.4 Validation, Retry & Feedback Loops

- **Syntax errors:** `tool_use` + `strict: true`. **Semantic errors:** validation logic + a **retry loop**.
- **A good retry sends 3 things:** the **original document**, the **failed extraction**, and the **specific validation error**. A blind retry usually repeats the mistake.

| Retry can fix | Retry can't fix |
|---|---|
| Wrong date format | Info **missing from the source** |
| Value in the wrong field | Data only in an **external document** |
| A missed line item (bad sum) | Facts the model doesn't have |

- **Self-check fields:** `calculated_total` vs `stated_total` · a `conflict_detected` boolean.

⚠️ **Exam trap:** `department` is **absent** from the source → **flag for human review**. Line items **don't sum** to the total → **retry with the error message**.

### 4.5 Batch Processing Strategies

- **Message Batches API:** **50% cheaper**, up to **24 hours** (a maximum, **no latency guarantee**), results matched with **`custom_id`**, and **no multi-turn tool calling** inside one request.

| Workflow | API |
|---|---|
| **Someone is waiting** (pre-merge checks) | **Real-time** |
| Overnight debt report, weekly audit, nightly test generation | **Batch** |

- **SLA maths:** 30-hour SLA − 24-hour worst case = **6 hours** buffer → submit **every 4 hours** (every 6 leaves no margin).
- **Failures:** find them by **`custom_id`** → **resubmit only the failures**, modified (chunk big documents, simplify prompts) → **refine prompts on 5-10 sample documents first**.

⚠️ **Exam trap:** the manager wants *everything* on batch for 50% savings → batch **only latency-tolerant** work, keep **blocking** work real-time.

### 4.6 Multi-Instance & Multi-Pass Review

- **Self-review is weak:** the same session keeps its reasoning and **confirms its own choices**. Use an **independent instance** with no prior context.
- **Inconsistent depth across many files:** the same **per-file pass + cross-file pass** fix as 1.6.
- **Confidence routing:** high confidence → report; low → **human review**. Raw scores are **uncalibrated**, so calibrate on **labelled validation sets** first.

⚠️ **Exam traps:** "please review carefully" in the same session, "use extended thinking" in the generating session, or "switch to a larger context model" are all **wrong**.

---

## D5: Context Management & Reliability (15%)

### 5.1 Context Window Management

- **Progressive summarisation loses exact facts**: amounts, dates, order numbers, IDs.
- **Fix: a persistent case-facts block**: a structured block pulled from the conversation, included in **every** prompt and **never summarised**.
- **"Lost in the middle":** models handle the **start and end** of long input best. **Put a key-findings summary at the start**, details under clear headings.
- **Trim verbose tool output** (e.g. 40+ fields) to the relevant fields **before** it enters history.
- The **API is stateless**: every request carries the full history.
- **Prompt caching:** put **stable content first** (system prompt, tools, documents), then the changing user message; mark the prefix with `cache_control`.

⚠️ **Exam trap:** the agent forgets "$247.83 refund for order #8891" → a **persistent case-facts block**, not "tell it to preserve figures", a bigger window or an external database.

### 5.2 Escalation & Ambiguity Resolution

| ✅ Valid escalation triggers | ❌ Unreliable triggers |
|---|---|
| Customer **explicitly asks for a human** → **escalate immediately**, no investigating first | **Sentiment** (frustration ≠ complexity) |
| **Policy gap or exception** (no documented answer) | **Self-reported confidence** (poorly calibrated) |
| **No meaningful progress** after a real attempt | |

- **Frustrated but solvable** → acknowledge and resolve. If they **repeat** the request for a human after your offer → escalate.
- **Several customers match** → **ask for another identifier** (email, phone, order number). **Never guess** by "most recent" or "most active".
- **Fix for poor escalation decisions:** **explicit escalation criteria + few-shot examples** in the system prompt, not sentiment analysis or a classifier.

### 5.3 Error Propagation in Multi-Agent Systems

- **Structured error context has 4 parts:** **failure type** · **what was attempted** (query, parameters, target) · **partial results** · **alternative approaches**.
- **Recover locally** (subagents retry transient failures with backoff); **propagate only** what they can't fix.
- **Coverage annotations:** the final report states which areas have **gaps** from unavailable sources.
- Access failure vs valid empty result: see 2.2.

| ❌ Anti-pattern | Why it's bad |
|---|---|
| **Silent suppression**: `{results: [], status: "success"}` | The coordinator believes nothing was found. **Worst**, because gaps are invisible |
| **Terminating the whole workflow** on one failure | Throws away all finished work |

⚠️ **Exam trap:** a subagent times out → return **structured error context**, not "empty success", not "stop everything", not a generic "search unavailable".

### 5.4 Codebase Exploration & Context Degradation

- **Symptom:** the agent says "typical patterns in this repo" instead of the **specific classes and paths** it found earlier. It's an **attention-quality** problem, not running out of tokens.

| Mitigation | How it helps |
|---|---|
| **Scratchpad files** | Save findings **outside** the conversation |
| **Subagent delegation** | Verbose exploring happens in **isolated context**; the coordinator keeps summaries |
| **`/compact`** | Summarises **before** the context is full |

- **Between phases:** inject Phase 1 findings into Phase 2 subagents (no cold start). **Crash recovery:** keep **state manifests** at known file paths and reload them on resume.

⚠️ **Exam traps:** a bigger window doesn't fix degradation. Restarting loses all findings. Pre-loading the whole codebase causes the same problem. **Answer: scratchpad files.**

### 5.5 Human Review & Confidence Calibration

- **Aggregate trap:** **97% overall** can hide **40-60% errors** on one document type. Validate **per document type and field**.
- **Raw confidence scores are uncalibrated.** Calibrate against **labelled validation sets**.
- **Stratified random sampling** also checks **high-confidence** items (to measure accuracy and spot new error patterns). Sampling only low-confidence items misses systematic errors.
- **Reviewer time** goes to the **highest-uncertainty items first**, reordered as new items arrive.
- **Order before automating:** measure by type and field → calibrate → set thresholds → sample → **only then** reduce human review on proven segments.

⚠️ **Exam trap:** "automate everything above 95% confidence" is a **critical risk**.

### 5.6 Information Provenance & Multi-Source Synthesis

- **Claim-source mapping has 5 fields:** **claim · source URL · document name · relevant excerpt · publication date.**
- **Attribution dies during synthesis** (paraphrasing strips the mapping), so **explicitly instruct** the synthesis agent to **keep** it.
- **Conflicting numbers from credible sources** → report **both values with source and date**. Never pick the newest, the average or the "most authoritative".
- **Dates explain differences:** 8% (2023) and 12% (2024) is a **trend**, not a contradiction.

| Content | Format |
|---|---|
| Financial data | **Table** |
| News / events | **Prose** |
| APIs, configs, technical findings | **Structured list** |

⚠️ **Exam trap:** 12% vs 8% growth → **show both with source and date**, don't average to 10%.

---

## 📝 Cheat Sheet

### Where Things Live (project = shared via git, user = personal)

| What | Project (team) | User (personal) |
|---|---|---|
| CLAUDE.md | `.claude/CLAUDE.md` or root `CLAUDE.md` | `~/.claude/CLAUDE.md` |
| Skills / commands | `.claude/skills/` · `.claude/commands/` | `~/.claude/skills/` · `~/.claude/commands/` |
| MCP servers | `.mcp.json` | `~/.claude.json` |
| Path rules | `.claude/rules/` with `paths:` | none |

### Never Pick These

| Wrong answer | Right answer | Lesson |
|---|---|---|
| Iteration cap, or parsing text, to stop a loop | **`stop_reason`** | 1.1 |
| Subagent-to-subagent messaging | Route through the **coordinator** | 1.2 |
| Stronger prompt for money/security/compliance | **Gate or PreToolUse hook** | 1.4, 1.5 |
| PostToolUse to block an action | **PreToolUse** | 1.5 |
| Bigger context window for dilution or degradation | **Multi-pass** / **scratchpad files** | 1.6, 5.4 |
| Few-shot or classifier as first fix for misrouting | **Expand tool descriptions** | 2.1 |
| Retrying an empty lookup | Separate **access failure** from **empty result** | 2.2 |
| Glob to find callers, or reading every file first | **Grep**, then Glob for tests | 2.5 |
| Team rules in the user-level file | **Project level** | 3.1 |
| CI job without `-p` | **`-p`** | 3.6 |
| "Report only high-confidence findings" | **Explicit criteria** | 4.1 |
| `tool_use` to stop fabrication, or lower temperature | **Nullable fields** | 4.3 |
| Retrying when the data isn't in the source | **Flag for human review** | 4.4 |
| Everything on the Batch API | Batch **only** latency-tolerant work | 4.5 |
| Sentiment or confidence as escalation trigger | **Explicit criteria + few-shot** | 5.2 |
| Empty-success or full shutdown on an error | **Structured error context** | 5.3 |
| Trusting overall accuracy, or raw confidence | **Segment and calibrate** | 5.5 |
| Picking or averaging conflicting sources | **Both values, with source and date** | 5.6 |

### Where the Exam Answer Differs from Today's Product

> The lessons say: **answer the Exam Guide v1.0 wording on the exam**.

| Topic | Exam answer | Today's product (not on the exam) |
|---|---|---|
| Failed **Edit** (non-unique anchor) | Edit → **Read + Write** | Widen `old_string` or use `replace_all` first |
| `/memory` vs `/context` | **`/memory`** shows what loaded | `/context` shows what loaded; `/memory` lists and opens files |
| Skill **`allowed-tools`** | **Restricts** tools | **Pre-approves** tools (no permission prompt) |
| Skill **`argument-hint`** | **Prompts** for missing parameters | A label shown in autocomplete |
| Few-shot count | **2-4** | Docs now say 3-5 |
| Tool overload | **18 tools vs 4-5** | Docs say selection degrades past about 30-50 tools |
| Batch + tools | **No multi-turn tool calling** in a batch | Server tools can run a loop in a batch; **client tools** still can't |
