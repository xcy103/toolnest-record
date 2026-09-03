# ToolNest — Roadmap

A living plan for building ToolNest during OPT self-employment. The goal is steady, real progress: **one or two things a day, done in depth, with a 4.5-hour planned workday**, learning while building. Simple tools take a day; more complex ones are split across 2–3 days. Learning days, infrastructure days, and company-admin tasks are mixed in so the work stays honest and sustainable over 1–2 months.

This file is updated as things change — it's a guide, not a contract.

## Principles

- **Front-end first.** Everything runs in the browser (Next.js + TypeScript + Tailwind, deployed on Vercel). No sign-up, no backend unless a tool truly needs it.
- **Learn as I go.** I'm starting as a beginner; hitting a new concept and spending a day learning it is expected and worth logging.
- **Ship small and often.** Every finished tool gets committed and deployed, so the live site and the commit history both grow daily.
- **Simple, fast, useful.** Clean UI, quick to load, genuinely helpful for everyday tasks.

## Daily Rhythm (mixed pace)

- **Workdays only:** Monday through Friday, using America/New_York dates. No scheduled development or work logs on Saturday or Sunday. Check the date before assigning a task; ask when a requested date conflicts with this rule.
- **Hours:** 4.5 hours is the daily allocation, not an automatically verified time entry. Record actual owner work and learning time when confirmed.
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
- Custom domain — still open
- ~~Privacy policy~~ ✅ (Aug 21) + terms (still open, needed once there's traffic)
- Company formation follow-up (post-SSN steps)

---

## Near-term Execution Plan (Jul 12 onward)

Two-part plan: **finish the current tool library first, then internationalize (zh/en).**
Same daily rhythm as before — ship to `toolnest`, write an English work log to
`toolnest-record` each day.

> **Status: Parts 1 & 2 complete (Jul 13–17).** Tool library finished (7 tools), and the
> site is now bilingual (`/en`, `/zh`, English default) with a language switcher and a
> bilingual sitemap. Phase 3 below is the current plan.

### Part 1 — Finish the tool library ✅

- **Day 1 — QR code generator (publish).** Last tool in the current registry.
  Decision: use a small, mature QR library (e.g. `qrcode`) rather than hand-rolling
  the encoder — the project is already taking on a dependency (next-intl) for i18n,
  so zero-dep is no longer a hard constraint. Render to canvas, support download as
  PNG. Flip `available: true`. **Tool library complete (7 tools).**

### Part 2 — Chinese/English internationalization (next-intl) ✅

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

## Phase 3 — Grow the Library + Restructure Navigation (Jul 18 onward)

> **Status: complete (Jul 20 – Aug 14).** All five waves shipped and the navigation
> restructure is done. The site went from 7 tools to 23 across 8 categories, with three
> ways to get around (instant search, category menu + category pages, and a full
> `/tools` listing). What followed is recorded under "After Phase 3" at the end of
> this file.

Goal: add a batch of everyday-useful tools, and — because a single long home page stops
scaling past ~10 tools — restructure the front-end around **category navigation** (not
numeric pagination). Every new tool now needs both `en` and `zh` messages; the i18n
scaffolding is already in place, so this is just an extra step per tool, not new plumbing.

Ordering rationale: ship one wave of quick, high-traffic tools first (to reach ~12 tools,
enough to make navigation worthwhile and testable), then do the navigation restructure so
every later tool slots into it automatically, then continue with the remaining waves.

### Wave 1 — Quick, high-traffic tools ✅ (Jul 20–24)

- **Password generator** — `crypto.getRandomValues`; length + character-set options. High search volume.
- **UUID generator** — `crypto.randomUUID`; v4, optional bulk count.
- **Word / character counter** — counts, lines, reading time.
- **Case converter** — UPPER/lower/Title/camelCase/snake_case/kebab-case.
- **Number base converter** — bin / oct / dec / hex, live cross-conversion.

New categories introduced: **Text**. (Password/UUID join **Generators**; base converter joins **Developer**.)

### Front-end restructure — Category navigation ✅ (Jul 27–28)

Do this after Wave 1. Builds on the existing `lib/tools.ts` registry (category pages
generate from `categoryKey`, so adding a tool stays a one-line registration).

- **Navbar**: replace the single "All Tools" link with a **categories menu** (dropdown on
  desktop, collapsible on mobile) listing each category.
- **Category pages** at `/[locale]/c/<category>` — each lists only that category's tools.
  Shorter pages, and each category gets its own indexable URL (good international SEO);
  category names come from the messages. Add these to the sitemap generator too.
- **Home** becomes a proper landing page: hero + a compact category overview / popular
  tools that link into the category pages, instead of dumping every tool.
- **Search**: a client-side instant filter over the registry (no backend), increasingly
  useful as the list grows.
- Keep a full "All tools" browse page (the current grouped view) for browse-everything users.

### Wave 2 — Time cluster ✅ (Jul 29–31)

- **World clock** — common cities' current time at a glance, live-updating.
- **Timezone meeting planner** — find overlapping working hours across a few zones.
- **Countdown / date-diff** — time until a date, or duration between two dates.

### Wave 3 — Developer tools ✅ (Aug 3–6)

- **JWT decoder** — split and show the base64 segments (decode only, no verification).
- **Regex tester** — live match highlighting against sample text.
- **Cron expression explainer** — human-readable description of a cron string.
- **Text diff** — line-by-line comparison of two texts.

### Wave 4 — Colour / design ✅ (Aug 7–10)

- **Color converter** — hex ↔ rgb ↔ hsl, with a picker.
- **Contrast checker** — WCAG AA/AAA pass/fail for a text/background pair.
- **Gradient generator** — build a CSS gradient and copy the code.

### Wave 5 — Higher effort / dependencies ✅ (Aug 11–14)

- **Markdown preview** (needs a markdown library), **image compressor/resizer** (canvas),
  **unit converter**. Take these on once the higher-value, lower-effort waves are shipped.

---

## After Phase 3 — Polish + Continued Backlog (Aug 17 onward)

No new wave plan; work is picked from the backlog below, with polish days mixed in.

- **Aug 17 — SEO / metadata pass.** Found that all 26 tool pages shared one title: metadata
  can only be exported from a Server Component, and every tool page is a Client Component.
  Fixed with a thin server `layout.tsx` per tool over a shared `lib/metadata.ts` — per-page
  titles, descriptions, canonicals, `hreflang` for both locales, Open Graph/Twitter, and
  JSON-LD structured data (`SoftwareApplication` per tool, `WebSite` on the home page).
  Two real narrow-screen overflows fixed along the way.
- **Aug 18 — JSON ↔ CSV converter** (27th tool). A hand-written RFC 4180 parser (quoted
  fields, doubled quotes, embedded newlines, CRLF/CR/LF), conservative type detection, 31 tests.
- **Aug 19 — Test suite.** The ad-hoc tests written for the trickier modules lived in temp
  files and were lost after each run. Added a checked-in suite using Node's built-in
  `node:test` runner and TypeScript stripping — `npm test`, no new dependencies — covering
  calc, md5, colour, units, markdown and csv (34 tests, later 42). Required rewriting
  `CalcError` without constructor parameter properties, which Node's strip-only mode can't run.
- **Aug 20 — Find & replace** (28th tool). Literal or regex, case sensitivity, whole-word
  matching, live highlighted preview; 19 tests. The interesting part is escaping in both
  directions — the search text and the replacement string.
- **Aug 21 — About + Privacy pages.** The two pages promised back in Phase 1: what the site
  is and how it's built, and a plain-language privacy note stating exactly what is stored
  (a `theme` value in local storage, a `NEXT_LOCALE` cookie) and what is not (no analytics,
  no ads, no third-party scripts, no uploads). Both bilingual, linked from the footer and
  listed in the sitemap. Roadmap brought up to date the same day.
- **Aug 24 — HTML entity encoder / decoder** (29th tool). Escapes the five structural HTML
  characters while leaving normal Unicode readable; decodes common named entities plus decimal
  and hexadecimal numeric entities. Added tests for one-layer decoding and malformed entities.
- **Aug 25 — Remove duplicate lines** (30th tool). Text cleanup utility that keeps the first
  occurrence, with options for case sensitivity, whitespace trimming and blank-line handling.
  Shared line-processing logic added with tests.
- **Aug 26 — Text sorter** (31st tool). Sorts lines ascending or descending, alphabetically or
  numerically, with optional duplicate removal. Reuses the shared line module and ships with
  bilingual metadata, category/search wiring and tests.
- **Aug 27 — Unix timestamp converter** (32nd tool). A focused Time tool for converting Unix
  seconds/milliseconds to readable local time, UTC, ISO 8601 and back again. Added strict integer
  parsing, JavaScript Date-range guards, negative timestamp coverage and per-locale page wiring.
- **Aug 28 — JSON ↔ YAML converter** (33rd tool). Added a library-backed Data/Developer tool
  using `yaml@2.9.0` rather than hand-rolling YAML parsing. Supports JSON → YAML, YAML → formatted
  JSON, one-document-at-a-time validation, bilingual UI/metadata and tests for invalid JSON/YAML
  plus multi-document rejection.
- **Aug 31 — Percentage calculator** (34th tool). Added three clearly labelled modes for percentage
  of a number, part-to-whole ratio and percentage change. Handles zero denominators explicitly,
  includes copy support, bilingual UI/metadata and shared calculation tests.
- **Sep 1 — BMI calculator** (35th tool). Added metric and imperial adult BMI calculations,
  standard screening categories and a clear non-diagnostic health note. Browser QA caught and fixed
  a unit-switch rounding issue so the displayed result remains stable across measurement systems.
- **Sep 2 — Tip calculator** (36th tool). Added custom/preset tip rates, currency formatting,
  1–100-person splitting and copyable totals. Integer-cent arithmetic rounds tips once and
  distributes remainder cents so payments add up exactly. Eight new tests include 2,400
  amount/rate/party-size combinations. Browser QA also fixed a shared narrow-screen navbar overflow
  and verified localized routes, copy, validation, category navigation and metadata.

**Still open:**

- Real-file browser smoke test of the image compressor — its canvas path can't be verified
  headlessly, and has been deliberately deferred.
- Custom domain (once chosen, `NEXT_PUBLIC_SITE_URL` replaces the `toolnest.vercel.app`
  fallback used by the sitemap and canonicals).
- Backlog candidates next: favicon generator and image resizer / format converter / crop.
- Analytics deliberately **not** added — the privacy page now promises there is none, so
  adding any would be a documented change, not a quiet one.

---

## Tool Backlog (pick from here)

Built ones are struck through; the rest are still fair game.

Text: ~~word/char counter~~ · ~~case converter~~ · ~~remove duplicate lines~~ · ~~text sorter~~ · ~~find & replace~~ · ~~text diff~~ · ~~lorem ipsum~~
Encode: ~~Base64~~ · ~~URL~~ · ~~JWT decoder~~ · ~~HTML entities~~
Data: ~~JSON formatter~~ · ~~JSON ↔ CSV~~ · ~~JSON ↔ YAML~~
Color: ~~hex ↔ rgb~~ · ~~color picker~~ · ~~gradient generator~~ · ~~contrast checker~~
Image: ~~compressor~~ · resizer · format converter · crop · favicon generator
Time: ~~unix timestamp~~ · ~~timezone converter~~ · ~~countdown~~ · ~~world clock~~ · ~~meeting planner~~
Generators: ~~password~~ · ~~UUID~~ · ~~QR code~~ · ~~hash~~
Dev: ~~number base converter~~ · ~~regex tester~~ · ~~cron explainer~~
Other: ~~markdown preview~~ · ~~unit converter~~ · ~~percentage calculator~~ · ~~BMI calculator~~ · ~~tip calculator~~
