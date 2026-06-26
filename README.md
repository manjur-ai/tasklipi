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

## Features by Role

### For Teachers

**Assignment Creation & AI Generation**
- Create and assign planned tasks to students individually or in bulk
- AI-generate **MCQ assignments** from source material (text, camera photos, PDF files) with configurable question count, difficulty levels, explanation modes (Off/Normal/Short), and custom instructions using `html2mcq` library
- AI-generate **QA (descriptive) assignments** with mark allocation (1–5 marks per question by answer depth)
- Built-in **MCQ builder** with single-correct, multi-correct, negative marking, and display-doc support
- Built-in **QA builder** with model answers, explanations, and rich-text answer fields
- **AI evaluation** of student QA answers — auto-grades against answer keys, handles media-rich answers with OCR

**Monitoring & Assessment**
- **Task monitor dashboard** — per-assignment view showing each student's completion status, MCQ score/total, and QA submission status
- **Study recordings** — listen to students' audio recordings with auto-analysis (speech percentage, silence percentage, reading detection)
- **Completion criteria** — set global rules (recording required, minimum speech score, MCQ pass %, note keywords, forced AI instruction)
- **Per-task pass criteria** — override global rules with task-specific requirements (recording duration, self-MCQ/QA scores, assigned MCQ/QA scores, note study time)
- **Streak tracking** — view student consistency on daily tasks

**Content Sharing**
- Send copies of projects (with all steps) to students
- Share weekly timetables with students
- Share projects live with view/assign access
- **QR code task distribution** — generate QR codes for quick task sharing
- Group-based batch operations (e.g., assign to all users in "Children" group)

### For Parents

