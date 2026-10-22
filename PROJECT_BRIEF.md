# Project Brief — [APP NAME]

> This file describes **my** version of the app. Where it disagrees with
> `AGENTS.md` (Pulse's original product rules), **this file wins**.

## In one sentence

[APP NAME] shows what Windows is doing in plain language — and, when I choose,
lets me act on what it finds safely.

## Where it comes from

- Forked from [Pulse](https://github.com/Regncreative/Pulse) by Regncreative (MIT license).
- My fork: https://github.com/sajaza/Pulse-app
- Pulse is kept as the `upstream` git remote so I can pull in its fixes.
- The original MIT copyright notice stays in `LICENSE`, and the README credits Pulse.

## Who it's for

- [ ] Me, for understanding my own PCs
- [ ] Friends/family I help with their PCs
- [ ] IT folks / power users
- [ ] Other: ______

## What stays the same as Pulse

- Local-first: no cloud, no account, no telemetry, no ads.
- Plain-language timeline of Windows events is the heart of the app.
- Native Windows 11 look (Fluent, Mica, dark-first).
- Same architecture: C++ Windows service + Flutter desktop app + named-pipe IPC
  + optional MCP server for AI clients.

## What's different in my version

| Area | Pulse | Mine |
|------|-------|------|
| Name & branding | Pulse | [APP NAME] — see `docs/project/REBRAND_CHECKLIST.md` |
| Read-only rule | Never changes Windows | **Mostly** read-only. A small set of opt-in, confirmed, logged actions is allowed — see `docs/project/ACTIONS_POLICY.md` |
| Features | Pulse roadmap | My roadmap — see `ROADMAP.md` |

## Still off-limits (same as Pulse)

Even with actions allowed, this app is **not** an antivirus, "PC cleaner",
"booster", RAM optimizer, registry cleaner or driver updater. No injecting into
processes, hooking, or patching Windows.

## Open decisions

- [ ] Final app name: ______
- [ ] Who it's for (above)
- [ ] First action to build (see ACTIONS_POLICY candidates)
- [ ] First new feature (see ROADMAP)

## Related files

- `ROADMAP.md` — what I'm building next
- `CHANGES_FROM_UPSTREAM.md` — everything I changed versus Pulse
- `docs/project/ACTIONS_POLICY.md` — rules for anything that changes Windows
- `docs/project/DEV_ENVIRONMENT.md` — my Mac + Windows VM setup
- `docs/project/REBRAND_CHECKLIST.md` — every place the name "Pulse" lives
- `docs/project/GLOSSARY.md` — terms explained in plain English
