<div align="center">

# Antidote
### Windows Optimization, Cleanup, Debloat & Privacy Hardening

**Free. Open source. No license. Built for everyone.**

[![Version](https://img.shields.io/badge/version-2.4.0-brightgreen?style=flat-square)](https://github.com/Tripartitus/Antidote/releases/latest)
[![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-blue?style=flat-square)](https://github.com/Tripartitus/Antidote)
[![License](https://img.shields.io/badge/license-Free%20%E2%80%94%20always-orange?style=flat-square)](https://github.com/Tripartitus/Antidote)
[![Built with](https://img.shields.io/badge/built%20with-.NET%209-purple?style=flat-square)](https://github.com/Tripartitus/Antidote)

*by [Tripartitus](https://github.com/Tripartitus) — [Twitch](https://www.twitch.tv/tripartitusgaming) · [YouTube](https://www.youtube.com/@TripartitusGaming)*

</div>

---

## What is Antidote?

Antidote is a Windows optimization tool that does what Windows should have let you do from the start — remove the bloat, silence the telemetry, tune the performance settings, and take back control of your machine. It is built as a proper desktop application with a modern, themed interface, not a script you squint at in a terminal.

It is not a magic speed-doubler or a snake-oil cleaner. Every change it makes is documented, every change it makes is reversible, and the health score it shows you is grounded in the actual state of your system — not a number fabricated to make the software look impressive.

Antidote is free for everyone. There is no Pro version, no feature gating, no license required. That is not going to change.

---

## Who is it for?

**Gamers** who want the lowest possible input latency and CPU overhead — Antidote applies MMCSS scheduling, disables Game DVR background capture, turns off fullscreen optimizations, removes mouse acceleration, and kills the network multimedia throttle that Windows silently applies.

**Privacy-conscious users** who want to stop the steady stream of telemetry Windows sends to Microsoft by default — Antidote disables DiagTrack, Cortana, Bing integration in the Start menu, Windows Recall / AI snapshots, location tracking, advertising IDs, and device-name telemetry. Sentinel Mode watches in the background and reverses any of it that Windows quietly turns back on.

**People setting up a new PC** who want to go from a fresh Windows install to a clean, configured system in one run — bloat removed, runtimes installed, preferred apps installed silently, browser hardened, and the privacy and performance baseline set.

**Users who are cautious** and want to understand what is happening to their machine before anything runs — Dry Run mode shows every step without making a single change, and the Info button on every phase explains in plain English exactly what it does, why, and what the trade-offs are.

**Anyone who has an old or slow PC** and wants to know whether there is anything recoverable — the System Health Score tells you exactly what is holding the machine back and which phases fix each issue.

---

## The core design principles

**Everything is reversible.** The reverse phases and Undo Center exist specifically so that no change Antidote makes is permanent if you decide you don't want it. Debloat (AppX removal) is the one explicit exception — removed Windows apps are not brought back automatically, and the interface says so clearly before you run it.

**Nothing is hidden.** Every phase has an Info button that reads like a real explanation, not marketing copy. The health score is calculated from actual registry and service state, not guessed. The System Map shows you what is happening live as each phase executes.

**The safety net comes first.** The first recommended phase is "Create System Restore Point." The first thing a run does is create a backup of the registry and service configuration. The Undo Center gives you a timestamped record of every run you can revert from.

---

## System Health Score

When Antidote opens, it scans your system and produces a **Software Health Score** out of 100, composed of 22 weighted checks across privacy, performance, and system state. A hardware ceiling is applied based on detected hardware (HDD installs and low-RAM systems get a realistic cap), so the score represents what is achievable on *your* machine, not on an imaginary ideal PC.

The score is broken into three sub-dimensions:

- **Privacy Score** — telemetry, data collection, advertising, location, and browser settings
- **Debloat / Performance Score** — MMCSS scheduling, CPU priority, Game DVR, network throttle, mouse, fullscreen optimization
- **Disk / Cleanup Score** — free space, temp folder size, process count

Each check is linked to the specific phase that fixes it, so the "Why this score?" breakdown tells you not just what is wrong but exactly which phase makes it right. After every run, the score re-scans automatically and updates.

The hardware summary also reads your CPU, RAM, storage type (NVMe / SSD / HDD), and GPU, and displays them in the dashboard for reference.

---

## Optimization phases

Antidote runs in phases — discrete, well-defined steps that each do one job. You choose which phases to run, what order is fixed by the engine for safety, and each phase can be individually inspected before you commit to anything.

### Safety

| Phase | On by default | Notes |
|---|---|---|
| Create System Restore Point | ✅ | Creates a Windows restore point before anything else. Always recommended. |

### Health & Repair

| Phase | On by default | Notes |
|---|---|---|
| System Repair (DISM + SFC) | ✅ | Runs DISM RestoreHealth and SFC /scannow to repair corrupted Windows files. |
| Disk Health Scan (chkdsk) | ⬜ | Schedules a chkdsk run on next boot. Marked optional because it is slow. |

### Cleanup

| Phase | On by default | Notes |
|---|---|---|
| Deep Cleanup | ✅ | Removes temp files, Windows Update cache, Prefetch, error reports, and other performance junk from known locations. |
| Browser Cleanup | ✅ | Clears cache and temporary files from installed browsers. |

### Disk

| Phase | On by default | Notes |
|---|---|---|
| Disk Optimization (TRIM / Defrag) | ✅ | Sends TRIM to SSDs and NVMe drives. Runs defrag only on HDDs. Accurately detects drive type before deciding which to run. |

### Performance

| Phase | On by default | Risk | Notes |
|---|---|---|---|
| Power Plan + GPU Scheduling | ✅ | Low | Sets the High Performance power plan and enables Windows Hardware-Accelerated GPU Scheduling. Also adjusts visual effects to "performance" mode. |
| Advanced FPS / Latency Tweaks | ✅ | Low | MMCSS scheduling (Win32PrioritySeparation=26, SystemResponsiveness=10), network multimedia throttle off, Game DVR off, fullscreen optimizations off, mouse acceleration off, startup delay removed, NDU service disabled. See phase Info for the detailed breakdown. |
| Advanced Memory Optimization | ⬜ | Moderate | Working-set trimming and memory compaction. Optional because the benefit varies by workload. |
| Gaming Process Priority & Affinity | ⬜ | Aggressive | Raises process priority and adjusts CPU affinity for running game processes. Aggressive because it can make background tasks less responsive. |
| Disable VBS / Memory Integrity | ⬜ | Aggressive | Disables Virtualization-Based Security and Memory Integrity (HVCI) for a measurable performance gain on older hardware. Read the Info before enabling — this reduces isolation security in exchange for performance. |

### Network

| Phase | On by default | Notes |
|---|---|---|
| Network Low-Latency Tweaks | ✅ | Disables Nagle's algorithm (TcpAckFrequency), tunes TCP/IP for low-latency interactive traffic. |
| REVERSE: Network Tweaks | ⬜ | Restores all network registry settings to Windows defaults. |

### Debloat & Privacy

| Phase | On by default | Risk | Notes |
|---|---|---|---|
| Debloat + Privacy Hardening | ✅ | Moderate | Removes AppX bloatware (News, Weather, Cortana, Copilot, Get Help, 3D Viewer, Office Hub, Solitaire, Mixed Reality Portal, OneNote, People, Print3D, Skype, Alarms, Feedback Hub, Maps, Sound Recorder, Groove Music, Movies & TV, Windows AI Copilot Provider). Disables telemetry, DiagTrack, Bing in Start, advertising ID, Edge metrics, and lockscreen suggestion ads. **AppX removal is permanent** — the phase says so clearly. |
| Deep Telemetry Block | ⬜ | Aggressive | Enterprise-level telemetry policy applied via the Policies registry hive. Includes device-name exclusion from telemetry. Aggressive because it applies policies that can conflict with managed/domain environments. |

### Apps & Updates

| Phase | On by default | Notes |
|---|---|---|
| Check for Application Updates | ✅ | Runs winget upgrade to update installed applications. |
| Install Dependencies (Runtimes) | ⬜ | Silently installs every Visual C++ Redistributable (2005–2022, x86 and x64), .NET Framework 4.8, .NET Desktop Runtime 6/7/8, and DirectX End-User Runtime. Useful on fresh builds or when apps complain about missing DLLs. |
| Install Selected Apps | ⬜ | Installs whichever apps you selected in the App Catalog (see below). Driven by winget. |
| Browser Hardening | ✅ | Applies privacy and performance settings to Edge and Chrome. Moderate risk because it changes browser defaults. |

### Reverse

| Phase | On by default | Notes |
|---|---|---|
| REVERSE: Registry Tweaks | ⬜ | Restores every registry value that the performance, FPS, and power phases modified back to Windows defaults. |

---

## Quick presets

Don't want to pick phases manually? Choose a preset and Antidote configures the right set for your use case.

| Preset | What it selects |
|---|---|
| **Minimal** | Only the essential safety and cleanup phases — safe for any machine, any user |
| **Recommended** | The well-balanced default: cleanup, repair, performance basics, debloat, privacy hardening, network tweaks |
| **Returning user** | Skips the phases you've already run on a previous session, focuses on anything new |
| **Gaming Beast** | Everything recommended, plus all gaming-specific performance tweaks and process priority |
| **Laptop Eco** | Battery-friendly selection — skips aggressive performance phases that drain power |
| **Privacy Fortress** | Maximum privacy hardening including deep telemetry block and browser hardening |

---

## Smart Optimize

One click. Antidote scans your system, reads the health score, and automatically selects the phases that matter most for your current state — skipping anything that's already done. Click **Run** and it takes care of the rest.

---

## Dry Run mode

Before committing to any changes, enable **Dry Run** and execute the full selected phase set. Every step is logged exactly as it would run, but nothing is written to the registry, no services are changed, no files are removed. Use it to see exactly what Antidote would do on your specific machine before it does anything.

---

## System Map

Accessible from **Menu → Tools → System Map**, the System Map is a live animated diagram of your machine's optimization state. Every phase is a node; every cluster of related phases is a group. As a run executes:

- Nodes that need work glow **red** before the run starts — seeded from the health scan
- The active phase pulses **amber** while it's running
- Completed phases ease smoothly to **green**
- A central ring fills as the run progresses, showing **% optimized** in real time

The map is a pure observer — it never interferes with the run, and the run proceeds identically whether the map is open or not. Open it at any point during or after a run to see where things stand.

---

## App Catalog

Antidote includes a curated catalog of applications that install silently via winget. Select what you want in **Menu → Install apps**, then include the *Install Selected Apps* phase in your run.

| Category | Apps |
|---|---|
| **Browsers** | Firefox, Brave, Chrome, LibreWolf, Vivaldi |
| **Utilities** | 7-Zip, WinRAR, Notepad++, Everything, PowerToys, ShareX, Rufus |
| **Cleanup** | BleachBit, CCleaner, Revo Uninstaller, WizTree |
| **Security** | Malwarebytes, Bitdefender Free, KeePassXC, Bitwarden, Cryptomator |
| **Communication** | Discord, Telegram, Signal, Thunderbird |
| **Media** | VLC, mpv, foobar2000, OBS Studio, HandBrake, Audacity |
| **Development** | Git, VS Code, Python 3.12, Node.js LTS, Windows Terminal |
| **Gaming** | Steam, Epic Games Launcher, GOG Galaxy, Heroic Games Launcher |

---

## Uninstall Apps

The Uninstall screen (Menu → Uninstall apps) lists every installed program on the machine — both classic Win32 installers and modern AppX packages — and lets you select and remove them in a batch.

Safety is built in: System and Driver entries are **locked** and cannot be selected. Critical packages (Windows Store, VCLibs, Desktop App Installer, Security Health, WindowsAppRuntime) are protected even from the standard user list. A pre-uninstall System Restore point is offered before any batch removal executes.

---

## Undo Center

Every Antidote run creates a timestamped backup before it makes a single change. The Undo Center (Menu → Tools → Undo Center) lists every backup and lets you restore:

- **Registry** — the values written by performance, FPS, network, and debloat phases
- **Service states** — startup types and running states of the services Antidote modifies
- **Restore point** — Windows own restore point created at the start of the run

---

## Sentinel Mode

Sentinel Mode (Menu → Tools → Sentinel Mode) installs a scheduled task that runs in the background every 6 hours and silently re-applies your privacy settings if Windows has reversed them.

It monitors and corrects:
- **DiagTrack** (telemetry service) — stops it and sets it to Disabled if Windows re-enables it
- **AllowTelemetry** — resets to 0 if the value has been changed
- **Content Delivery Manager** — re-disables Start menu suggestion ads and lockscreen suggestions

Sentinel never modifies anything beyond what Antidote's debloat phase already set. It runs as administrator via the Task Scheduler and produces a log entry each time it checks.

---

## Privacy Leak Visualizer

The Privacy Visualizer (Menu → Tools → Privacy Visualizer) shows a read-only breakdown of your current privacy state — which telemetry endpoints and data collection settings are blocked, which are still active, and your current Privacy Score. It requires no run to open; it reads the live system state directly.

---

## Game Library Optimizer

The Game Library Optimizer (Menu → Tools → Game Library Optimizer) scans for installed games across Steam and Minecraft (including Modrinth modpack instances) and applies per-game tweaks:

- Reads Steam's library VDF to find all installed game folders across all Steam library locations
- Detects Java / javaw.exe for Minecraft-type launchers
- Applies process priority and CPU affinity hints for detected games
- Optionally generates a tuned JVM arguments file for Minecraft instances
- Optionally adjusts `options.txt` render settings toward saner defaults (with a backup first)
- All tweaks are local — no internet connection required

---

## Auto-updater

Antidote checks for new releases automatically against the GitHub releases API. When a newer version is found, you can download and install it directly from within the app. The updater:

- Compares your installed version against the latest GitHub release (with correct handling of .NET Version semantics)
- Downloads the installer to a temporary location with live progress
- Uses a trampoline mechanism (a generated `.cmd` file) to safely replace the running executable — which cannot update itself while running
- Re-launches Antidote after the update completes

---

## Settings persistence

Antidote remembers your choices between sessions — no reconfiguring every time you open it.

| Setting | Saved |
|---|---|
| Light / Dark theme | ✅ |
| Accent color | ✅ |
| Selected phases | ✅ |
| Selected apps | ✅ |
| Dry Run toggle | ✅ |
| Sentinel Mode on/off | ✅ |
| Ambient music on/off + volume | ✅ |
| Last used preset | ✅ |

Settings are stored in `%APPDATA%\Antidote\settings.json` and written atomically (temp-file-then-move) so a crash during save can never corrupt your configuration.

---

## Theming

Antidote ships with a full Frutiger Aero aesthetic in both Light and Dark mode, with selectable accent colors. Every element follows the theme — cards, dialogs, progress bars, checkboxes, menus, the System Map, and every secondary window. The title bar tints to match the accent in both light and dark on Windows 11.

Available accent hues: **Green Cyan** (default) · **Purple** · **Blue** · **Red** · **Teal** · **Yellow Green** · **Red Violet**

An optional rainbow outline mode cycles the accent through the full spectrum continuously.

---

## Logging

Every run produces a timestamped log file at `%APPDATA%\Antidote\logs\`. The log records every step executed, its result, any errors, the final phase/step summary, and elapsed time. Logs stream to disk line by line during the run — if the process is killed mid-run (e.g. during a long DISM operation), the log up to that point is preserved.

---

## System requirements

| | |
|---|---|
| **Operating System** | Windows 10 (version 1903 or later) or Windows 11 |
| **Architecture** | x64 only |
| **RAM** | 2 GB minimum free |
| **Privileges** | Administrator — required. Most phases modify HKLM registry, stop services, or manage scheduled tasks. |
| **Runtime** | .NET 9 (included in the installer) |
| **Disk** | ~50 MB for the application |

---

## A note on SmartScreen

When you download and run the installer, Windows SmartScreen may warn you that the application is from an unknown publisher. This is expected — the application is not yet code-signed. A code-signing certificate is actively being worked toward (it is one of the things donations go toward). The full source code is available on GitHub for inspection.

To proceed: click **More info → Run anyway**.

---

## Support the project

Antidote is free and will stay free. If it's been useful to you and you'd like to support its development:

- 🪙 **Crypto** — [nowpayments.io/donation/Tripartitus](https://nowpayments.io/donation/Tripartitus)
- ☕ **Cash** — [buymeacoffee.com/tripartitus](https://buymeacoffee.com/tripartitus)

Donations go toward maintenance, a code-signing certificate, and the tooling and time that goes into continued development. Entirely voluntary — the software does not change based on whether you donate.

---

## Find the developer

| | |
|---|---|
| 🎮 Twitch | [twitch.tv/tripartitusgaming](https://www.twitch.tv/tripartitusgaming) |
| 📺 YouTube | [youtube.com/@TripartitusGaming](https://www.youtube.com/@TripartitusGaming) |

---

<div align="center">

*Antidote v2.4 · Windows optimization done right · Free for everyone, always*

</div>
