# Changes From Upstream (Pulse)

A running list of everything I changed compared to
[Regncreative/Pulse](https://github.com/Regncreative/Pulse). This makes it much
easier to pull in Pulse's future fixes and see where conflicts might happen.

**Upstream base:** `087f75e` (Merge PR #23, docs/readme-refresh)

## How to pull in Pulse updates

```bash
# one-time setup
git remote add upstream https://github.com/Regncreative/Pulse.git

# whenever you want Pulse's latest changes
git fetch upstream
git checkout master
git merge upstream/master
# fix any conflicts, test, then push
```

## Log

| Date | Area | What changed | Files | Conflict risk with upstream |
|------|------|--------------|-------|-----------------------------|
| 2026-10-22 | Docs | Added project brief, roadmap, actions policy, dev setup, rebrand checklist, glossary | `PROJECT_BRIEF.md`, `ROADMAP.md`, `CHANGES_FROM_UPSTREAM.md`, `docs/project/*` | None (new files) |
| 2026-10-22 | Docs | Note at top of `AGENTS.md` pointing to `PROJECT_BRIEF.md` | `AGENTS.md` | Low (3 lines at top) |
