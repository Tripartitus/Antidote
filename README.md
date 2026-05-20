<p align="center">
  <img src="https://cdn.corenexis.com/files/c/6264165720.png" alt="Antidote Logo" width="48">
</p>

<h1 align="center">Antidote</h1>

<p align="center">
  <strong>A modern Windows optimization, debloat, and privacy toolkit with a clean GUI</strong><br>
  <em>By Tripartitus</em>
</p>

---
![Screenshot](https://cdn.corenexis.com/files/c/3335384720.png)
**Antidote is a complete rework and major update of my previous project, Win11GS (Windows 11 Gamer Setup).**  
It features a brand-new UI, a genuine icon, dozens of additions, and extensive fixes while keeping the core philosophy of the original.

## What Is Antidote?

Antidote is a one-stop tuning utility for Windows 10 and Windows 11. It bundles dozens of system maintenance, performance, privacy, and cleanup tasks behind a simple checkbox interface. Pick exactly what you want, preview safely in dry-run mode, and run.

Every action is reversible (via built-in restore point, explicit REVERSE phases, or re-running Windows defaults). Every option includes a detailed in-app explanation so you know exactly what it does before committing.

## Who It's For

Antidote is for **anyone** running Windows — not just gamers:

- **Gamers** — reduce background overhead, lower input latency, free RAM, and enable GPU scheduling for better frame rates.
- **Privacy-conscious users** — disable telemetry, ads, Recall, Copilot, and Cortana in one click.
- **Power users** — bulk-install and update dozens of apps via winget, and clean years of junk.
- **IT pros & technicians** — standardize cleanup and debloat across machines without memorizing PowerShell commands.
- **New PC setups** — go from fresh Windows install to clean, fast, and configured in minutes.
- **Slow or cluttered PCs** — clear caches, repair the OS image, and reset network defaults without a full reinstall.

## Key Features

- **Opt-in everything** — sensible defaults selected; only run what you choose.
- **Dry-run mode** — preview every change without touching your system.
- **Built-in restore point** — automatic Windows restore point before any modifications.
- **In-app explanations** — every option has an "Info" button with full details, trade-offs, and how to undo it.
- **Reverse phases** — dedicated undo options for network and registry tweaks.
- **Bulk app installer** — 40+ curated apps installable at once via winget.
- **Bulk app uninstaller** — remove any installed program (AppX or classic) with search and select-all.
- **Light & dark themes** — clean Aero-Frutiger inspired design with one-click toggle.
- **Persistent settings** — remembers your phase selections, app choices, theme, and dry-run preference.
- **Detailed logs** — every action logged to `%APPDATA%\Antidote\logs\` with one-click folder access.
- **Cancel anytime** — running phases can be stopped mid-process; GUI stays responsive.
- **UAC-aware** — auto-elevates to administrator on launch.

## Available Phases

Each phase is independent and toggleable. **on** = recommended default for most users. **off** = off by default.

### Safety
- **Create System Restore Point** — Creates a Windows restore point before any changes. Roll back everything from System Properties if needed.

### Health & Repair
- **System Repair (DISM + SFC)** — Runs DISM health checks and `sfc /scannow` to repair the component store and fix corrupted system files.
- **Disk Health Scan (chkdsk)** — Read-only scan of the C: drive. Can take 30–60 minutes; recommended after power loss or improper shutdowns.

### Cleanup
- **Deep Cleanup (Temp + Performance Junk)** — Clears temp folders, Prefetch, Windows Update downloads, thumbnail caches, Recycle Bin, Recent files, jump lists, and error reports. Often recovers many GB.

### Disk
- **Disk Optimization (TRIM / Defrag)** — Automatically runs TRIM on SSDs or defragmentation on HDDs to maintain performance.

### Performance
- **Power Plan + GPU Scheduling** — Activates Ultimate Performance plan, sets visual effects to "best performance", and enables Hardware-Accelerated GPU Scheduling.
- **Advanced FPS / Latency Tweaks** — Applies registry tweaks for lower latency: MMCSS priority, network throttle off, Game DVR off, fullscreen optimizations off, mouse acceleration off, and NDU service disabled.
- **Disable VBS / Memory Integrity** — Turns off Virtualization-Based Security. Can boost FPS 5–15% in CPU-bound games (security trade-off — read the in-app Info first).

### Network
- **Network Low-Latency Tweaks** — Flushes DNS, resets Winsock/IP stack, sets TCP autotuning to normal, and disables Nagle's algorithm on active adapters.
- **REVERSE: Network Tweaks** — Restores Windows defaults for Nagle's algorithm and TCP autotuning. Use if tweaks feel worse or for troubleshooting.

### Debloat & Privacy
- **Debloat + Privacy Hardening** — Removes preinstalled AppX bloatware (News, Weather, Skype, Copilot, Recall, etc.), cleanly uninstalls OneDrive, disables telemetry services, and applies registry policies to turn off Cortana, web search, location tracking, ads, Windows AI, Edge metrics, and feedback.
- **REVERSE: Registry Tweaks** — Reverts all registry and service changes from the FPS/Latency and Debloat phases. Does **not** reinstall removed AppX apps (retrieve from Microsoft Store if needed).

### Updates & Apps
- **Check for Application Updates** — Auto-installs winget if missing, then silently upgrades all winget-supported applications.
- **Install Dependencies (Runtimes)** — Installs all Visual C++ Redistributables (2005–2022), modern .NET runtimes, and legacy DirectX components.
- **Install Selected Apps** — Installs apps you choose from the 40+ app catalog (see below).

## Application Catalog

The "Choose apps to install" window offers 40+ curated apps grouped by category. Select what you want — Antidote installs them all silently via winget.

**Browsers**: Mozilla Firefox · Brave · Google Chrome · LibreWolf · Vivaldi  
**Utilities**: 7-Zip · WinRAR · Notepad++ · Everything · PowerToys · ShareX · Rufus  
**Cleanup**: BleachBit · CCleaner · Revo Uninstaller · WizTree  
**Security**: Malwarebytes · Bitdefender Free · KeePassXC · Bitwarden · Cryptomator  
**Communication**: Discord · Telegram · Signal · Thunderbird  
**Media**: VLC · mpv · foobar2000 · OBS Studio · HandBrake · Audacity  
**Development**: Git · Python · Node.js LTS · VS Code · Windows Terminal  
**Gaming**: Steam · Epic Games Launcher · GOG Galaxy · Heroic Games Launcher  

A separate "Uninstall apps..." window lets you remove any currently installed program (AppX or classic) with search, multi-select, and optional pre-uninstall restore point.

## Screenshots

*(Add screenshots of the main window, App Chooser, Info dialog, and progress view here.)*

## Installation & Usage

1. Download `Antidote.exe` (and `Banner.png`) from the latest release.
2. Right-click → **Run as administrator** (or double-click — UAC prompt appears automatically).
3. Review the phase list. Defaults are safe for most users — many people just click **Run**.
4. **Recommended on first run**: Check **Dry Run** first to preview exactly what will happen.
5. Click **Run selected phases**. You can cancel at any time.
6. Logs are saved to `%APPDATA%\Antidote\logs\`. Use the **Open log folder** button to view them.

A reboot is recommended after the first full run — some registry changes take effect after sign-out or restart.

## Compatibility

- **Windows 11** — Fully supported (all features active).
- **Windows 10 (1809 and newer)** — Fully supported. Windows-11-only features (Recall, Copilot policies) silently no-op.
- **Older Windows versions** — Not supported.

## Safety & Disclaimer

Antidote modifies system settings, services, registry keys, and installed packages. Defaults are conservative and reversible. Every phase has an in-app **Info** button explaining trade-offs.

**Important notes:**
- Always enable **Create System Restore Point** on your first run.
- Read the Info dialog before enabling security trade-off phases (e.g., Disable VBS / Memory Integrity).
- The Debloat phase permanently removes AppX packages. Registry/service changes are reversible via the REVERSE phase, but removed apps are not automatically restored.
- This software is provided **as-is** with no warranty. Use at your own risk.

For most users, running the defaults results in a noticeably faster, cleaner, and more private Windows experience.

## Logs & Settings

- **Logs**: `%APPDATA%\Antidote\logs\Antidote_YYYYMMDD_HHmmss.log`
- **Settings** (phase selection, theme, app picks, dry-run state): `%APPDATA%\Antidote\settings.json`

## Credits

Created and maintained by **Tripartitus**.

This is a self-made project. Every phase, line of UI code, and default setting is the result of extensive testing and tuning. If Antidote saved you time, a star on the repo is greatly appreciated!

---

*Antidote — the cleaner, modern successor to Win11GS.*
