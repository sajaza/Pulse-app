# Rebrand Checklist

Every place the name "Pulse" is baked in. Rename them **together**, so my app can
be installed alongside the original Pulse without the two fighting over the same
service, pipe or folders.

Pick these first:

| Thing | Pulse value | My value |
|-------|-------------|----------|
| Display name | Pulse | ______ |
| Service name | `PulseService` | ______Service |
| Named pipe | `\\.\pipe\PulseService` | ______ |
| Data folder | `ProgramData\Pulse` | ______ |
| Installer AppId (GUID) | `8F3C2A91-…` | **new GUID** (`[guid]::NewGuid()` in PowerShell) |
| Frame magic | `PULS` | keep as-is (internal only) |

## Must change (or the two apps collide)

- [ ] **Service name** — `service/pulse_service/src/service_core/service_core.cpp`
      (`L"PulseService"` appears in several places)
- [ ] **Named pipe name** — C++ service, Dart client and PulseMCP
      (search for `pipe\\PulseService`)
- [ ] **ProgramData folder** — `kProgramDataRelative` in
      `shared/pulse_common/include/pulse/constants.hpp`
- [ ] **Installer** — `tools/installer/Pulse.iss`: `MyAppName`, **new `AppId` GUID**,
      `DefaultDirName`, `OutputBaseFilename`
- [ ] **MCP server name** — the name registered in Cursor / Claude Desktop config
- [ ] **Export folder** — `Downloads\Pulse` in `apps/pulse_app/lib/platform/export_writer.dart`

## Should change (branding)

- [ ] `apps/pulse_app/pubspec.yaml` — `description`, `display_name`, `publisher_display_name`
- [ ] Window title and in-app text (~90 Dart files mention "Pulse" — review, don't blind-replace)
- [ ] `apps/pulse_app/windows/runner/Runner.rc` — product/company name, `.exe` metadata
- [ ] App icon — `apps/pulse_app/assets/branding/`, `branding/logo/`
- [ ] `README.md` — new name, my screenshots, credit to Pulse
- [ ] `docs/branding/BRANDING.md`
- [ ] GitHub repo name / description (optional)

## Probably leave alone

- Folder and package names like `pulse_app`, `pulse_service`, `pulse_protocol`.
  Renaming them touches hundreds of files and makes merging upstream fixes
  painful. Users never see them.
- `LICENSE` — keep Pulse's MIT notice (you may add your own line).

## How to find leftovers

```powershell
git grep -n "PulseService"
git grep -n -i "pulse" -- "*.iss" "*.rc" "*.yaml" "*.json"
```

When done, log it in `CHANGES_FROM_UPSTREAM.md`.
