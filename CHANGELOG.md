# Changelog

## Unreleased

- **Convex support:** apps built on Convex now show what each screen asks the backend for.
  - Every exported query, mutation and action in `convex/` is an endpoint on the map, named by its file and export, for example `QUERY /orders:list`.
  - `useQuery(api.orders.list)`, `ctx.runMutation(internal.jobs.send)` and every other use of the generated `api` / `internal` objects connect to the function they name.
  - Webhooks registered with `http.route(...)` in `convex/http.ts` are endpoints too.
  - `convex/_generated/` is left off the map, so the generated API file no longer links every screen to every backend file.
- **Health for Convex:** public functions that never check who is calling are reported, the same way open endpoints are. Internal functions are skipped, since only the backend can call them. Sign-in checks count when they're in the function, in a helper in the same file, or in an internal check function it calls.
- **Fewer false Health alarms:** sample secrets labelled as bad examples (`vulnerable_example:` in a security checklist, for instance) are no longer reported as leaked keys.

## 0.1.2 (2026-10-27)

- **Floorplan Cloud waitlist:** once a map has been open for two minutes, a corner card asks, once, whether you'd like an email when Floorplan Cloud (shared, synced team maps) launches. Nothing is sent unless you click **Notify me**, and then only your email and "just me" or "with my team". **Use my Claude email** fills in your Claude account's address, and you see it before anything is sent. **Don't ask again**, or `FLOORPLAN_NO_PROMPTS=1`, turns it off. See [Privacy and security](docs/privacy-and-security.md#floorplan-cloud-waitlist).
- The waitlist service's code is in `services/waitlist/`: rate-limited per IP address and overall, write-only, and capped.

## 0.1.1 (2026-10-27)

- **More connections found:** requests made through small helpers imported from an API client, like `post("/orders", …)` in a Python job, are now matched to the endpoints they reach.
- **Fewer false Health alarms:**
  - Express routers protected where they're mounted (`app.use('/admin', requireStaff, adminRouter)`), including routers nested inside them, are no longer reported as open to anyone.
  - Newsletter, contact and waitlist sign-ups are treated as public on purpose.
- **Flows:** the page heading fades out while a flow plays, so the flow bar no longer overlaps it.
- **Screens:** a screen's board is labelled "Screen" instead of "Answer".
- **README:** screenshots, from a demo app mapped end to end.

## 0.1.0 (2026-10-27)

First release.

- **The map:** an interactive node graph of a codebase, from the whole app down to single files and endpoints. Every part has a plain-English name and description. It works across several repos side by side.
- **Connections:** imports, and web requests matched to the server endpoints they reach, including URLs built in variables, nested template strings and small request helpers. Flask blueprint and Express router prefixes are resolved, nested mounts included.
- **Screens:** detects an app's pages (Next.js, React Router, Vue, SvelteKit, Remix, Nuxt, Astro, Expo, Angular, TanStack) and shows everything behind each one.
- **Health check:** passwords and keys in code, endpoints anyone can use without signing in, unused files and very large files, each with a ready-made fix prompt. Secret values are never stored.
- **Ask:** questions answered as a mini-map with a walkthrough, through the Claude Code CLI or the Claude app.
- **Flows:** guided walkthroughs, plus "Request a new flow".
- **Start here** tour, plain-language glossary and a "Show technical detail" switch.
- **Recent work:** the cards Claude just changed are highlighted, each with a note tying the change to what was asked.
- **Updates:** refreshes re-read only what changed, and an open map reloads itself.
- **Git:** nothing Floorplan creates is committed. The map folder ignores itself, and Claude's notes go in `CLAUDE.local.md`.
