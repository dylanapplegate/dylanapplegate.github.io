---
title: "Building a Local-First, AI-Powered CLI Task Manager"
date: 2025-03-21
description: "How I built a CLI-based productivity assistant using TypeScript, Prisma, Docker, and LM Studio"
tags: [TypeScript, CLI, AI, Prisma, LM Studio, Productivity]
---

Over the past few days, I’ve been building a project that reflects both how I work and how I _want_ to work: **intentionally, locally, and with just enough automation** to stay focused.

This is just the beginning — and it only took a day to get the first working version. My long-term goal is to turn this into a **full LM-powered personal agent** that helps me land a job or secure paid freelance work.

### 🚀 What I Built

[`my-project-manager`](https://github.com/dylanapplegate/my-project-manager) is a **local-first, intelligent CLI-based task manager** designed to help developers (like me) stay grounded and goal-aware — even while offline.

At its core, it's a task tracker with AI-powered suggestions. But more than that, it’s the first step in building a **CLI-native personal productivity agent**.

If you're curious about where this project is going, check out the [full roadmap](https://github.com/dylanapplegate/my-project-manager/blob/main/roadmap.md) — it outlines the evolution from CLI utility to AI-powered assistant.

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

### 📊 Testing and Reliability

- 7 CLI commands and modules are fully unit tested with mocks for both **Prisma** and **LM Studio**
- Edge cases like invalid inputs, empty task lists, and AI errors are covered
- Tests run fast thanks to mocked databases and models

This isn’t a throwaway tool — it’s production-grade even in its CLI form.

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

---

### 🔗 Try It or Star It

To get started quickly:

```bash
git clone https://github.com/dylanapplegate/my-project-manager
cd my-project-manager
nvm use          # Sets Node.js version from .nvmrc
npm install
docker-compose up -d  # Starts PostgreSQL
npm start             # Runs the CLI
```

If you don’t want to install `tsx` globally, you can still run commands like:

```bash
npm start -- add "Write blog post" -d 2025-03-22
```

👉 [View full setup in README](https://github.com/dylanapplegate/my-project-manager#readme)

---

This project reflects how I want to build software: **thoughtful, testable, local-first, and empowering**. If you're interested in this kind of work — let's connect!
