[⬅ Back to course index](../README.md)

# 📚 Claude 101 — Course Notes

---

## Chapter 1: What is Claude?

> Claude is more than a chatbot—it's an AI assistant designed to be your thinking partner.

### 🧠 Key Takeaways

- **Claude is built to be helpful, harmless, and honest** — At a high level, Claude is guided by principles that help it avoid toxic or discriminatory outputs, avoid helping humans engage in illegal or unethical activities, and broadly behave as a helpful, honest, and harmless AI system. This approach, called **Constitutional AI**, means Claude is trained to align with human values and operate transparently.
- **Claude is more than a chatbot** — Claude is capable of a wide variety of conversational and text processing tasks while maintaining a high degree of reliability and predictability, including summarization, search, creative and collaborative writing, Q&A, coding, and more. Think of Claude as a thinking partner who can help you tackle complex problems and work through challenging situations, not just answer simple questions.
- **Claude is designed to be steerable and collaborative** — Claude can take direction on personality, tone, and behavior, and customers report that Claude is much less likely to produce harmful outputs, easier to converse with, and more steerable—so you can get your desired output with less effort.
- **You can access Claude wherever you work** — Claude apps are available to all plan types—Free, Pro, Max, Team, and Enterprise. Your conversations, projects, memory, and preferences sync across all devices when you're signed in. Whether you're at your desk or on the go, Claude is available through web, desktop, and mobile apps.

### 🛠️ Understanding Claude's Capabilities

Claude can help with a wide range of tasks that go far beyond simple question-and-answer interactions to assistant-like partnership that can both **automate** *and* **augment** your work.

| Area | What Claude Excels At |
|------|------------------------|
| ✍️ **Writing & content creation** | Collaborates on social media posts, professional emails, and complex reports. Because Claude is trained to take direction on personality and tone, you can iterate together on structure and clarity until your voice comes through clearly. |
| 🔎 **Research & analysis** | Helps you explore research angles, compile findings, and analyze data to surface meaningful insights. You can upload documents and Claude will help you make sense of complex information — enabled by Claude's large **context window**, which can ingest 200K+ tokens (about 500 pages of text or more), with up to 1M tokens available on Pro, Max, Team, and Enterprise plans when using supported models. |
| 💻 **Coding assistance** | One of Claude's greatest strengths. Strong performance on real-world coding tasks means it can help you write, debug, and explain code across multiple programming languages. |
| 🧩 **Problem-solving & reasoning** | Handles complex cognitive tasks, mathematical problems, strategic thinking and analysis, and research. Claude can respond near-instantly or take time to reason first — a capability called **Thinking**. When a problem calls for careful analysis, Claude can work through it step by step before it answers. |
| 📖 **Learning new things** | Adapts to your learning style and pace. **Learning mode** is a Claude experience that guides your reasoning process rather than providing answers, helping develop critical thinking skills. |

