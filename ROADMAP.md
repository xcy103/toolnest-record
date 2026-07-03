# ToolNest — Roadmap

A living plan for building ToolNest during OPT self-employment. The goal is steady, real progress: **one or two things a day, done in depth, ~4 hours**, learning while building. Simple tools take a day; more complex ones are split across 2–3 days. Learning days, infrastructure days, and company-admin tasks are mixed in so the work stays honest and sustainable over 1–2 months.

This file is updated as things change — it's a guide, not a contract.

## Principles

- **Front-end first.** Everything runs in the browser (Next.js + TypeScript + Tailwind, deployed on Vercel). No sign-up, no backend unless a tool truly needs it.
- **Learn as I go.** I'm starting as a beginner; hitting a new concept and spending a day learning it is expected and worth logging.
- **Ship small and often.** Every finished tool gets committed and deployed, so the live site and the commit history both grow daily.
- **Simple, fast, useful.** Clean UI, quick to load, genuinely helpful for everyday tasks.

## Daily Rhythm (mixed pace)

- **Simple tool** → ~1 day (learn the idea + build + style + ship)
- **Complex tool** → 2–3 days (day 1: learn + scaffold page, day 2: build the logic, day 3: polish, mobile, test, ship)
- **Learning day** → when a tool needs a new technique
- **Infrastructure day** → homepage, navigation, categories, search, about/legal pages
- **Company admin** → branding, domain, privacy policy, formation follow-up (sprinkled in)

---

## Phase 0 — Founding & Foundation ✅ (done, Jun 29 – Jul 2)

- Jun 29 — SSN application; defined the business
- Jun 30 — self-study: how websites are built, front-end basics
- Jul 1 — researched similar tool sites (features + design)
- Jul 2 — chose tech stack, scaffolded the site framework, deployed live on Vercel

## Phase 1 — First Tools + Site Skeleton (Week 1–2, ~Jul 3 onward)

Get the site usable: a homepage, a way to navigate to tools, and the first few working tools.

- First simple tool (e.g. **Word / Character Counter**) — learn the flow end to end
- Homepage layout + tool directory/navigation
- 2–3 more text tools (case converter, remove duplicate lines, text sorter)
- A shared page layout / component style so every tool looks consistent
- About page + footer

## Phase 2 — Grow the Tool Library (Week 3–4)

Add tools across categories, one (or one every couple of days for the harder ones).

- **Encoding:** Base64 encode/decode, URL encode/decode
- **JSON:** formatter / validator, JSON ↔ CSV
- **Color:** hex ↔ rgb, color picker, contrast checker
- **Generators:** password generator, UUID, QR code, hash (MD5/SHA)
- **Time:** unix timestamp converter, timezone converter
- Add tool **categories** and a simple **search** as the list grows

## Phase 3 — Richer Tools + Polish (Week 5–6)

Take on tools that need more learning, and tighten up quality.

- **Image tools** (client-side): compressor, resizer, format converter (PNG/JPG/WebP), favicon generator
- **Markdown** preview/editor
- Mobile/responsive pass across all tools
- **SEO** basics (titles, descriptions, sitemap), performance check
- Analytics to see which tools get used

## Ongoing / Company Admin (interspersed)

- Branding: name treatment, simple logo, favicon
- Custom domain
- Privacy policy + terms (needed once there's traffic)
- Company formation follow-up (post-SSN steps)

---

## Tool Backlog (pick from here)

Text: word/char counter · case converter · remove duplicate lines · text sorter · find & replace · text diff · lorem ipsum
Encode: Base64 · URL · JWT decoder · HTML entities
Data: JSON formatter · JSON ↔ CSV · JSON ↔ YAML
Color: hex ↔ rgb · color picker · gradient generator · contrast checker
Image: compressor · resizer · format converter · crop · favicon generator
Time: unix timestamp · timezone converter · countdown
Generators: password · UUID · QR code · hash
Other: markdown preview · unit converter · percentage/BMI/tip calculators
