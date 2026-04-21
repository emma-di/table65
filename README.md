# Table 65

House cooking signup board for 65 High Street. Single HTML file, Supabase backend,
real-time sync across all devices.

## Stack

- **Frontend** — vanilla HTML/CSS/JS, no build step
- **Backend** — [Supabase](https://supabase.com) (Postgres + realtime websockets)
- **Hosting** — Netlify

---

## How it works

- All meal data lives in Supabase (Postgres)
- Supabase Realtime pushes any INSERT/UPDATE/DELETE to every connected browser
  instantly via websockets — no refresh needed
- The green dot in the header turns red if the connection drops
- Each person's name is saved to their own `localStorage` so they don't have to
  re-enter it each visit

## File structure

```
cooking-board/
├── index.html   ← the whole app
├── schema.sql   ← run once in Supabase SQL editor
└── README.md
```
