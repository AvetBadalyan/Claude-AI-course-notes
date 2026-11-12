[⬅ Back to course index](../README.md)

# 📚 Introduction to Model Context Protocol — Course Notes

> Builds on [Claude 101](../claude-101/README.md) (Ch 8 "Connecting Your Tools" — connectors) and [Claude Code 101](../claude-code-101/README.md) (Ch 11 "MCP"). This course goes under the hood: what MCP solves, how **clients** and **servers** work, and how to build both with **tools**, **resources**, and **prompts**.

### 🗺️ Course Map

| Unit | Chapters | Status |
|------|----------|:------:|
| 🗂️ **Introduction** | [Ch 1: Introducing MCP](#chapter-1-introducing-mcp) · [Ch 2: MCP Clients](#chapter-2-mcp-clients) · [Background: What Is MCP?](#-background-what-is-the-model-context-protocol-mcp) | 🚧 |
| 🗂️ **Hands-on with MCP Servers** | Ch 3: Project Setup · Ch 4: Defining Tools with MCP · Ch 5: The Server Inspector | 🔲 |
| 🗂️ **Connecting with MCP Clients** | Ch 6: Implementing a Client · Ch 7: Defining Resources · Ch 8: Accessing Resources · Ch 9: Defining Prompts · Ch 10: Prompts in the Client | 🔲 |
| 🗂️ **Assessment and Wrap Up** | Ch 11: MCP Review | 🔲 |
| 🗂️ **Quiz** | Final assessment on MCP | 🔲 |

> _Two lessons have no chapter of their own: **"Welcome to the course"** (an intro video; its course-goals slide is summarized in the Introduction below) and the **"Course satisfaction survey"** (a feedback form with no learning content)._

> **Annotation guide for these notes:** 📌 = my own reading from screenshots/context — **not stated in the lesson text itself**. 🔗 = my cross-reference between chapters — **my mapping, not the lesson's wording**. For exam prep, focus on the **📝 Quick Reference** tables and **Key features for exam** bullet lists at the end of each chapter.

---

> 🗂️ **Unit 1: Introduction** · Background reading

## 📖 Background: What Is the Model Context Protocol (MCP)?

> 📎 *Source: the official MCP docs ("What is the Model Context Protocol?"), supplied as background reading for the Introduction unit. It is not one of the course's lesson videos, and it was cross-checked against the live docs.*

### 🧠 Key Takeaways

- **MCP** (Model Context Protocol) is an **open-source standard** for **connecting AI applications to external systems**
- With MCP, AI applications like **Claude** or **ChatGPT** can connect to:
  - **Data sources** — e.g. local files, databases
  - **Tools** — e.g. search engines, calculators
  - **Workflows** — e.g. specialized prompts
- …so they can **access key information and perform tasks**
- **Analogy:** MCP is like a **USB-C port for AI applications**. USB-C is a standardized way to connect electronic devices; MCP is a **standardized way to connect AI applications to external systems**

![Diagram: AI applications on the left (Chat interface: Claude Desktop, LibreChat · IDEs and code editors: Claude Code, Goose · Other AI applications: 5ire, Superinterface) connect through "MCP — Standardized protocol" in the middle, with bidirectional data flow, to data sources and tools on the right (Data and file systems: PostgreSQL, SQLite, GDrive · Development tools: Git, Sentry · Productivity tools: Slack, Google Maps)](assets/L0-what-is-mcp/mcp-standardized-protocol.webp)

> 📌 *From the diagram:* MCP sits **in the middle** with **two-way (bidirectional) data flow** on both sides. The **left** column is the **AI applications** (clients' side) and the **right** column is the **data sources and tools** (servers' side). The product names are examples shown in the picture (my reading).

### 🔌 What Can MCP Enable?

| Example |
|---------|
| 📅 **Agents** can access your **Google Calendar** and **Notion**, acting as a more personalized AI assistant |
| 🎨 **Claude Code** can generate an **entire web app from a Figma design** |
| 🏢 **Enterprise chatbots** can connect to **multiple databases** across an organization, so users can analyze data through chat |
| 🧊 **AI models** can create **3D designs in Blender** and print them on a **3D printer** |

### 🎯 Why Does MCP Matter?

| Who | Benefit |
|-----|---------|
| 👩‍💻 **Developers** | MCP **reduces development time and complexity** when building or integrating with an AI application or agent |
| 🤖 **AI applications / agents** | Access to an **ecosystem of data sources, tools, and apps**, which enhances their capabilities and improves the end-user experience |
| 🙋 **End-users** | **More capable** AI applications or agents that can **access user data and take actions on the user's behalf** when necessary |

> 🔗 Same "**USB-C for AI**" idea as [Claude 101, Ch 8](../claude-101/README.md) (where MCP powers **connectors**) and the **external tools and data sources** definition in [Claude Code 101, Ch 11](../claude-code-101/README.md) (my mapping).

> 🎓 **Memory tip:** **MCP = USB-C for AI.** One standard plug, many apps on one side and many tools/data on the other.

---

> 🗂️ **Unit 1: Introduction** · Welcome to the course (no chapter)

## 🎯 Course Goals

> 📌 *From the "Course goals" slide in the Welcome video (the lesson has no text, so this is my reading of the slide, not lesson wording).* It's a handy map of the whole course.

| Goal | Meaning | Covered in |
|------|---------|-----------|
| 🔭 **Overview of MCP** | Understand **what problems MCP solves** | Ch 1 |
| 🔌 **MCP Clients and Servers** | **Servers host resources, tools, and more. Clients use servers** | Ch 1-2, Ch 6 |
| 🛠️ **Tools** | Tools are **implemented on a server** and **extend an LLM's capabilities** | Ch 4 |
| 📄 **Resources** | Servers can deliver **any kind of document or information** to clients | Ch 7-8 |
| 💬 **Prompts** | Servers can provide clients with **pre-optimized prompts** | Ch 9-10 |

> 🔗 The "Covered in" column maps each goal to the Course Map chapters (my mapping).

> 🎓 **Memory tip:** servers offer **T-R-P** (**T**ools · **R**esources · **P**rompts); **clients use** them.

---

> 🗂️ **Unit 1: Introduction** · Chapter 1

## Chapter 1: Introducing MCP

> **Model Context Protocol (MCP)** is a **communication layer** that provides Claude with **context and tools** *without* requiring you to write a bunch of tedious **integration code**. Think of it as a way to **shift the burden of tool definitions and execution** away from your server to **specialized MCP servers**.

### 🧠 Key Takeaways

- MCP is a **communication layer** that gives Claude **context and tools** without you writing integration code
- It **moves tool definitions and execution** from **your server** to dedicated **MCP servers**
- **Architecture:** an **MCP Client** (inside *your* server) connects to **MCP Servers**; each server contains **tools, prompts, and resources** and is an **interface to some outside service**
- **Anyone can author an MCP server**; service providers often publish **official** ones (e.g. AWS)
- **MCP vs. calling an API directly:** with MCP the **tool schemas and functions are already defined for you**
- **MCP vs. tool use:** they are **complementary, not the same**. The difference is **who does the work**

---

### 🏗️ The Basic Architecture

When you first meet MCP you'll see this diagram:

![Architecture diagram: inside "Our Server" sits an MCP Client, which connects to two MCP Servers; each MCP Server contains Tools, Prompts, and Resources, and each connects to its own Outside Service](assets/L1-introducing-mcp/mcp-architecture.png)

| Piece | What it is |
|-------|------------|
| 🖥️ **Our Server** | **Your** application. It contains the **MCP Client** |
| 🔌 **MCP Client** | The part of your server that **connects to MCP servers** |
| 🗄️ **MCP Server** | An **interface to an outside service**. It holds **tools, prompts, and resources** |
| 🌐 **Outside Service** | The real service behind the server (e.g. GitHub) |

> 🔗 The three things inside an MCP server (**tools, prompts, resources**) are exactly what the later hands-on lessons build one by one (Ch 4, Ch 7, Ch 9) (my mapping).

---

### 😓 The Problem MCP Solves

**Example app:** a chat interface where users ask Claude about their **GitHub data**. A user asks: *"What open pull requests are there across all my repositories?"* To answer, Claude needs **tools to access GitHub's API**.

![Slide "Sample App": a chat interface using an LLM with tools that can access a user's GitHub account; the user asks "What open pull requests are there across all my repositories?" and the AI reply is "…"](assets/L1-introducing-mcp/sample-app.png)

GitHub has **massive functionality**: repositories, pull requests, issues, projects, and more. **Without MCP**, you must create an **incredible number of tool schemas and functions** to cover it.

![Slide "Tool Functions": "Our Server" contains many tools, each with a schema and a function: get_repos(), list_repos(), create_repos(), search_issues(), update_issue(), create_issue(), get_issue(), create_file(). Caption: all of this is code that we (developers) have to write, test, and maintain](assets/L1-introducing-mcp/tool-functions.png)

> ⚠️ **That's code *you* have to write, test, and maintain**: a lot of effort and an ongoing maintenance burden.

> 📌 *From the slide:* each tool is drawn as a **schema + function pair**. The tool names shown (`list_repos`, `create_repos`, `search_issues`, `update_issue`, `create_issue`, `get_issue`, `create_file`) are slide examples. The lesson text itself only names `get_repos()` (my reading).

| | ❌ **Without MCP** | ✅ **With MCP** |
|---|---|---|
| **Who writes the GitHub tools?** | **You** (schemas + functions) | A **GitHub MCP server** |
| **Where do tools live?** | **Your server** | The **MCP server** |
| **Your maintenance burden** | **High**, ongoing | **Low**, you just connect |

---

### ⚙️ How MCP Works

MCP **shifts this burden** by moving **tool definitions and execution** from your server to a dedicated **MCP server**. Instead of authoring all the GitHub tools yourself, an **MCP Server for GitHub** handles it.

![Slide "Model Context Protocol": it shifts the burden of tool definitions and execution onto MCP Servers. "Our Server" holds a get_repos() tool (schema + fn) with two-way arrows to an empty "MCP Server" box and to Claude](assets/L1-introducing-mcp/mcp-shifts-burden.png)

- The MCP server **wraps up tons of functionality** around GitHub and exposes it as a **standardized set of tools**
- Your application **connects to that MCP server** instead of implementing everything from scratch

---

### 🗄️ MCP Servers Explained

**MCP Servers provide access to data or functionality implemented by outside services.** They are specialized interfaces that expose **tools, prompts, and resources** in a **standardized** way.

![Slide "MCP Servers": MCP Servers provide access to data or functionality implemented by some outside service. "Our Server" talks two ways to an "MCP Server for Github", which contains a get_repos() tool (schema + fn) that calls Github; Claude sits below Our Server](assets/L1-introducing-mcp/mcp-server-github.png)

In the GitHub example:
- The **MCP Server for GitHub** contains tools like **`get_repos()`**
- It **connects directly to GitHub's API**
- **Your server talks to the MCP server**, which handles **all the GitHub-specific implementation details**

---

### ❓ Common Questions

| Question | Answer |
|----------|--------|
| **Who authors MCP servers?** | **Anyone.** Often the **service providers themselves** publish **official** MCP servers (e.g. **AWS** might release one with tools for its services) |
| **How is this different from calling APIs directly?** | MCP servers give you **tool schemas and functions already defined**. Calling an API directly means **you author those tool definitions yourself**. MCP saves that work |
| **Isn't MCP just the same as tool use?** | **No, a common misconception.** They're **complementary but different**: **MCP servers** provide **tool schemas + functions already defined for you**; **tool use** is **how Claude actually calls those tools**. The key difference is **who does the work**: with MCP, **someone else has already implemented the tools** |

> 💡 **The benefit:** instead of maintaining a complex set of integrations yourself, you use MCP servers that **handle the heavy lifting** of connecting to external services.

---

### 🔁 Recap

**MCP** is a **communication layer**. Your server's **MCP client** connects to **MCP servers** (each wrapping an outside service and exposing **tools, prompts, and resources**), so **you don't write and maintain the integration code**. MCP is **not** the same as tool use. They work together.

### 📝 Quick Reference: Introducing MCP (for exam prep)

| Concept | Key point |
|---------|-----------|
| 🔌 **MCP** | **Communication layer** giving Claude **context + tools** without custom integration code |
| 🎯 **Core idea** | **Shifts the burden** of tool definitions + execution **from your server to MCP servers** |
| 🖥️ **MCP Client** | Lives **in your server**; connects to MCP servers |
| 🗄️ **MCP Server** | Interface to an **outside service**; exposes **tools, prompts, resources** |
| 👥 **Authors** | **Anyone**; service providers often make **official** servers (e.g. AWS) |
| ⚖️ **vs. direct API calls** | MCP: schemas/functions **already defined**. Direct API: **you** author them |
| ⚖️ **vs. tool use** | **Complementary, not the same**. MCP = *who provides* the tools; tool use = *how Claude calls* them |

> 🎓 **Memory tip:** **"MCP = someone else already wrote the tools."** Flow: **Your server (MCP client) → MCP server (tools · prompts · resources) → Outside service.**

**Key features for exam:**
- **MCP** = a **communication layer** that gives Claude **context and tools** without you writing integration code.
- It **moves tool definitions and execution** from your server to **MCP servers**.
- An **MCP client** (in your server) connects to **MCP servers**; each server holds **tools, prompts, and resources** and fronts an **outside service**.
- **Anyone** can write an MCP server; **service providers often publish official ones**.
- MCP servers come with **tool schemas and functions already defined**; calling an API directly means **you write them**.
- **MCP ≠ tool use**: they're **complementary**. The difference is **who does the work** (with MCP, someone else already implemented the tools).

---

> 🗂️ **Unit 1: Introduction** · Chapter 2

## Chapter 2: MCP Clients

> The **MCP client** is the **communication bridge** between **your server** and **MCP servers**. It is your **access point to all the tools** an MCP server provides, and it handles the **message exchange and protocol details** so your application doesn't have to.

### 🧠 Key Takeaways

- The **MCP client** = the **bridge** between your server and MCP servers; it **hides protocol details**
- MCP is **transport agnostic**: client and server can talk over **different protocols**
- **Most common setup:** client and server on the **same machine**, talking via **standard input/output (stdio)**
- Other transports: **HTTP**, **WebSockets**, and various network protocols
- The **two main message types** you work with:
  - **`ListToolsRequest` / `ListToolsResult`**: "what tools do you provide?"
  - **`CallToolRequest` / `CallToolResult`**: "run this tool with these arguments"
- These messages are **defined in the MCP specification**

---

### 🔀 Transport Agnostic Communication

**Transport agnostic** = the client and server can communicate over **different protocols**, depending on your setup.

![Slide "Transport Agnostic": inside "Our Server" the MCP Client has a two-way link labeled "Standard IO" to an "MCP Server for Github" marked "Running locally"](assets/L2-mcp-clients/transport-standard-io.png)

![Slide "MCP Client": the same layout, but the two-way link between the MCP Client and the MCP Server for Github is labeled "Websockets"](assets/L2-mcp-clients/transport-websockets.png)

| Transport | When / note |
|-----------|-------------|
| 💻 **Standard I/O (stdio)** | **Most common.** Client and server run on the **same machine** (server "running locally") |
| 🌐 **HTTP** | Connect over the network |
| 🔌 **WebSockets** | Connect over the network (shown in the slide) |
| ➕ **Other network protocols** | Also possible |

> 📌 *From the slides:* the link is drawn **two-way** (arrow on both ends) in both pictures, and only the label changes (**Standard IO** vs **Websockets**). That is the "transport agnostic" point (my reading).

---

### 📨 MCP Message Types

Once connected, client and server exchange **specific message types** defined in the **MCP specification**.

| Message pair | Direction | Meaning |
|--------------|-----------|---------|
| 📋 **`ListToolsRequest`** → **`ListToolsResult`** | Client asks, server answers | "Give me a list of tools you provide" → "Here are the tools I can run" |
| ▶️ **`CallToolRequest`** → **`CallToolResult`** | Client asks, server answers | "Please run a particular tool with these arguments" → "Here's the result of the tool run" |

![Slide "MCP Communication": the MCP Client inside Our Server sends ListToolsRequest ("Give me a list of tools you provide") to the MCP Server for Github and gets back ListToolsResult ("Here are the tools I can run")](assets/L2-mcp-clients/list-tools-messages.png)

![Slide "MCP Communication": the MCP Client sends CallToolRequest ("Please run a particular tool with these arguments") to the MCP Server for Github and gets back CallToolResult ("Here's the result of the tool run")](assets/L2-mcp-clients/call-tool-messages.png)

---

### 🔄 The Full Flow

**Example:** a user asks *"What repositories do I have?"* The query travels through **your server → MCP client → MCP server → GitHub** and back through **Claude**.

![Sequence diagram with six columns: User, Our Server, MCP Client, MCP Server, Claude, Github. Steps: user asks "What repositories do I have?"; server says "I need a list of tools to send to Claude"; ListToolsRequest/ListToolsResult between client and MCP server; "Query + Tools" sent to Claude; Claude replies ToolUse; server says "Please run this tool with these args"; CallToolRequest to MCP server, which sends a request to Github; Github responds; CallToolResult returns to the server; toolResult sent to Claude; Claude answers "Your repositories are…" back to the user](assets/L2-mcp-clients/full-flow-sequence.png)

| # | Step | What happens |
|:-:|------|--------------|
| 1 | **User Query** | The user submits the question to **your server** |
| 2 | **Tool Discovery** | Your server needs to know **which tools are available** to send to Claude |
| 3 | **List Tools Exchange** | Your server asks the **MCP client** for the available tools |
| 4 | **MCP Communication** | The MCP client sends **`ListToolsRequest`** to the MCP server and receives **`ListToolsResult`** |
| 5 | **Claude Request** | Your server sends the **user's query + the available tools** to Claude |
| 6 | **Tool Use Decision** | **Claude decides** it needs to call a tool (**`ToolUse`**) |
| 7 | **Tool Execution Request** | Your server asks the **MCP client** to run the tool Claude specified |
| 8 | **External API Call** | The MCP client sends **`CallToolRequest`** to the MCP server, which makes the **actual GitHub API call** |
| 9 | **Results Flow Back** | GitHub responds; the data flows back through the MCP server as a **`CallToolResult`** |
| 10 | **Tool Result to Claude** | Your server sends the **tool result** (**`toolResult`**) back to Claude |
| 11 | **Final Response** | Claude **formulates the final answer** using the repository data |
| 12 | **User Gets Answer** | Your server **delivers Claude's response** to the user |

> 💡 Many steps, but **each component has a clear responsibility**. The MCP client **abstracts away server communication**, so you focus on **application logic**.

> 📌 *From the diagram:* the two labels in tan boxes, **`ToolUse`** (Claude → your server) and **`toolResult`** (your server → Claude), are the **Claude-side** messages. The brown boxes (**`ListTools…`**, **`CallTool…`**) are the **MCP-side** messages (my reading).

> 🔗 Steps 5, 6, 10, 11 are the normal **tool use loop** from earlier courses; MCP only changes **where the tools come from (step 3-4)** and **who runs them (step 7-9)** (my mapping).

---

### 🔁 Recap

The **MCP client** sits in your server and talks to MCP servers over **any transport** (usually **stdio** locally). It uses **`ListTools`** to discover tools and **`CallTool`** to run them, while your server shuttles **tools + results** to and from **Claude**.

### 📝 Quick Reference: MCP Clients (for exam prep)

| Concept | Key point |
|---------|-----------|
| 🔌 **MCP client** | **Bridge** between your server and MCP servers; handles **message exchange + protocol details** |
| 🔀 **Transport agnostic** | Client and server can use **different protocols** |
| 💻 **Most common transport** | **Standard input/output**, both on the **same machine** |
| 🌐 **Other transports** | **HTTP**, **WebSockets**, other network protocols |
| 📋 **List tools** | **`ListToolsRequest`** → **`ListToolsResult`** |
| ▶️ **Call tool** | **`CallToolRequest`** → **`CallToolResult`** |
| 📜 **Where messages are defined** | The **MCP specification** |
| 🤖 **Who decides to use a tool** | **Claude** (your server then asks the client to run it) |
| 🌍 **Who calls the external API** | The **MCP server** (e.g. GitHub), not the client |

> 🎓 **Memory tip:** **"List, then Call."** First **List** tools (so Claude knows them), then **Call** the one Claude picks. The client is just the **messenger**; the **MCP server** does the real work.

**Key features for exam:**
- The **MCP client** is the **communication bridge** between your server and MCP servers.
- MCP is **transport agnostic**: **stdio** (most common, same machine), **HTTP**, **WebSockets**, others.
- **`ListToolsRequest` / `ListToolsResult`**: ask for and receive the **available tools**.
- **`CallToolRequest` / `CallToolResult`**: ask to **run a tool with arguments** and receive its **result**.
- Flow: **list tools → send query + tools to Claude → Claude requests tool use → client calls tool on MCP server → result back to Claude → final answer to user**.
- The **MCP server** makes the **actual external API call** (e.g. GitHub).
