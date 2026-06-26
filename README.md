# Tasklipi

**AI-powered personal task manager with smart planning, streak tracking, and multi-gateway payments.**

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://python.org)
[![Flask](https://img.shields.io/badge/framework-Flask-green.svg)](https://flask.palletsprojects.com)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/deploy-Docker-2496ED.svg)](https://docker.com)

---

## What is Tasklipi?

Tasklipi is a **full-stack personal task management platform** that combines traditional daily task tracking with AI-powered planning. It helps users organize their day, track streaks, and generate smart task plans using large language models.

The backend is a single-file Flask application with a mobile-first SPA frontend. The platform supports multiple AI providers, a multi-gateway payment system for premium features, and timezone-aware streak scheduling.

---

## Key Features

### Task Management
- **Daily tasks** with add/edit/delete, reorder, and completion tracking
- **AI Task Planner** — generates a full day plan from a high-level goal using LLMs
- **Per-task streak tracking** — monitor consistency on individual tasks (🔥 streak counter)
- **Overall streak system** — timezone-aware daily reset, longest streak tracking
- **Planned tasks** — organize tasks by time blocks (Morning, Afternoon, Evening)

### AI Integration
- **Multi-provider support**: OpenAI, Anthropic (Claude), Google Gemini, DeepSeek, Groq, OpenRouter
- **Smart task planning** — generates structured plans with categories and time estimates
- **AI model selection** — user-configurable provider + model per account
- **Automatic fallback** — retries with exponential backoff across providers

### Payment System
- **Multi-gateway support**: Razorpay, PhonePe, Paytm, PayU, UPI (via QR)
- **Subscription plans** — monthly/yearly with AI usage allocation
- **AI balance top-up** — pay-as-you-go for AI features
- **HMAC-signed activation** — secure server-to-server payment verification
- **India/non-India pricing** — region-aware billing

### Streak Scheduler
- **Background worker** — runs every 60s, processes users by timezone
- **Atomic SQL updates** — prevents race conditions between scheduler and inline handlers
- **Server-downtime recovery** — automatically catches up missed days on restart
- **Per-user timezone** — saves browser timezone on login, defaults to Asia/Kolkata

### Frontend
- **Single-page application** — all JS/CSS inline, no build step, no bundler
- **Mobile-first design** — bottom toolbar, `visualViewport` keyboard handling
- **Account dashboard** — profile, preferences, AI model config, timezone settings
- **Shared accounts** — monitor mode for parents/kids
- **Dark/light mode**

---

## Architecture

```
┌─────────────────────────────────────────────┐
│              Client (Browser)                │
│  ┌───────────────────────────────────────┐   │
│  │     SPA Frontend (static/index.html)  │   │
│  │     ~13,200 lines — inline JS/CSS     │   │
│  └──────────────┬────────────────────────┘   │
│                 │ REST API + HTML             │
│                 │ X-LF-Token auth             │
├─────────────────┼───────────────────────────┤
│  Flask Backend  │                             │
│  ┌──────────────▼────────────────────────┐   │
│  │         app.py (~9,500 lines)         │   │
│  │  • Auth (OTP, sessions, tokens)       │   │
│  │  • Task CRUD + AI planning            │   │
│  │  • Streak engine + scheduler          │   │
│  │  • Payment verification               │   │
│  │  • User management + billing          │   │
│  │  • File upload / media serving        │   │
│  └──────────────┬────────────────────────┘   │
│                 │                             │
│  ┌──────────────▼────────────────────────┐   │
│  │      SQLite Database                   │   │
│  │  • Users, tasks, daily_tasks           │   │
│  │  • Subscriptions, ai_ledger            │   │
│  │  • Sessions, promo_codes               │   │
│  │  • Auto-migrates on startup            │   │
│  └───────────────────────────────────────┘   │
│                                              │
│  ┌───────────────────────────────────────┐   │
│  │   Landing Server (landing/app.py)     │   │
│  │   • Payment page (tasklipi.com)       │   │
│  │   • Razorpay / PhonePe / Paytm / PayU │   │
│  │   • HMAC → activation callback        │   │
│  └───────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

### Tech Stack

| Layer | Technology |
|:---|:---|
| Backend | Python 3.9+, Flask, Flask-Compress |
| Database | SQLite (auto-migration) |
| Frontend | Vanilla JS SPA (inline, no build) |
| Auth | OTP-based login, session tokens |
| AI Providers | OpenAI, Anthropic, Gemini, DeepSeek, Groq, OpenRouter |
| Payments | Razorpay, PhonePe, Paytm, PayU, UPI |
| Deployment | Docker, Docker Compose |
| Cache | In-memory TTL cache with background warmer |
| Background | Threaded workers (streak scheduler, cache warmer) |

---

## Deployment

```bash
docker compose up -d
```

Compatible with **Coolify**, **Railway**, and **Render** — single-container deploy via Dockerfile.

Environment variables configure the AI providers, payment gateways, and database path (`DATA_DIR`).

---

## Project Structure

```
toolfy-task-server/
├── app.py                    # Main Flask application (~9,500 lines)
├── landing/
│   └── app.py                # Payment processing server
├── static/
│   ├── index.html            # SPA frontend (~13,200 lines)
│   └── sw.js                 # Service worker (caching/offline)
├── Dockerfile
├── docker-compose.yml
└── AGENTS.md                 # Project conventions
```

---

## Key Design Decisions

- **Single-file backend**: All routes, DB logic, and scheduling in one Python file — easy to deploy, debug, and maintain.
- **No build step**: Inline JS/CSS in the HTML file — no npm, no bundler, no transpilation.
- **Atomic SQL for streaks**: Race conditions between the background scheduler and inline completion handlers are eliminated using conditional `UPDATE` statements with `CASE WHEN` guards.
- **Timezone-aware scheduling**: Each user's timezone is captured on login and used for streak reset calculations. A background worker scans all users every 60s, but skips those whose local day hasn't changed.
- **HMAC payment verification**: The payment landing server calls the main app with a signed payload. The shared secret (`TASKLIPI_ACTIVATION_SECRET`) prevents forged activation requests.

---

## Highlights for Developers

- **~9,500 lines, single file** — demonstrates ability to build and maintain a large, production-grade application in a monolithic architecture
- **Multi-provider AI orchestration** — integrates 6+ LLM providers with fallback, retry, and user-configurable model selection
- **Multi-gateway payments** — 5 payment gateways with HMAC security, subscription management, and region-aware pricing
- **Background workers** — threaded scheduler with timezone awareness and atomic SQL for consistency
- **OTP auth** — token-based session management without passwords
- **Mobile-first SPA** — no framework, no build step — pure vanilla JS at scale (~13,200 lines)

---

## License

MIT
