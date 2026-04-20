# Table 65

House cooking signup board for 65 St Giles'. Single HTML file, Supabase backend,
real-time sync across all devices.

## Stack

- **Frontend** — vanilla HTML/CSS/JS, no build step
- **Backend** — [Supabase](https://supabase.com) (Postgres + realtime websockets)
- **Hosting** — any static host (Netlify, Vercel, GitHub Pages)

---

## Setup

### 1. Create a Supabase project

1. Go to [supabase.com](https://supabase.com) → New project
2. Pick a name, set a database password, choose a region close to the UK

### 2. Create the database table

In your Supabase dashboard go to **SQL Editor → New query**, paste the contents
of `schema.sql`, and run it. This creates the `meals` table and enables realtime.

### 3. Get your API keys

Go to **Project Settings → API** and copy:
- **Project URL** — looks like `https://xxxxxxxx.supabase.co`
- **anon / public key** — the long `eyJ...` string

### 4. Add them to index.html

Open `index.html` and replace the two placeholder values near the bottom:

```js
const SUPABASE_URL  = 'YOUR_SUPABASE_URL';
const SUPABASE_ANON = 'YOUR_SUPABASE_ANON_KEY';
```

### 5. Deploy

**Netlify (fastest):**
1. [app.netlify.com/drop](https://app.netlify.com/drop) → drag the folder in
2. Done — you get a shareable URL immediately

**Vercel:**
```bash
npx vercel --cwd ./cooking-board
```

**GitHub Pages:**
1. Push the repo to GitHub
2. Settings → Pages → Source: main / root

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

## Security note

The current RLS policies allow anyone with the URL to read and write. That's
fine for a private house share — just don't post the link publicly. If you want
to lock it down, add a simple Supabase auth flow (magic link email works well)
and tighten the RLS policies to `auth.uid() is not null`.
