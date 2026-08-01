# TIL: Understanding Model Context Protocol (MCP)

**Date:** August 1, 2026

## What is MCP?

Today I learned about **Model Context Protocol (MCP)**.

In simple terms:

> **MCP is a standard protocol that allows AI models to communicate with external tools, APIs, databases, local files, and other services.**

It acts as a bridge between an AI model and external resources.

---

## How MCP Works

```text
User
   │
   ▼
AI Model
   │
   ▼
MCP Server
   ├── GitHub
   ├── Database
   ├── Weather API
   ├── Local Files
   └── Custom Services
```

The flow is simple:

1. A user asks the AI a question.
2. The AI determines which tool it needs.
3. The AI calls the appropriate tool through the MCP server.
4. The MCP server communicates with the required resource.
5. The result is returned to the AI.
6. The AI responds to the user.

---

## API vs MCP

### REST API

```text
Frontend
   │
   ▼
REST API
   │
   ▼
Database / External Services
```

### MCP

```text
AI
   │
   ▼
MCP Server
   │
   ▼
Tools
   │
   ▼
Database / APIs / Files / Services
```

The main difference is:

* REST APIs expose **HTTP endpoints**.
* MCP exposes **AI tools**.

For example:

Instead of:

```http
GET /weather
GET /users
POST /issues
```

You expose tools such as:

```text
getWeather()
getUsers()
createIssue()
```

The business logic can remain the same—the interface changes.

---

## Key Components

### Tools

Functions that the AI can execute.

Examples:

* `getWeather()`
* `createIssue()`
* `readFile()`

### Resources

Data that AI can read.

Examples:

* Local files
* Documents
* Database records

### Prompts

Reusable prompt templates that can be shared with AI clients.

---

## My Understanding

The easiest way for me to understand MCP is:

> **The AI decides what needs to be done, while the MCP server executes that request by communicating with the appropriate tools and resources.**

---

## Next Steps

I'm planning to learn MCP by building practical projects:

* [ ] Basic MCP Server
* [ ] File System MCP
* [ ] GitHub MCP
* [ ] Weather MCP
* [ ] Database MCP
* [ ] Multi-Server MCP

---

## Takeaway

MCP is **not a replacement for REST APIs**.

Instead, it provides a **standard interface** that allows AI applications to use your existing tools, APIs, databases, and services without requiring custom integrations for every AI platform.

**Learning by building is the best way to understand MCP, so my next step is to create practical MCP projects and document the journey.**