> Get inspired on ways to use Claude in your specific function by exploring the [use-case gallery](https://claude.com/resources/use-cases) on claude.com. For a deeper dive into what AI can (and can't) do, see the [AI Capabilities](https://anthropic.skilljar.com/ai-capabilities-and-limitations) course.

### 🌐 Ways to Access Claude

Claude is the intelligence—the AI assistant you're learning to work with throughout this course. That same intelligence is available across multiple interfaces, each suited to different types of tasks.

| Interface | Description |
|-----------|-------------|
| **[Claude.ai](https://claude.ai/)** (+ mobile/desktop apps) | The primary way most people interact with Claude — ask questions, brainstorm ideas, create and edit documents, and more. Ideal for conversations, writing assistance, research, analysis, and creating files. **This is the focus of this course.** |
| **[Claude Code](https://claude.com/product/claude-code)** | An agentic coding tool designed for developers, but usable for all kinds of file manipulation on your desktop. Can directly edit files, run commands, and create commits. |
| **[@Claude](https://claude.com/claude-and-slack)** | Brings Claude directly into Slack — chat from the AI assistant header in any channel/conversation, or tag @Claude in threads. When connected, Claude searches your workspace's channels, DMs, and shared files for context. |
| **[Claude Design](https://claude.ai/design)** | A dedicated space for turning ideas into working interfaces. Describe what you want — or start from a sketch or screenshot — and Claude builds an interactive prototype you can refine and hand off to your team. |
| **[Claude for Microsoft 365](https://support.claude.com/en/articles/13892150-work-across-excel-powerpoint-and-word)** | Brings Claude into Excel, PowerPoint, Word, and Outlook as a sidebar — analyze, draft, and edit inside the document you already have open, carrying context from one app to the next. |

> This course focuses primarily on [Claude.ai](https://claude.ai/), but you can also check out [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) for more on using Claude in development workflows.

### 🤔 Lesson Reflection

- What tasks in your current work might benefit from having Claude as a thinking partner?
- Take a look at your calendar (or better yet, ask Claude to) and identify a few tasks you might want to use Claude to support.

---

## Chapter 2: Your First Conversation with Claude

> ⏱️ Estimated time: 20 minutes · 🎥 Video: *Getting started with Claude.ai*

> Claude brings AI intelligence, but you bring the context and expertise that makes the work meaningful.

### 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Start a new conversation with Claude and navigate the interface
- Write effective prompts using clear, specific language
- Upload files and images to provide Claude with additional context
- Use follow-up messages to iterate and refine Claude's responses

### 🧠 Key Takeaways

- Claude is a powerful, intelligent collaborator that amplifies your capabilities across all of your work. Claude brings AI intelligence, but **you** bring the context and expertise that makes the work meaningful.
- The best approach when speaking to Claude is like you would a coworker — **naturally, concisely, and conversationally.**
- Before your next conversation with Claude, consider: **setting the stage** (your role, objectives, and context), **defining the task** (what action you want Claude to take), and **specifying rules** (style, tone, and examples).
- When you upload relevant documents or background information into a chat, Claude considers that content in its response — think of it as a shortcut so Claude can understand what your needs are.
- The real power of Claude comes with **continued and frequent communication**, not just one-off prompts.

### 💬 Starting Your First Conversation

When you open [Claude.ai](https://claude.ai/), you'll see a clean interface with a text input area at the bottom of the screen.

Your prompts can range from simple questions (like brainstorming code names for a new feature) to complex requests to co-create files.

### ✍️ Writing Effective Prompts

All interactions with Claude begin with a **prompt**, and these prompts, combined with other context, impact Claude's response. The best approach when speaking to Claude is like you would a coworker — naturally, concisely, and conversationally.

But you may ask, what is a good prompt? Before your next conversation with Claude, consider a few things:

![Writing a good prompt? 1. Set Stage, 2. Define Task, 3. Specify Rules](assets/L2-first-conversation/writing-a-good-prompt.png)

| # | Element | Ask yourself |
|---|---------|--------------|
| 1 | 🧩 **Setting the stage** | What is your role and what are your objectives? Is there context about your work that Claude should know about? |
| 2 | ✏️ **Defining the task** | What action do you want Claude to take? Do you want Claude to write, analyze, build, or something else? |
| 3 | ✅ **Specifying rules** | What's the style or tone you want Claude to use? Are there examples that you can attach to show Claude what you're looking for? |

#### Putting It Together

Here's an example prompt that uses all three elements:

> *"I'm the marketing lead at an indie streaming startup, and we're preparing an investor pitch deck for Series A investors. Can you research the current state of the independent film streaming market and identify key trends, competitor positioning, and growth opportunities? Use current web research with citations and structure it as a professional report of up to 5 pages, with an executive summary, market analysis, competitive landscape, and growth opportunities."*

| Element | How it shows up in this prompt |
|---------|--------------------------------|
| 🧩 **Setting the stage** | Marketing lead at an indie streaming startup, preparing a Series A investor pitch deck — the context and objective |
| ✏️ **Defining the task** | Research the market, with relevant details (trends, competitors, opportunities) — the specific action |
| ✅ **Specifying rules** | Current web research with citations, structured as a professional report — the exact style and format |

Here's that same prompt being entered into Claude.ai — note the toolbar below the input box (tools menu, model picker, and Research toggle):

![Typing the market analysis prompt into Claude.ai, with the tools menu open showing Use style, Extended thinking, Web search, Drive search, Gmail search, and Calendar search](assets/L2-first-conversation/prompt-box-tools-menu.png)

![Claude.ai home screen with the same prompt drafted and the model picker open, showing Opus 4.1 and Sonnet 4.5](assets/L2-first-conversation/model-selector-dropdown.png)

> 💡 **Want to go deeper?** This prompt framework is adapted from the **4D Framework for AI Fluency**, developed through research collaboration between Professor Rick Dakan (Ringling College of Art and Design) and Professor Joseph Feller (University College Cork). The framework identifies four core competencies — **Delegation, Description, Discernment, and Diligence** — that enable effective collaboration with AI. See [ai-fluency/README.md](../ai-fluency/README.md) for the full course notes.

#### 🤖 Choosing a Model: Opus vs. Sonnet

The model picker (shown above) lets you choose which Claude model handles your request:

![Claude model review — Opus: the largest scale model, hybrid reasoning capabilities](assets/L2-first-conversation/model-review-opus.png)

![Claude model review — Sonnet: default mode, balances capabilities with cost-effectiveness](assets/L2-first-conversation/model-review-sonnet.png)

| Model | Best for | Notes |
|-------|----------|-------|
| 🔵 **Opus** | Most **complex** tasks | The largest scale model, with hybrid reasoning capabilities |
| 🟢 **Sonnet** | **Everyday** tasks | Default mode — balances capabilities with cost-effectiveness |

![Opus vs. Sonnet — side-by-side comparison card](assets/L2-first-conversation/model-review-opus-vs-sonnet.png)

#### 💭 Extended Thinking Mode

Inside the tools menu you'll also find **Extended thinking** — a toggle that gives Claude space to reason step-by-step before answering. It's not a fit for every prompt:

![Thinking Mode best practices — good fits: project planning, planning & trend analysis, technical problems, math & coding; not worth it for: simple questions, basic information, general writing](assets/L2-first-conversation/thinking-mode-best-practices.png)

| ✅ Good fit | ❌ Not worth it |
|-------------|-----------------|
| Project planning | Simple questions |
| Planning & trend analysis | Basic information |
| Technical problems | General writing |
| Math & coding | |

### 📎 Adding Context

Uploads, connectors, and custom preferences offer ways to give Claude even more context about your work.

Claude can analyze both text and visual elements (like images, charts, and graphics) in PDFs and other documents.

| Supported file types |
|-----------------------|
| PDF, DOCX, CSV, TXT, and common image formats like PNG and JPEG |

Some practical ways to use file uploads:
- Upload a document and ask Claude to summarize the key points
- Share an image and ask Claude to describe or analyze what it sees
- Attach a spreadsheet and ask Claude to identify trends in the data
- Upload code and ask Claude to explain how it works or find bugs

Once uploaded, Claude will automatically attempt to parse the file's content. In the chat, the file appears as an attachment and you can then prompt Claude about it.

> 💡 **Pro tip:** If you'd like Claude to consider specific preferences in every response, go to **Settings > General > "What personal preferences should Claude consider?"** to set preferences that apply to every conversation.

### 🔁 Iterating on Claude's Responses

Conversations with Claude are meant to be **iterative**. Chaining bite-sized prompts together allows for a natural dialogue where you guide the conversation based on Claude's replies.

If Claude's first response isn't quite what you wanted, you have several options:

| Option | Example |
|--------|---------|
| **Ask follow-up questions** | Build on Claude's response by asking for more detail, a different angle, or clarification: *"Can you expand on the second point?"* or *"That's helpful, but can you make it more concise?"* |
| **Provide feedback** | Tell Claude what you liked and didn't like about its response: *"This is good, but the tone is too formal. Can you make it more conversational?"* |
| **Redirect or restart** | If Claude went in a different direction than you intended, steer it back: *"Actually, I was asking about X, not Y. Let me clarify..."*. Worst case, restart your conversation in a new chat to fully refresh the context. |

> 💡 **Pro tip:** You can also click the pencil icon on any of your messages to edit and resubmit your prompt — useful when you want to refine your request rather than add a new message.

### 🌟 Personalizing Claude

Two features help Claude work better for you over time, increasing the power of your prompts:

| Feature | What it does |
|---------|---------------|
| 🧠 **Memory** | Automatically saves key context from your conversations — your role, preferences, past decisions, and working style — so you don't have to repeat yourself every time you start a new chat. Review, edit, or delete anything Claude remembers anytime in Settings; memory syncs across all your devices. |
| 🎨 **Styles** | Customize how Claude communicates. Choose from preset options — like concise, formal, or explanatory — or create your own custom style by describing exactly how you want Claude to write. Once set, your style applies across all conversations automatically. |

### 🤔 Put It Into Practice

Before moving on, try prompting Claude with a question or task. If you need an idea to get started, feel free to explore the [use-case gallery](https://claude.com/resources/use-cases).

---

## Chapter 3: Getting Better Results

> ⏱️ Estimated time: 15 minutes

### 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Recognize common challenges when starting out with AI and use troubleshooting techniques to overcome them
- Define AI Fluency and know where to go to learn more about working with AI in a fluent way
- Explain how you might set up evals to better understand how Claude might perform with your unique workflows

### 🛠️ Common Challenges and How to Fix Them

As you start working with Claude, you'll likely encounter moments where the response isn't quite what you expected. **This is normal** — it's an opportunity to refine your approach.

| Challenge | What's happening | Try this |
|-----------|-------------------|----------|
| **Claude's response is too generic** | Your prompt didn't include enough context about your specific situation | Add details about your audience, role, or constraints. Instead of *"Write an email about the project delay,"* try *"Write an email to our enterprise client explaining that the software integration will be delayed by two weeks. They've been patient so far but this is the second delay. Keep it professional but apologetic."* |
| **The response is too long (or too short)** | Claude is guessing at appropriate length | Be explicit: *"Give me a two-paragraph summary"* or *"Keep this under 100 words"* or *"I need a comprehensive analysis — length isn't a concern."* |
| **Claude didn't follow my format** | Claude understood what you want but not how you want it presented | Show, don't just tell. Provide an example of the format, or describe the structure explicitly: *"Use bullet points with bold headers for each section."* |
| **I got confident-sounding information that turned out to be wrong** | Claude occasionally generates plausible but incorrect information, especially with specific facts or niche topics (a **hallucination**) | For high-stakes work, verify key facts independently. Ask Claude to cite sources or indicate confidence level. Enable web search to ground responses in current information. |
| **The tone isn't right** | Claude defaults to helpful and professional, which may not match your needs | Describe the tone in plain language: *"Make this more conversational"* or *"This should sound authoritative and formal."* Provide an example of writing in the style you want. |

### 🔁 The Iteration Mindset

One of the most important shifts when working with Claude is recognizing that your **first prompt rarely produces a perfect result** — and that's okay. Think of your initial prompt as the start of a conversation, not a one-shot request.

Effective Claude users:
- **Treat first drafts as starting points.** Review what Claude produces, identify what's working and what isn't, then refine.
- **Give specific feedback.** *"Make it shorter"* is fine, but *"Cut the first two paragraphs and make the conclusion more action-oriented"* is better.
- **Know when to start fresh.** If a conversation has gone off track, sometimes it's faster to open a new chat with a clearer prompt than to try to redirect.

### 🧭 What is AI Fluency?

> **AI Fluency** is the ability to collaborate effectively with AI tools — not just knowing which buttons to click, but developing the judgment to use AI well across different situations.

The **4D Framework for AI Fluency**, developed through research collaboration between Professor Rick Dakan (Ringling College of Art and Design) and Professor Joseph Feller (University College Cork), identifies four core competencies that, when combined, help you make the most of your AI interactions:

| # | Competency | What it includes |
|---|------------|-------------------|
| 1 | 🎯 **Delegation** | Deciding what work should be done by humans, what work should be done by AI, and how to distribute tasks between them. Includes understanding your goals, AI capabilities, and making strategic choices about collaboration. |
| 2 | 💬 **Description** | Effectively communicating with AI systems. Includes clearly defining outputs, guiding AI processes, and specifying desired AI behaviors and interactions. |
| 3 | 🔍 **Discernment** | Thoughtfully and critically evaluating AI outputs, processes, behaviors and interactions. Includes assessing quality, accuracy, appropriateness, and determining areas for improvement. |
| 4 | 🛡️ **Diligence** | Using AI responsibly and ethically. Includes making thoughtful choices about AI systems and interactions, maintaining transparency, and taking accountability for AI-assisted work. |

You've already been practicing these skills throughout this course:
- The prompt framework from **Lesson 2** (setting the stage, defining the task, specifying rules) is rooted in **Description**.
- The troubleshooting techniques above draw on **Discernment** and **Diligence**.

> 💡 To learn more, check out the full [ai-fluency/README.md](../ai-fluency/README.md) course notes — our free AI Fluency course explores all four competencies in depth, with practical exercises and real-world applications.

### 📊 Evaluating Claude for Your Workflows

As you start integrating Claude into more of your work, you might wonder: *how do I know if Claude is actually good at this particular task?*

This is where **Discernment** becomes essential. **Evals** (short for evaluations) are a way to develop intuition for assessing Claude's outputs on the tasks that matter to you — systematic ways to test how well Claude performs on specific types of tasks that matter to you.

#### Why Evals Matter

Your work is unique. Claude might excel at drafting marketing copy but need more guidance for technical documentation in your specific domain. Running simple evals helps you:
- Understand where Claude adds the most value in your workflow
- Identify tasks where you'll need to provide more context or examples
- Build confidence in Claude's outputs for recurring tasks

#### 🧪 A Simple Eval Approach

You don't need complex infrastructure to evaluate Claude. Here's a practical approach:

![Delegation-Diligence loop — Delegation approach: reproduce past data analysis using AI; Diligence questions: evaluate AI output quality against known results](assets/L3-better-results/delegation-diligence-loop.png)

| # | Step | What to do |
|---|------|------------|
| 1 | **Gather examples** | Collect 5–10 examples of a task you do regularly — emails you've written, reports you've created, analyses you've done. |
| 2 | **Create test prompts** | Write prompts that would generate similar outputs. Include the context you'd naturally have when doing this work. |
| 3 | **Compare outputs** | Run your prompts and compare Claude's responses to your examples. Ask: *Does Claude capture the key information? Is the tone and style appropriate? What's missing or could be improved?* |
| 4 | **Refine your approach** | Based on what you learn, adjust your prompts, add examples to show Claude what good looks like, or identify where human review is essential. |

### 📈 Example: Using Claude for Data Analysis

> 🎥 This example is taken from the *AI Fluency for nonprofits* course, but it's relevant for anyone working with data in AI.

![Data analysis scenario — Valley Veterans Services: analyzes program attendance alongside employment outcomes, calculating participation rates; tracks monthly changes and whether attendance correlates with job placement success; the analysis takes hours; Rio wants to interpret the results himself but could do without the data cleaning and formula mayhem](assets/L3-better-results/data-analysis-scenario-valley-veterans.png)

To evaluate how Claude might work with your data:
1. Find a dataset you've manually analyzed
2. Create prompts that request Claude to do the analysis on your behalf
3. Compare Claude's results to your originals
4. Note patterns and refine your prompt accordingly — maybe Claude gets the right numbers but misses the overall patterns

![Key takeaways — identify a specific analytical task to delegate; find past data where you already completed that analysis; work with AI to reproduce your past analysis and systematically evaluate the results; identify gaps, refine your delegation, and test again](assets/L3-better-results/data-analysis-video-key-takeaways.png)

This kind of lightweight evaluation helps you develop intuition for how to work with Claude on tasks that matter to you — and where to focus your review and refinement energy.

### 🤔 Lesson Reflection

- Which of the common challenges have you already encountered? What techniques might you try next time?
- Where in your work would a simple eval help you understand if Claude is a good fit for a recurring task?
- How might the 4D Framework help you think about your collaboration with Claude?

---

## Chapter 4: How You'll Work with Claude on Your Desktop

> ⏱️ Estimated time: 6 minutes

### 🎯 Learning Objectives

By the end of this lesson you'll be able to:
- Distinguish the ways you work with Claude on the desktop — working with Claude turn by turn, handing whole tasks off for Claude to run, and building software in your codebase
- Recognize which shape of work a task calls for before you start it
- Find where each way of working lives in the desktop app today

### 🖥️ Working with Claude on Your Desktop

The Claude desktop app is your home base for working with Claude — from a quick question mid-meeting to a report Claude assembles from six sources while you do something else. The work sorts into **three shapes**, and knowing which one you're in is the whole skill of this lesson:

1. 💬 **Working with Claude, turn by turn.** You and Claude go back and forth. You ask, Claude answers, you steer, it revises. The thinking happens in the exchange.
2. 🤝 **Handing work off to Claude.** You describe an outcome — a finished brief, a formatted deliverable, a task that runs every Monday — and Claude plans it, does it, and comes back with the result. You review the plan and the output; you don't stitch the steps together yourself.
3. 💻 **Building software with Claude Code.** Claude works directly in a codebase: reading it, writing and testing code, running commands. Built for developers, and worth knowing about even if you never open it.

The first two are where most knowledge workers spend their day; the third is the developer's workspace.

> **In the product today.** Turn-by-turn work happens in **Chat**. Work you hand off runs in **Cowork**. Building software happens in the **Code tab**. All three live in the Claude desktop app.

### 💬 Working with Claude, Turn by Turn

This is Claude as a thinking partner: the shape of work where the value is in the exchange itself. You bring a half-formed idea, an unfamiliar dashboard, a paragraph that isn't landing — and you work it out together, one turn at a time.

**Reach for this when:**
- **The answer changes what you ask next.** You're brainstorming, and each response opens the next question. You couldn't have written the whole request up front, because you didn't know yet.
- **You want to stay in it.** Drafting, editing, thinking out loud — the point is your judgment on every turn, not a finished thing at the end.
- **It's quick.** A question, a rewrite, a "what does this mean?" — small enough that setting up a whole task would be overhead.

**Try it out when:**
- You're staring at an unfamiliar dashboard. Screenshot it and ask *"what do these metrics mean?"* Claude explains while the dashboard stays in view, and your follow-up (*"okay, which of these should I actually worry about?"*) is the next turn.
- You're between meetings and need to structure a presentation. Talk it through by voice; Claude drafts an outline from what you said; you push back on section three; it revises. Four turns, done before your next call.
- You've been jotting product-launch ideas across Apple Notes for weeks. Ask Claude to pull together everything about the launch, figure out what you left half-finished, and check your other connected tools for gaps. Then work the gaps together.

**In the product today.** In the desktop app this is **Chat** — the same Claude you know from claude.ai, plus a few things that come from running natively on your computer:

| Feature | What it does |
|---------|---------------|
| **Quick entry** | Double-tap the Option key (Mac) to pull Claude up over whatever you're working on. It answers in a compact window that stays on top as you switch apps. |
| **Screenshots and window sharing** | Capture a screenshot or share a window so Claude sees what you see. (Mac) |
| **Dictation** | Talk through a problem instead of typing. (Mac) |
| **Desktop connectors** | Connect local tools and services so Claude can work with what's on your machine. |

### 🤝 Handing Work Off to Claude

Working agentically with Claude is a new way of working for many people. Instead of asking a question, you hand Claude the whole piece of work — gather the context, do the analysis, produce the finished thing — and it comes back done. You're **delegating**, not just chatting.

**Reach for this when:**
- **The task has several steps** you'd normally do in sequence. Pull the figures, compare them, draft the summary, format the doc. Handed off, that's one instruction, not four errands.
- **The output is a real deliverable.** A Word doc, a spreadsheet, a deck, a formatted PDF — saved where you need it, not pasted into a chat window for you to reassemble.
- **The work spans your tools.** Meeting notes in one place, the thread in Slack, last quarter's numbers in a spreadsheet. Set up a Friday roll-up as a scheduled task and Claude gathers all three itself every time it runs — nothing for you to round up first.
- **It should happen on a schedule, or while you're doing something else.** A Friday review of what shipped. A Monday briefing that preps you for your next meeting.

> Handing work off doesn't mean stepping back from it. Before Claude starts, it may ask a few questions to pin down scope and format, and it shows you the plan. As it works, you can watch the task take shape — the sources it's drawing from, the files forming, its progress through the plan — and steer at any point. And when Claude is set to ask before acting, it stops for your approval on the actions that matter, like sending an email or sharing a file. **You stay in control of what leaves your desk.**

**Try it out when:**
- You want to query all your tools like a database. *"Review what we decided about pricing last quarter across meeting notes, Slack, and email, then update the Q3 deck with the findings."* Claude finds the answer across all of them and updates the deck. Hand it off, keep working, check the result.
- You have a folder of 50+ project documents — contracts, financial reports, meeting transcripts. Ask Claude to find the ones most relevant to your initiative and produce a summary memo. It reads every page and pulls out the patterns that only emerge from reading all of them. Review fifty like you'd review five.
- You do the same work every Monday morning — check messages, assemble a status update, prep for the day's meetings. Set it up once as a scheduled task, and start Monday with answers instead of admin.

**In the product today.** In the desktop app, you can hand off tasks in **Cowork**. What that gives you today:

| Capability | What it does |
|------------|---------------|
| **Local folder access** | Point Claude at a folder; it reads what's there and saves finished work back to the same place. This is the concrete difference from turn-by-turn Chat, which can read what you upload but hands finished files back as downloads rather than saving them into your folder. |
| **Scheduled tasks** | Set a task once — a daily briefing, a weekly roundup, a morning inbox triage — and Claude runs it on the cadence you set. If your computer or the app was closed at the scheduled time, it catches up when you're back. |
| **Subagents** | For a big job, Claude splits the work across background workers running in parallel, each with its own context, and hands you one finished deliverable. |
| **Projects** | Group related tasks into a workspace with its own files, instructions, and memory — like projects in Chat, but built around the tasks you run. |
| **Browser use** | With Claude in Chrome, Claude navigates websites and pulls what it finds straight into the task — competitor pricing across ten sites, data from pages with no API. |
| **Computer use** | When there's no connector for what you need, Claude can operate your computer directly — clicking, typing, opening apps — asking permission before each app it touches, with a blocklist for anything off-limits. In research preview on Pro and Max plans. |
| **Plugins** | Ready-made bundles of skills, connectors, and agents built for a specific kind of work — a sales plugin, a finance one, a legal one — so Claude works the way that role works. Browse and add them under **Customize → Plugins**. |

> Cowork is available to **Pro, Max, Team, and Enterprise** users, with new capabilities added regularly.

### 💻 Building Software with Claude Code

If you write code, the desktop app gives you a full development environment. Claude works directly in your codebase — reading what's there, writing and modifying code, running commands. Visual diffs show what changed, a built-in terminal shows commands as they run, and **git tracks every version** so you can always roll back.

> If you're not a developer, the takeaway is just this: it's a separate tab, and this course doesn't need it — *Claude Code in Action* covers it in depth.

You choose **where** the work happens:

| Environment | What it means |
|-------------|----------------|
| **Local** | Select a folder on your computer and Claude works directly with those files — reading your project, using local tools, and running a development server you can preview in your browser. |
| **Cloud** | Connect a GitHub repository and Claude works in a cloud environment. Sessions continue even if you close the app, so you can start a big refactor and check back later. Good for larger codebases, or when you want to keep the work off your machine. |

You also choose **how much Claude does on its own**:

| Setting | What it means |
|---------|----------------|
| **Manually approve** | Claude proposes every change and waits for your approval. |
| **Accept edits** | Claude applies file edits automatically. |
| **Plan** | Claude creates a plan before making changes. |

> **In the product today.** This lives in the **Code tab** of the desktop app, available on Pro, Max, Team, and Enterprise plans. You can run multiple sessions across projects and filter them by environment (Local or Cloud) and status from the sidebar.

### 🧭 Choosing the Right Shape for the Task

You won't pick a tab first — you'll notice what kind of work is in front of you, and the tab follows. Here's the whole lesson in one table.

| You're about to… | The shape it takes | Where it lives today |
|-------------------|---------------------|------------------------|
| Ask, brainstorm, draft, or think something through, turn by turn | Working with Claude, turn by turn | **Chat** (quick entry, dictation, screenshots) |
| Hand off a multi-step task that ends in a finished deliverable, spans your tools, or runs on a schedule | Handing work off | **Cowork** (folder access, connectors, scheduled tasks, subagents) |
| Write, test, run, and ship code in a codebase | Building software | **The Code tab** (Local or Cloud) |

### 🤔 Lesson Reflection

- Think about how you used Claude this week. Which requests were turn-by-turn thinking, and which were really whole tasks you fed in one question at a time because that's the habit?
- Take the task you'd most like off your plate. Is it multi-step, does it end in a real file, does it span your tools? If yes to any, it's a hand-off — write down the outcome you'd describe to Claude, not the first question you'd ask.

---

## Chapter 5: Introduction to Projects

> 🗂️ **Unit: Organizing Your Work and Knowledge** · ⏱️ Estimated time: 20 minutes · 🎥 Video: *Introduction to Projects — Getting started with projects in Claude.ai*

### 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain what projects are and when to use them
- Create a new project with a name, description, and visibility settings
- Add documents and files to your project's knowledge base
- Write effective project instructions to guide Claude's behavior
- Share projects with teammates (for Claude for Work (Team and Enterprise plan) users)

### 🧠 Key Takeaways

- **Projects are self-contained workspaces** with their own memory, chat histories, knowledge bases, and customized instructions. Think of them as dedicated environments for specific work streams.
- **Project knowledge** enhances Claude's understanding by letting you upload relevant documents that Claude references across all chats within that project. No more re-uploading the same files each time.
- **Project instructions** guide Claude's behavior — you can specify tone, expertise level, response style, and more. These instructions apply to every conversation within the project.
- **Projects scale automatically.** When your knowledge base approaches context limits, Claude switches to searching your project knowledge and pulling in only what's relevant, expanding capacity by up to **10x** while maintaining response quality.
- For **Claude for Work** users, projects enable collaboration. Share projects with teammates so everyone benefits from the same context, instructions, and accumulated knowledge.

### 🗂️ What Are Projects?

Projects are ideal for **storing knowledge** Claude should reference, **organizing related chats** around a specific topic or work area, and **collaborating** with team members who need access to the same shared context.

#### When to Use Projects

Projects are particularly valuable when you're working on something **ongoing** — not just a one-off question. Consider creating a project when you have a workflow with:
- **Reference materials** you'll use repeatedly (meeting notes, survey results, reports, historical data, etc.)
- **Consistent requirements** for how Claude should respond (always use formal language, always cite sources, always follow our template)
- **Team collaboration needs** where multiple people should work from the same foundation

### 🧩 Anatomy of a Project Page

A project page is built around three right-hand panels, each with its own visibility badge:

| Panel | Typical access | What it holds |
|-------|-----------------|-----------------|
| 🧠 **Memory** | *Only you* (private by default) | Builds automatically after a few chats — persists context across conversations within the project |
| 📋 **Instructions** | *All project users* | The behavior rules you write in Step 2 below, editable via a pencil icon |
| 📁 **Files** | *All project users* | Your knowledge base, with a capacity meter (e.g. *"1% of project capacity used"*) and a **+** button to add more |

Above that sits the project name, a **Share** button, and the chat prompt box (with its own model picker and history icon). Below the prompt box, chats split into **Your chats** (private until shared) and **Activity**.

> 💡 **Example:** a *"Brand Voice & Marketing Writing Assistant"* project for a flower distribution company — its instructions define Claude as *"a marketing writing assistant for Flower Power,"* and its knowledge base holds a Voice & Style Manual, a Brand Voice Framework, and Brand Voice & Messaging Guidelines (`.docx`/`.txt`/`.pdf` files, each shown with a line count).

### 🏗️ Creating Your First Project

Setting up a project takes just a few minutes.

#### Step 1: Set Up Your Project

1. Hover over the left sidebar and click **"Projects,"** or navigate directly to `claude.ai/projects`
2. Click **"+ New Project"** in the upper right corner
3. Give your project a descriptive name (e.g., *"Q4 Marketing Campaign"* or *"Product Documentation"*)
4. Add a brief description of what you're working on. Claude doesn't see this description directly — it helps you and your teammates understand the project's purpose.
5. Choose your **visibility settings**: keep it private or share with your organization (for Claude for Work users)

#### Step 2: Add Project Instructions

Project instructions tell Claude how to behave across all conversations in this project. Click **"Instructions"** to open the instructions panel.

Good project instructions typically include:

| Type | Example |
|------|---------|
| **Context** about what you're working on | *"This project is for creating marketing content for our B2B software product."* |
| **Process** instructions | *"First consider a blog structure that will entice this audience, then write the draft."* |
| **Tone and style** preferences | *"Use a professional but conversational tone. Avoid jargon when possible."* |
| **Specific requirements** | *"Always include a call-to-action at the end of marketing copy."* |

Once you've written your instructions, click **"Save instructions."** These apply to every chat in this project and work alongside any user preferences and styles you've set.

> 💡 You can also use project instructions to **automate workflows** — e.g., *"When I upload a meeting transcript, create a structured summary using this template."* Think of instructions as programming Claude's behavior for this project.

#### Step 3: Build Your Knowledge Base

Your project's knowledge base is where you upload documents that Claude should reference, via the files menu on the right side of your project's main page.

Click the **"+"** button to add content — supported types include PDF, DOCX, CSV, TXT, HTML, and more, or connect to **Google Drive** to link documents directly.

**What to upload:**
- Reference documents (brand guidelines, style guides, templates)
- Background materials (research reports, meeting notes, requirements docs)
- Examples of work you want Claude to emulate
- Technical documentation or specifications

> 💡 **Pro tip:** Name your files descriptively. Claude uses file names to understand and retrieve the right information, so `Q4-2024-Brand-Guidelines.pdf` is more helpful than `document1.pdf`.

### 📈 How Projects Handle Large Knowledge Bases

Projects automatically scale to handle large amounts of content through a process called **Retrieval Augmented Generation (RAG)**. At a high level, Claude can automatically find and use the most relevant parts of your uploaded documents when answering, without you needing to tell it which file to look at.

When your project knowledge approaches the context window limit, Claude stops loading everything at once and instead **searches your project's files**, retrieving only what's relevant to your question — expanding your project's capacity by **up to 10x** while maintaining response quality.

You'll see a visual indicator when your project is RAG-enabled, but the experience should feel the same — you can still upload documents, chat with Claude, and get context-aware responses.

### 💬 Working Within Your Project

Once your project is set up, you can start chatting with Claude. Each conversation within the project **automatically** has access to your knowledge base and follows your project instructions.

### 🤝 Collaboration Features

For users on **Claude for Work (Team and Enterprise)** plans, projects become even more powerful through collaboration features.

#### Permission Levels

| Level | What it means |
|-------|-----------------|
| 👀 **Can view** | Members can see project contents, access knowledge, and chat — but can't make changes. Read-only access with discussion rights. |
| ✏️ **Can edit** | Members have full collaboration power. They can modify instructions, update knowledge, manage other members, and actively contribute to the project. |
| 👑 **Owner** | Project creators control everything, including who sees the project. They can share with specific people or make projects visible to the entire organization. |

#### Sharing Your Project

1. Open the project you want to share
2. Click the **"Share project"** button to the right of the project name
3. Add individual members using their name or email, or copy and paste a list of email addresses for bulk sharing (the project then shows up in their **"Shared with you"** section)
4. Or, share with **"Everyone at [your organization]"** to make your project discoverable within the Team tab

> In the share dialog, each person gets their own access-level dropdown (e.g., **Can edit**) next to their name, plus a **General access** setting (e.g., *"Only people invited"*) and a **Copy link** shortcut for bulk sharing.

Team members receive **email notifications** when you share a project with them, and they can find shared projects in their **"Shared with me"** tab.

### 💡 Example Projects to Inspire You

Not sure where to start? Here are some common project types across different functions:

| Project | What to upload | What Claude does |
|---------|------------------|--------------------|
| **Q4 product launch** | Product specs, competitive analysis, messaging brainstorming notes | Keeps this context top of mind for any inquiry or document draft |
| **Research support** | Competitive review, user research data, customer feedback | Synthesizes sources, drafts reports, maintains consistency across recommendations |
| **Client account hub** | Client's brand guidelines, past deliverables, communication history | Matches their tone and references their specific context when creating proposals or reports |
| **Event planning workspace** | Venue contracts, speaker bios, attendee data | Generates run-of-show documents, attendee communications, and post-event reports consistent with your event's theme |
| **Job description generator** | Past job descriptions, team charters, internal headcount request docs | Drafts job descriptions that reflect your team's actual work and culture |

More ideas from the video — projects aren't just for work:

| 🌂 Bring a product to market | ✏️ Establish a content creation hub | 🍎 Develop an educational course |
|---|---|---|
| **📊 Financial & budget planning** | | **🏠 Manage a home renovation** |

### ✅ Best Practices for Projects

- **Start focused, then expand.** Begin with a specific use case rather than trying to create one project for everything. You can always add more content as you go.
- **Keep your knowledge base current.** Outdated documents can lead to outdated responses. Review and update your project knowledge periodically.
- **Write clear instructions.** Be specific about what you want. Vague instructions lead to inconsistent results.
- **Name your documents descriptively** (e.g., `Q4-2025-Sales-Report.pdf` not `report.pdf`) and group related files together. Claude uses filenames and proximity to understand relationships between documents.
- **Reference documents by name.** When asking questions, you can mention specific documents to help Claude focus its search: *"Based on our Q3 report, what were the top customer concerns?"*

### 🤔 Lesson Reflection

- What ongoing work could benefit from having a dedicated project with persistent context?
- What documents do you expect you'll be re-uploading or re-explaining to Claude on a regular basis?
- If you're on a team, are there projects that would benefit from shared knowledge and instructions?

---

## Chapter 6: Creating with Artifacts

> 🗂️ **Unit: Organizing Your Work and Knowledge** · ⏱️ Estimated time: 20 minutes

### 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain what artifacts are and when Claude creates them
- Share artifacts with colleagues and publish them publicly
- Troubleshoot common artifact issues

### 🎨 What Are Artifacts?

**Artifacts** are standalone, interactive outputs that Claude creates in a dedicated window alongside your conversation. Instead of getting a long block of code or text buried in the chat, you see your content rendered and ready to use — whether that's a working website, an interactive chart, or a document you can immediately download.

Claude automatically creates an artifact when content meets certain criteria:
- It's **significant and self-contained**, typically over 15 lines
- It's something you're likely to want to **edit, iterate on, or reuse**
- It represents **complex content** that stands on its own without needing the surrounding conversation
- It's content you'll want to **reference or use later**

### 🧰 Common Artifact Types

Claude can create different types of artifacts, each suited to different needs:

| Type | What it's for |
|------|-----------------|
| 📄 **Documents** (markdown & plain text) | Great for anything text-heavy that you'll want to export or continue editing, like meeting notes, reports, project plans, blog posts, and other written content |
| 💻 **Code snippets** | Working code in any programming language — Python, JavaScript, C++, and more. View the code, copy it, or download it to use in your own projects |
| 🌐 **HTML pages** | Complete web pages with HTML, CSS, and JavaScript in a single file. Perfect for landing pages, forms, interactive demos, or quick prototypes |
| 🖼️ **SVG images** | Scalable vector graphics for logos, icons, illustrations, and other visual elements. These render directly in the artifact window so you can see exactly what you're getting |
| 📊 **Mermaid diagrams** | Flowcharts, sequence diagrams, Gantt charts, org charts, and more. Describe the relationships you want to visualize, and Claude will create a diagram you can refine |
| ⚛️ **React components** | Interactive UI elements with real functionality — calculators, dashboards, games, data visualizations. These aren't just mockups; they include actual logic and respond to user input |

> Word documents, Excel spreadsheets, PowerPoint presentations, and PDFs work differently. Claude creates those through a separate **file creation** capability, not as artifacts, and returns them to you as files you can download.

### ✨ Creating Your First Artifact

Creating an artifact is as simple as having a conversation. Just describe what you want, and Claude will determine whether to present it as an artifact. For example, you might say:

- *"Create a flowchart showing our customer onboarding process"* — note: Claude may now generate visual diagrams like flowcharts as HTML using **Imagine**, in addition to code-based artifacts
- *"Build an interactive dashboard that lets me input monthly expenses and see a breakdown"*
- *"Design a landing page for a productivity app with a hero section and feature list"*
- *"Write a project brief template I can reuse for new initiatives"*

If Claude doesn't automatically create an artifact when you expect one, you can explicitly ask: *"Create this as an artifact"* or *"Show me this in an artifact."*

When Claude generates an artifact, it appears in a dedicated window to the right of your conversation. From here, you can:

| Action | What it does |
|--------|---------------|
| **View different formats** | Toggle between a preview (how it looks) and the underlying code |
| **Copy content** | Click the copy icon to grab the content for use elsewhere |
| **Download files** | Save the artifact as a file to your computer |
| **View code** | See exactly what Claude generated under the hood |

### 🔗 Sharing and Publishing Artifacts

Once you've created something useful, you have several options for sharing it:

| Option | Who it's for | How it works |
|--------|----------------|----------------|
| **Copy or download** | Anyone | For personal use or sharing via other channels, use the copy or download buttons in the lower right corner of the artifact window |
| **Share within your organization** | Claude for Work (Team & Enterprise) | The shared artifact stays within your organization and requires team authentication to access |
| **Publish publicly** | Free, Pro, and Max users | Makes the artifact accessible to anyone with the link |

When you publish:
- Only the **selected version** becomes public (your chat remains private)
- **Anyone can view and interact** with the artifact without a Claude account

To publish, click the **"Share"** or **"Publish"** button in the upper right corner of the artifact. You can unpublish at any time by returning to that artifact and removing public access.

> ⚠️ Once published, an artifact is publicly accessible via its link — anyone can view it, even without a Claude account. Published artifacts are **not indexed by search engines**, so they won't appear in Google results.

### 💡 Tips for Getting the Most from Artifacts

- **Be specific about what you want.** *"Build a budget tracker"* is good, but *"Build a monthly budget tracker where I can input expenses by category, see a pie chart breakdown, and get a warning when I'm over budget"* is better.
- **Describe the end user.** Telling Claude who will use the artifact helps it make appropriate design choices. *"This flowchart is for new employees"* leads to different results than *"This flowchart is for the engineering team."*
- **Iterate incrementally.** Ask Claude to add one feature or make one change at a time. This makes it easier to identify what's working and catch issues early.
- **Request artifacts when needed.** If you ask for something substantial and Claude responds in the chat instead of creating an artifact, just say *"Please create that as an artifact."*

### 🤔 Lesson Reflection

- What recurring work could benefit from having an interactive artifact you can reuse?
- Are there processes in your work that would be clearer as a flowchart or diagram?
- What prototype or tool would help you test an idea quickly?

---

## Chapter 7: Working with Skills

> 🗂️ **Unit: Organizing Your Work and Knowledge** · ⏱️ Estimated time: 15 minutes

### 🎯 Learning Objectives

By the end of this lesson, you will be able to:
- Explain what Skills are and how Claude uses them
- Identify Anthropic's built-in Skills for document creation
- Enable and manage Skills in your settings

> 📋 **Plan availability:** Skills are currently a feature preview for **Pro, Max, Team, and Enterprise** plans. If you're on the Free plan, you can read along to understand the concept and skip the hands-on steps.

### 🧩 What Are Skills?

**Skills** are folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. Think of them as **expertise packages** — they teach Claude how to complete specific tasks in a repeatable way.

You've already seen Skills at work if you've used Claude to create Excel spreadsheets, PowerPoint presentations, Word documents, or PDFs — those file creation capabilities are powered by Skills running behind the scenes. But Skills go far beyond document creation: custom Skills can codify entire repeatable workflows — a quarterly variance analysis methodology, a brand voice review process, or a compliance checklist — so Claude follows the same rigorous steps every time.

#### Types of Skills

| Type | Who makes them | How they're used |
|------|------------------|--------------------|
| 🏛️ **Anthropic Skills** | Created and maintained by Anthropic | Enhanced document creation for Excel, Word, PowerPoint, and PDF files. Available to all paid users — Claude invokes them automatically when relevant, no setup needed |
| 🛠️ **Custom Skills** | You or your organization | Built for specialized workflows and domain-specific tasks — e.g. applying brand guidelines to presentations, structuring meeting notes in a specific format, or executing your organization's data analysis workflows |

### ⚙️ Enabling Skills

Skills are currently available as a **feature preview** for users on Pro, Max, Team, and Enterprise plans. To use Skills, you'll need **Code execution and file creation** enabled, since Skills require Claude's secure sandboxed computing environment to function.

1. Navigate to **Settings > Capabilities**
2. Ensure that **Code execution and file creation** is toggled on
3. Scroll to the **Skills** section
4. Toggle individual skills on or off as needed

| Plan | Enabling Skills |
|------|-------------------|
| **Enterprise** | Organization **Owners** must first enable both Code execution and Skills in Admin settings before individual members can access them |
| **Team** | Enabled by **default** at the organization level |

Once enabled, you'll see available Skills listed in your settings, including Anthropic's built-in Skills and any custom Skills you've uploaded.

### 🚀 Using Skills in Practice

The beauty of Skills is that you typically don't need to think about them — Claude handles skill selection automatically based on your request. Examples of prompts that would invoke Skills:
- *"Create an Excel spreadsheet tracking monthly expenses with formulas for totals"*
- *"Turn this meeting notes document into a PowerPoint presentation"*
- *"Generate a PDF report summarizing this data"*
- *"Build a financial model in Excel with scenario analysis"*

When Claude uses a Skill, you'll see it mentioned in Claude's chain of thought as it works. The output will be a downloadable file you can save to your computer or directly to Google Drive.

#### 📁 File Editing

This same capability means Claude can work with your **actual files** (within a contained environment) to create updated versions of them.

> Note: in Chat, Claude creates a **new version** of the document rather than editing the original in place.

Upload slides, spreadsheets, contracts (or any `.xlsx`, `.pptx`, `.docx`, or `.pdf` files) and watch as Claude creates slides, performs analyses, and adds suggested edits. When Claude is done, you can download these files or open them in Drive — e.g. a "Pricing Analysis" spreadsheet, a "Market Research" PDF, a "Pitch Deck" presentation, or a "Food Truck Business" document.

> ⚠️ To use these capabilities you'll need to give Claude access to external data sources — toggle **"Allow limited network access"** on when prompted. This lets Claude install packages and libraries to perform advanced data analysis, custom visualizations, and specialized file processing. Monitor closely, as it **increases security risks**; allowed domains can be managed in Settings.

### 🔒 Security Considerations

Because Skills can include executable code, it's important to use them thoughtfully:
- Only install custom Skills from trusted sources
- Anthropic's built-in Skills are tested and maintained by Anthropic
- Custom Skills you upload are private to your individual account
- If you're installing a custom Skill from an external source, review its contents before use to understand what it does

### 🏗️ Creating Custom Skills

While Anthropic's built-in Skills cover common document creation tasks, the real power of Skills comes from **creating your own**. Custom Skills let you teach Claude your specific workflows, brand guidelines, and ways of working — so Claude can apply that knowledge automatically whenever it's relevant.

The easiest way to create a custom Skill is through **conversation with Claude itself** — you don't need to write code or manually create files; Claude handles the technical structure for you.

| Step | What to do |
|------|-------------|
| 1. **Start a new chat** | Tell Claude what you want to create, e.g. *"I want to create a skill for writing quarterly business reviews"* or *"I need a skill that applies our brand guidelines to presentations."* |
| 2. **Answer Claude's questions** | Claude interviews you about your workflow: What should this skill do? What makes good output for this type of work? Can you give examples of when you'd use this skill? |
| 3. **Upload reference materials** | Templates, style guides, brand assets, or examples of work you're proud of — all help Claude understand exactly what you're looking for |
| 4. **Save your skill** | Claude generates a file containing your properly structured skill. Save it and it's ready for Claude to use |
| 5. **See your skills** | Find the **Customize** tab in the left sidebar — see all skills available to you, and edit them manually or by chatting with Claude |

Your custom Skill will appear in your Skills list alongside Anthropic's built-in Skills. From that point forward, Claude will **automatically invoke it** whenever you work on relevant tasks — no manual triggering needed. You can improve your skills with iteration — ask Claude to edit a skill and it will update the files for you.

### ⚖️ Skills vs. Projects

You might be wondering — if both skills and projects can be used to give more context to Claude, when should I use each? Think of it this way: **projects store knowledge, skills perform tasks.**

- **Projects are knowledge hubs.** They hold the reference materials Claude needs to understand your work — project specs, meeting notes, research documents. When you upload files to a project, Claude draws on that information across every conversation within that project.
- **Skills are procedural machines.** They encode *how* Claude should execute a task — the specific steps, order of operations, and methodology you want followed every time. Skills shine when you have repeatable workflows you want Claude to run consistently.

The two features **complement each other**. A skill can reference knowledge stored in a project — your "customer call prep" skill might pull from customer profiles uploaded to a project's knowledge base. The project provides the **what** (information), the skill provides the **how** (process).

|  | 🗂️ Projects | 🛠️ Skills |
|---|---|---|
| **Purpose** | Store knowledge Claude references | Define processes Claude executes |
| **Best for** | Long-term context, reference materials, team collaboration | Repeatable workflows, multi-step tasks, consistent methodology |
| **Example** | Customer hub, research buddy, feedback generator | Process guidelines (like brand or legal), blog drafting, PDF creation |
| **Persistence** | Knowledge available across all chats in the project | Instructions applied when the skill is invoked |

### 🤔 Lesson Reflection

- What types of documents do you create regularly that could benefit from Claude's built-in Skills?
- Are there repetitive workflows in your work that might be good candidates for custom Skills?
- How might Skills change the way you think about document creation and data analysis?

---

<!-- Add new lectures below this line -->
