# Glossary

Terms used in this project, in plain English. vSphere comparisons where they help.
Add your own as you learn.

| Term | What it means here | vSphere-ish analogy |
|------|--------------------|---------------------|
| **Windows service** | A program Windows runs in the background, even with nobody logged in. Ours is `PulseService`. | Like the agent on an ESXi host (hostd) — always running, no UI |
| **SCM** (Service Control Manager) | The part of Windows that starts, stops and restarts services. | Like vCenter's control over host services |
| **Console mode** (`--console`) | Running the service as a normal program in a terminal, for development. | Running a component by hand to watch its logs |
| **Flutter** | Google's UI toolkit. Our app's windows, pages and charts are written in it. | The vSphere Client UI |
| **Dart** | The programming language Flutter uses. | — |
| **C++** | The language the background service is written in; it talks directly to Windows. | — |
| **Named pipe** | A private local channel the app and the service use to talk. | Like the connection between the vSphere Client and vCenter, but only on one PC |
| **IPC** | "Inter-process communication" — two programs talking. Here: over the named pipe. | — |
| **Wire protocol / framing** | The exact byte format of messages on the pipe (starts with `PULS`). | The API contract both sides agree on |
| **Protobuf** | A compact format for structured messages; defines the shape of each message. | Like a WSDL/API schema |
| **Event Log** | Windows' built-in record of what happened (what Event Viewer shows). | Host/vCenter events and tasks list |
| **Humanizer** | Code that turns "Event ID 1000" into "Explorer unexpectedly closed." | — |
| **PDH** | Windows performance counters API (CPU, memory, disk…). | Performance charts / counters |
| **ETW** | Event Tracing for Windows — a deeper, faster event stream. Future feature. | — |
| **MCP** | Model Context Protocol — lets AI apps (Claude, Cursor) call tools. PulseMCP exposes read-only system info to them. | A plug-in that gives an outside tool scoped API access |
| **SDDL** | A text format for Windows permissions, e.g. who may open the pipe. | Roles & permissions on an object |
| **LocalService** | A low-privilege Windows account the service runs as. | A limited-role service account |
| **UAC / elevation** | The "Do you want to allow…" admin prompt. | Logging in as administrator for one task |
| **ADR** | Architecture Decision Record — a short doc explaining a big design choice. Lives in `docs/architecture/decisions/`. | A change record |
| **upstream** | The original Pulse repo I forked from. | The template a VM was cloned from |
| **fork** | My own copy of Pulse on GitHub (`sajaza/Pulse-app`). | A clone of the template |
| **branch / pull request (PR)** | A branch is a separate line of changes; a PR asks to merge it into `master` after review. | A snapshot you test before committing changes |
| **CI** | GitHub Actions that build and test the code on every push (`.github/workflows/ci.yml`). | Automated health checks |
| **Windows on ARM** | The Windows version that runs on Apple Silicon VMs; runs x64 apps via emulation. | — |