**Child Monitoring**
- **Share relationship** — connect your account to your child's account with controller or assigner role
- **Switch view** — see your child's dashboard, tasks, schedule, and progress in real-time
- **Completion criteria** — set rules your child must meet before marking tasks done:
  - Recording required (min duration + min speech score)
  - Self-MCQ required (min pass percentage)
  - Note keywords (specific words in task title trigger mandatory self-note)
  - MCQ/QA relaxation (either one suffices to pass)
  - Forced AI instruction (overrides child's custom instruction)
- **Per-task pass criteria** — set task-level requirements (e.g., "recording must be at least 30 minutes with 60% speech")

**Progress Tracking**
- View child's streak, longest streak, and daily completion history (last 7 days)
- View child's executor timeline — see what they worked on each day
- Listen to child's study recordings with speech analysis
- View MCQ/QA exam results, scores, and AI evaluation feedback
- Receive push notifications about child's task completion
- Chat with child through the built-in messenger

**Task Management**
- Send daily routine tasks directly to your child's account
- Assign planned tasks with attached assignments
- Set up weekly timetables for your child
- Monitor which tasks have attached notes and study recordings

### For Students

**Task Organization**
- **Daily tasks** — routine tasks with per-task streak tracking and overall streak system; drag-and-drop reorder; category filters
- **Planned tasks** — one-time tasks with scheduling, priority levels, and status tracking (Pending/In Progress/Done/Skipped); alarms with push notifications
- **Projects** — multi-step projects with sub-steps, deadlines, status tracking, and drag-and-drop reorder
- **Lists & Goals** — create and manage personal lists and goals; share with connected accounts
- **Weekly timetable** — recurring schedule slots with subject, location, teacher, color coding; list/grid view
- **Categories** — customizable category system (Personal, School, Study, etc.) for all task types

**AI-Powered Features**
- **AI Task Planner** — describe your day in plain text (e.g., "Math class at 9am, doctor at 2pm") and get structured planned tasks with times and categories; **prompt store** saves/loads up to 30 named prompt templates
- **Ask AI Tutor** — ask questions about a study task with optional image attachments; get structured answers with HTML formatting
- **Self-MCQ Generator** — generate practice MCQs from your notes, textbook photos, or PDF files
- **Self-QA Generator** — generate practice descriptive questions from your study material
- **AI evaluation** — get AI-graded feedback on your QA answers

**Study Tools**
- **Study recordings** — record yourself studying; auto-analyzed for speech percentage, silence percentage, and reading detection
- **Notes** — markdown editor per task with reading time tracker (accumulated reading time across sessions)
- **Pomodoro focus timer** — configurable work/break cycles with visual ring progress and session tracking
- **Executor** — today's timeline view showing all active tasks with elapsed time counters and real-time status; **ad-hoc tasks** (free-form entries not linked to any source task); day navigation with date picker

**Exams & Assessments**
- **MCQ exams** — full-screen exam mode with one-at-a-time or all-visible display; skip/review-later; auto-grading; retake options (all or incorrect only); AI evaluation; **explanation modes** (Off/Normal/Short) on AI-generated questions
- **QA exams** — rich-text answer editor with keyboard shortcuts; **auto-save draft** to localStorage; skip; AI-graded feedback with per-question scores and model answers; focused retake (incorrect/partly correct only)
- **Quick self exams** — one-click MCQ/QA generation from any study task

**Engagement & Motivation**
- **Streak system** — per-task streaks (🔥 counter) and overall streak; timezone-aware daily reset
- **Milestone celebrations** — confetti animations at 7/30/100/365-day streaks and 10/50/100/500/1000 tasks
- **Screensaver** — idle-triggered full-screen overlay showing your goals
- **Push notifications** — task alarms and reminders via browser push API; cross-device alarm dismiss (dismiss on one device syncs to all)
- **PWA back-button exit guard** — first back press closes overlays; second confirms app exit

**Productivity**
- **Planned task alarms** — per-task alarm with sync-dismiss across all devices; native Android alarm plugin support
- **Executor timer** — countdown timer with presets (5/10/15/25/30/45/60 min) and custom input; Web Audio alarm with vibration
- **Drag-and-drop** — reorder tasks, projects, and steps with mouse and touch support
- **Attachments** — upload images, videos, PDFs, and documents; auto-generated WebP thumbnails (128×128)
- **Image processing** — crop modal with quadrilateral drag handles and 90° CW rotate; browser-side normalization to 1536px longest side at JPEG 92% quality before upload
- **Link previews** — fetch Open Graph / Twitter Card metadata from URLs
- **Grade visualization** — color-coded score pills (gradeColor, gradePillClass) and progress rings (ringHTML) for MCQ/QA results
- **AI token usage** — per-operation, per-model token accounting visible in account profile (total, last 30 days, per-operation breakdown)
- **Onboarding flow** — persona selection (student/teacher/parent/professional/other), name input, class/grade or subject, preset categories by persona
- **Dark/light mode**

### For Spouses & Partners

**Collaborative Task Management**
- **Share accounts** — connect with your partner's account; view each other's tasks and schedules
- **Assign tasks** — create and assign tasks to your partner with assigner role
- **Collaborate on projects** — share projects live with step-by-step tracking
- **Shared lists and goals** — collaborate on shared shopping lists, goals, or plans
- **Chat** — built-in real-time messenger with text and image sharing

**Account Sharing Options**
- **Controller role** — full read, write, and assign access to partner's account
- **Assigner role** — read access plus ability to assign and track tasks
- **Friend role** — chat-only access
- **QR code sharing** — quick account linking by scanning a QR code

### Behind the Scenes

- **AI orchestration** — multi-provider support (OpenAI, Anthropic, Google Gemini, DeepSeek, Groq, OpenRouter) with automatic fallback and user-configurable model selection; per-operation model chaining (e.g., Groq for OCR, Gemini for MCQ generation)
- **Per-user timezone** — saved on login; used for streak reset, daily rollover, and alarm scheduling
- **Background workers** — streak scheduler (60s interval), alarm pusher (10s interval), cache warmer (3s interval), daily cleanup of old recordings/notes/AI sources
- **Security** — OTP-based passwordless auth with escalating rate limits (2min cooldown, 5-resend → 60min block, 5 wrong OTPs → 24h lockout); 30-day persistent tokens surviving app restarts; configurable email providers (Brevo, SendGrid, Gmail SMTP, AWS SES, Mailgun, Mailjet, MailerSend, Resend) with automatic fallback chain; crawler/AI opt-out headers; strict CORS origin validation; dev/test login bypass with env guard
- **Performance** — SQLite WAL mode, hot-path database indexes, bounded in-memory TTL cache with 3s background warmer; client-side localStorage cache with debounced saves and tab prefetching
- **Single-file architecture** — all routes, DB logic, and scheduling in one Python file (~9,500 lines); SPA frontend in one HTML file (~13,200 lines) with no build step**

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
