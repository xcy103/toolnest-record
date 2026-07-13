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

## Near-term Execution Plan (Jul 12 onward)

Two-part plan: **finish the current tool library first, then internationalize (zh/en).**
Same daily rhythm as before — ship to `toolnest`, write an English work log to
`toolnest-record` each day.

### Part 1 — Finish the tool library

- **Day 1 — QR code generator (publish).** Last tool in the current registry.
  Decision: use a small, mature QR library (e.g. `qrcode`) rather than hand-rolling
  the encoder — the project is already taking on a dependency (next-intl) for i18n,
  so zero-dep is no longer a hard constraint. Render to canvas, support download as
  PNG. Flip `available: true`. **Tool library complete (7 tools).**

### Part 2 — Chinese/English internationalization (next-intl)

Chosen approach: **next-intl** with locale-prefixed URLs (`/en/...`, `/zh/...`).
Confirmed compatible with Next 16 (peerDeps allow `^16.0.0`). **Default locale: English**
(`/` redirects to `/en`) to lean into the "open to the world" goal and international SEO.
Note: Next 16 deprecated `middleware` → renamed to `proxy`; the locale redirect must use
the new `proxy.ts` convention (verify next-intl wiring against it during setup).

- **Day 2 — i18n infrastructure (no visible change).** Install next-intl; add
  `i18n/routing.ts` + `request.ts` + `navigation.ts`; wrap `next.config`; set up the
  `proxy.ts` redirect; move everything in `app/` under `app/[locale]/`. Site still
  builds and renders (English default). URLs become `/en/...`.
- **Day 3 — Externalize copy into a dictionary.** Create `messages/en.json` with every
  UI string (navbar, home, footer, ToolLayout, all 6 tool pages, plus tool
  names/descriptions/categories from `lib/tools.ts`). Refactor components/pages to read
  from translations via `useTranslations`. Still English-only, but data-driven.
- **Day 4 — Chinese translation.** Create `messages/zh.json`, translating every entry
  (including tool names, descriptions, and error messages).
- **Day 5 — Language switcher + SEO.** Add a locale switcher in the navbar (reuse the
  ThemeToggle localStorage pattern). Per-locale `<html lang>`, localized metadata
  (title/description), `hreflang` tags, and a bilingual sitemap. QA both locales,
  mobile pass, deploy.

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
