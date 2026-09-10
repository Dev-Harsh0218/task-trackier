# HANDOFF — Task-Trackier (parallel session pickup)

**Read this first.** Full context for a Claude session picking up this project mid-build.

---

## One-paragraph summary

Harsh (backend engineer, laid off 2026-09-03 from Astro Arun Pandit, on 30-day notice, ₹50K/month EMI, actively job-hunting) is building **Task-Trackier** — a JIRA-inspired internal issue tracker with a **weighted developer scoring system**. Originally built at AppSuccessor for 100–200 employees; this is the open-source reference implementation. It's on his resume across all three variants (SDE / Backend / FullStack) and needs to be a live, defensible portfolio piece.

## Repo family (3 repos)

| Repo | Purpose | State |
|---|---|---|
| [`task-trackier-platform`](https://github.com/Dev-Harsh0218/task-trackier-platform) | Meta-repo — architecture doc, cross-repo README | ✅ done |
| [`task-trackier`](https://github.com/Dev-Harsh0218/task-trackier) | Python monorepo — Django API + Kafka scoring worker + SSE gateway | 🟡 Slice 1 done (scaffold only). Slices 2–7 pending. |
| [`task-trackier-web`](https://github.com/Dev-Harsh0218/task-trackier-web) | Next.js frontend — marketing site + authed Kanban app | ❌ **not yet bootstrapped** (biggest gap) |

## Current filesystem state

- Backend: `/Users/devharsh0218/Business/task-trackier/` — has full scaffold (`services/{api,scoring-worker,sse-gateway}/{src,tests}/`), `pyproject.toml`, `docker-compose.yml` stub, README, TODO.md
- Platform meta: `/Users/devharsh0218/Business/task-trackier-platform/` — README + TODO
- Frontend: local dir does not exist yet — needs `mkdir` at `/Users/devharsh0218/Business/task-trackier-web/`

## Two possible directions (pick one, don't do both simultaneously)

### Direction A — bootstrap the frontend (recommended first)
The frontend is the biggest visible gap. Two Next.js apps in a Turborepo:
- `apps/marketing` — public marketing site (like `linktester-web` or `fornello-web`)
- `apps/app` — authed Kanban board that consumes the Django REST API + subscribes to SSE
Deploy marketing to Vercel immediately (public URL for resume/GitHub). App can point at a mock API until backend Slice 3 lands.

### Direction B — advance the backend slices
Continue slice-by-slice per `TODO.md`:
- Slice 2 — Django models (Sprint, Ticket, Developer, Comment, Attachment) + migrations + admin
- Slice 3 — DRF endpoints + pagination + filters
- Slice 4 — Kafka publisher wiring on ticket mutations
- Slice 5 — scoring-worker consumer + `compute_weighted_score()`
- Slice 6 — sse-gateway consumer + Redis pub/sub + `EventSource` HTTP endpoint
- Slice 7 — 3 Dockerfiles + full docker-compose integration test

**Recommendation**: Direction A first (frontend visible on Vercel = immediate resume credibility), then Direction B in a following session.

## User's preferences (do NOT skip)

1. **NO `Co-Authored-By: Claude`** on any commit — hard rule. Verified across every repo this session. See `/Users/devharsh0218/.claude/projects/-Users-devharsh0218-Business-job/memory/feedback_no_claude_coauthor.md`.
2. **Rapid execution.** He says "just do what you think would be best" — pick sensible defaults and move. Confirm only before destructive/hard-to-reverse actions.
3. **Consistent naming pattern.** All portfolio projects across the account follow `<brand>-{platform,web,api}` or `<brand>-{web,backend}` kebab-case.
4. **Match the aesthetic bar.** Recent Next.js sites (`fornello-web`, `studyvize-website`, `messaging-server-web`) all use: Next.js 16 App Router + Turbopack + Tailwind v4 + Framer Motion (`13.2.0`) + `next/font` typography + tasteful animations. Don't ship a create-next-app default.
5. **Push is authorized.** No need to ask each time.

## Related repos this session shipped

Reference these for aesthetic/architecture pattern:
- `fornello-web` (marketing site — warm restaurant palette)
- `messaging-server-web` (dark terminal aesthetic — closer to what task-trackier-web should feel like)
- `linktester-web` (Turborepo with `apps/marketing` + `apps/panel` — closest structural analogue)
- `studyvize-website` (premium animated marketing site)

## User context for tone/framing

- Backend engineer, ~2.5–3 years experience
- Full-stack (Node.js / Django / React / AWS) with Erlang exposure
- Laid off 2026-09-03, 30-day notice, ₹50K/month EMI pressure
- Prefers dev-culture voice, Neovim/tmux user, opinionated engineering
- Interested in Go direction + AI/LLM exposure

## Assets NOT to touch from this session

- `/Users/devharsh0218/Business/job/` — resume + outreach templates (main session is working on this)
- The 6 other portfolio projects (`fornello*`, `studyvize*`, `leadiiq*`, `linktester*`, `aduo*`, `messaging-server*`) — all shipped, don't modify

## When you (Claude) start a fresh session, do this

1. Read this file entirely
2. Read `TODO.md` (backend slices) and `README.md` (architecture)
3. Read `task-trackier-platform/README.md` (cross-repo view)
4. Check git state: `cd /Users/devharsh0218/Business/task-trackier && git log --oneline`
5. Ask user: *"Direction A (bootstrap frontend + deploy) or Direction B (advance backend slices)?"*
6. Proceed after user confirms.
