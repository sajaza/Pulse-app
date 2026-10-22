# Development Environment

My setup: an Apple Silicon Mac → macOS VM for Claude/dev tools → a **Windows VM**
where the app is actually built and run. The app is Windows-only, so building
and testing must happen in Windows.

Fill in the blanks as you set things up — this is the first place to look when
something breaks.

## Machines

| Role | What | Notes |
|------|------|-------|
| Host | Mac, Apple Silicon (arm64), 1 TB | Daily driver |
| Dev VM (macOS) | `lennys-virtual-machine-local` | Claude desktop app, editor, git |
| Windows VM | ______ (Parallels / VMware Fusion / UTM) | Builds & runs the app |
| Real Windows PC (optional) | ______ | For hardware-dependent testing |

## Windows on ARM — what to expect

An Apple Silicon Mac can only run the **ARM64** version of Windows 11. Pulse is
built and released as **x64**.

- x64 apps run on Windows on ARM through emulation, so the installed app will
  likely work.
- **Building** may need extra work: the C++ service and Flutter Windows build
  must target either x64 (cross-compile) or ARM64. Check each step in
  `BUILD.md` and record what worked below.
- Inside any VM, hardware info is partly fake or missing: GPU metrics, battery,
  SMBIOS/motherboard, some sensors. Don't "fix" bugs that only appear in the VM
  without checking on real hardware.

## Toolchain (record exact versions)

See `BUILD.md` for the official prerequisites.

| Tool | Version | Installed how |
|------|---------|---------------|
| Windows 11 | ______ (ARM64) | |
| Visual Studio (C++ desktop workload) | ______ | |
| CMake | ______ | |
| Ninja | ______ | |
| Flutter (stable) | ______ | |
| Git | ______ | |
| Node (for PulseMCP) | bundled | |
| Inno Setup (installer) | ______ | only for packaging |

## Getting the code into the Windows VM

- [ ] Option A: `git clone https://github.com/sajaza/Pulse-app.git` inside Windows
- [ ] Option B: shared folder from the Mac (can be slow/unreliable for builds — prefer A)

## Daily commands (run in PowerShell, inside the repo folder)

```powershell
# Terminal 1 — background service in console mode
.\tools\scripts\run_service_console.ps1

# Terminal 2 — the Flutter app
.\tools\scripts\run_app.ps1

# Before committing
cd apps\pulse_app; flutter analyze; flutter test
```

## Things that broke and how I fixed them

| Date | Problem | Fix |
|------|---------|-----|
| | | |
