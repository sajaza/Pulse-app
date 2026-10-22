# Actions Policy

Pulse never changes Windows. My version may, but only through the rules below.
Every new action must be added to the **Approved actions** table before any code
is written for it.

## Why this needs care

The background service is a long-running Windows service, and the app talks to
it over a named pipe. Today that pipe only *returns information*, so a
misbehaving program talking to it can at worst read data. Once the service can
*do* things, the pipe becomes a doorway: if it's not locked down, any program on
the PC could ask the service to act on its behalf.

Two facts from the current code that matter:

- The service runs as `NT AUTHORITY\LocalService` (ADR-002) — a deliberately
  low-privilege account. Most useful actions (restarting services, deleting
  system temp files) need more power than that.
- The pipe's permissions (`kPipeSddl` in
  `shared/pulse_common/include/pulse/constants.hpp`) let **every logged-in
  user** (`BU`) read and write it. Fine for read-only; not fine for actions.

## The rules

1. **Off by default.** Each action has its own switch in Settings → Actions.
2. **Confirm every time.** The UI shows exactly what will happen ("Restart the
   Print Spooler service") and the user clicks to confirm. No silent actions.
3. **Fixed allowlist.** The service only accepts action *IDs* from the table
   below with validated parameters (e.g. a service name that exists). It never
   accepts raw commands, scripts, file paths or command-line arguments over the
   pipe.
4. **Least privilege.** Don't raise the main service's account. Prefer:
   - actions that run in the app as the user, when admin isn't needed; or
   - a separate small helper that elevates (UAC prompt) for that one action
     and exits.
   Decide this per action and record it in the table.
5. **Lock the door.** Action requests must only be accepted from an
   authenticated client (e.g. verify the caller's process / restrict pipe
   permissions for the action channel). Design this before the first action
   ships, and write an ADR for it.
6. **Audit log.** Every action — requested, confirmed, succeeded, failed — is
   written to a local log the user can see in the app and export.
7. **Not from AI by default.** The MCP server stays read-only. If an AI client is
   ever allowed to *propose* an action, the human still confirms in the app.
8. **Reversible where possible.** Prefer actions that can be undone. If it can't
   be undone, the confirmation says so.
9. **Still not a cleaner/optimizer.** Actions exist to fix something the
   timeline explained, not to "boost" the PC.

## Approved actions

| ID | What it does | Needs admin? | Runs where | Reversible? | Risk | Status |
|----|--------------|--------------|------------|-------------|------|--------|
| _none yet_ | | | | | | |

## Candidate actions (ideas, not approved)

| Idea | Why it's useful | Notes |
|------|-----------------|-------|
| Restart a stopped/crashed Windows service | Timeline shows "Print Spooler stopped" → one-click restart | Admin; good first candidate; only for services that already exist |
| Open the relevant Windows settings page | Jump to Windows Update, Device Manager, etc. | No admin; zero risk — easiest first action |
| End a hung app | Timeline shows an app not responding | Same user's processes only; no admin |
| Create a System Restore point | Safety net before changes | Admin; only "create", never "restore" |
| Clear the user's own temp folder | Disk low warning | Borderline "cleaner" territory — decide carefully |

## Checklist before shipping an action

- [ ] Added to the Approved actions table
- [ ] ADR written if it changes the service, pipe or privilege model
- [ ] Off by default; confirmation text reviewed
- [ ] Parameters validated in the service, not just the UI
- [ ] Audit log entry written for every outcome
- [ ] Tested in the Windows VM **and** noted if real hardware is needed
- [ ] Entry added to `CHANGES_FROM_UPSTREAM.md`
