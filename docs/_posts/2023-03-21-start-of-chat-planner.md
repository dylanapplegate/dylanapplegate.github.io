---
title: "Building a Local-First, AI-Powered CLI Task Manager"
date: 2025-03-21
description: "How I built a CLI-based productivity assistant using TypeScript, Prisma, Docker, and LM Studio"
tags: [TypeScript, CLI, AI, Prisma, LM Studio, Productivity]
---

I’m building a local-first, AI-powered CLI productivity agent — one that’s purpose-built for developers, job seekers, and indie hackers who want to work with intention and without cloud dependencies.

The current version is just the seed of a much bigger vision: a personal AI assistant that understands your goals, suggests the most impactful task, and evolves to support job hunting, content creation, learning, and reflection — all running locally, with full privacy and no SaaS friction.

It’s the productivity system I’ve always wanted: fast, grounded, offline, and extensible.

---

### 🚀 What I Built

[`my-project-manager`](https://github.com/dylanapplegate/my-project-manager) is a **local-first, intelligent CLI-based task manager** — and the first building block in a much larger system.

At its core, it’s a task tracker with AI-powered prioritization. But over time, it will become a **goal-aware, locally hosted productivity agent** — supporting workflows like LeetCode, blogging, GitHub contributions, LinkedIn content, and even weekly reviews. All offline. All under your control.

---

### 🔧 Tech Stack

- **TypeScript** for type safety and fast iteration
- **Prisma + PostgreSQL** for managing task data
- **Docker + Docker Compose** for local dev
- **LM Studio SDK** for running AI models locally
- **Commander.js** for intuitive CLI commands
- **Jest** for 98%+ test coverage
- `.nvmrc` for consistent Node.js versioning (`v23.9.0`)
- `tsx` for executing ES module CLI commands

---

### 🧩 CLI Commands

```bash
# Add a task
my-task-manager add "Write blog post" -d 2025-03-22

# List tasks
my-task-manager list            # pending
my-task-manager list --completed

# Mark task complete
my-task-manager complete 3

# Get smart suggestion
my-task-manager suggest
```

### 🛠 CLI Commands Overview

| Command                                    | Description                          |
| ------------------------------------------ | ------------------------------------ |
| `my-task-manager add "Task"`               | Adds a new task                      |
| `my-task-manager add "Task" -d 2025-03-22` | Adds a task with a due date          |
| `my-task-manager list`                     | Lists all pending tasks              |
| `my-task-manager list --completed`         | Lists completed tasks                |
| `my-task-manager complete 3`               | Marks task #3 as completed           |
| `my-task-manager suggest`                  | Suggests the next best task using AI |

The `suggest` command is where things get interesting: it queries the last 5 completed tasks and top 5 pending ones, then uses a local LM Studio model to recommend a single high-impact task. This happens entirely offline.

---

### 🧠 How AI Suggestions Work

The core logic is in `getTaskSuggestion()`, which:

- Formats completed and pending tasks as prompt input
- Sends a system prompt to the local LM Studio model
- Asks the model to pick _one next best task_ based on urgency, goals, and dependencies
- Returns the AI-generated recommendation directly to the terminal:

```bash
🤖 AI Suggestion: Next Task: Finalize CLI tests
Reasoning: You've completed related features, and this task ensures stability before expanding further.
```

It's not just cute — it helps me avoid decision fatigue and maintain momentum.

---

### 🔮 Why This Matters

Most productivity tools feel like bolt-ons or spreadsheets with a UI. I’m aiming to build something different — something _personal_.

This project is meant to evolve into a trusted co-pilot: a task manager that not only tracks work, but understands your priorities, pace, and patterns. One that surfaces meaningful tasks without cloud lock-in, and grows with your goals.

It’s open source, offline-first, and designed for the way real developers think.

---

### 📊 Testing and Reliability

- 7 CLI commands and modules are fully unit tested with mocks for both **Prisma** and **LM Studio**
- Edge cases like invalid inputs, empty task lists, and AI errors are covered
- All external services (DB and AI models) are mocked, making tests fast, deterministic, and offline-capable
- Tests run fast thanks to mocked databases and models, with over 98% total test coverage including edge cases, database errors, and AI failures

This isn’t a throwaway tool — it’s production-grade even in its CLI form. The test suite makes sure it stays that way as features grow.

---

### 🤖 On AI-Assisted Development

While building this project, I adopted a hybrid workflow that combined traditional coding with [**vibe coding**](https://en.wikipedia.org/wiki/Vibe_coding) — a technique where AI tools (like custom GPTs or coding copilots) assist in code generation through natural-language prompts. This method allowed me to move faster during prototyping and automate repetitive boilerplate logic.

But make no mistake: a large portion of the system was crafted through deliberate, manual engineering. Every AI-assisted section was reviewed, tested, and refined with care. I leaned on automation where it made sense — but always with a human in the loop to ensure clarity, correctness, and long-term maintainability.

All of the tests, in particular, were written manually — not generated — to ensure complete clarity and intentional coverage.

This blended approach reflects my philosophy toward modern software development: use the best tools available, but never lose sight of the craft.

---

### 🛣️ The Road Ahead

This CLI is just **Phase 1**. Here’s where the project is headed next:

#### 🧭 Phase 2: Goal-Based Workflows

Introduce semantic filters and flows for common developer goals:

- **LeetCode practice**: Track problems solved, prioritize topics
- **Blogging & publishing**: Draft planning, deadlines, submissions
- **LinkedIn post planning**: Schedule meaningful posts, track engagement
- **GitHub contributions**: Tie tasks to repos, track issue-based progress

#### 🖥️ Phase 3+: Full Personal Productivity Agent

- **Local web dashboard** (React-based) for visual task management
- **Bi-directional sync** between CLI and UI
- **Long-term AI context** using vector memory
- **Custom prioritization models** for multi-goal planning

Ultimately, I want this to evolve into a **personal productivity agent for developers, job seekers, and indie builders** — one that knows your goals, works offline, and keeps you focused on what truly matters. If it works, it won't just track tasks — it'll help me **earn income** and **regain financial stability**.

Want to follow along? The GitHub roadmap is where I’m tracking every phase — from goal-based workflows to AI memory and reflection tools. There’s a lot coming.

---

### 🔗 Try It Locally (or Star It for Later)

To get started quickly:

```bash
git clone https://github.com/dylanapplegate/my-project-manager
cd my-project-manager
nvm use          # Sets Node.js version from .nvmrc
npm install
docker-compose up -d  # Starts PostgreSQL
# Make sure you have a .env file with DATABASE_URL set
npm start             # Runs the CLI
```

If you don’t want to install `tsx` globally, you can still run commands like:

```bash
npm start -- add "Write blog post" -d 2025-03-22
```

👉 [View full setup and usage instructions in the README](https://github.com/dylanapplegate/my-project-manager#readme)

### 🛠️ Installation Notes

This project uses a `.nvmrc` file to pin Node.js to version v23.9.0. If you're using `nvm`, run:

```bash
nvm use
```

If you're not using `tsx` globally, you can still run commands using:

```bash
npm start -- <command>
```

For example:

```bash
npm start -- add "Write blog post" -d 2025-03-22
```

### 🧠 Setting Up LM Studio

To use the AI suggestion feature, you need to have [LM Studio](https://lmstudio.ai/) installed and running locally with a compatible model loaded.

Recommended setup:

1. **Download and install LM Studio** from [https://lmstudio.ai/](https://lmstudio.ai/).
2. **Open LM Studio**, go to the "Models" tab, and download a compatible chat model such as `gemma:3-4b-it` or any local LLM that supports system + user prompts.
3. Once downloaded, click **"Start Chat Server"**.
4. Ensure LM Studio is running in the background while using the CLI.

The CLI will send prompt text directly to LM Studio's local HTTP server. No cloud interaction required.

Otherwise, install `tsx` globally and use the CLI directly:

```bash
npm install -g tsx
npm link
my-task-manager add "Write blog post" -d 2025-03-22
```
