<div align="center">

# Antidote
### Optimization, Cleanup, Debloat & Privacy Hardening — now on Windows, Linux & Android

**Free to use. Built for everyone.**

[![Windows](https://img.shields.io/badge/Windows%2010%20%7C%2011-v2.5-blue?style=flat-square)](https://github.com/Tripartitus/Antidote/releases)
[![Linux](https://img.shields.io/badge/Linux%20(Flatpak)-v0.4.8-orange?style=flat-square)](https://github.com/Tripartitus/Antidote/releases)
[![Android](https://img.shields.io/badge/Android-v0.6-green?style=flat-square)](https://github.com/Tripartitus/Antidote/releases)
[![License](https://img.shields.io/badge/license-free%20to%20use-lightgrey?style=flat-square)](https://github.com/Tripartitus/Antidote)

*by [Tripartitus](https://github.com/Tripartitus) — [Twitch](https://www.twitch.tv/tripartitusgaming) · [YouTube](https://www.youtube.com/@TripartitusGaming) · [GitHub](https://github.com/Tripartitus)*

</div>

---

## What is Antidote?

Antidote does what your operating system should have let you do from the start —
remove the bloat, silence the telemetry, tune performance, clean the junk, and
take back control of your machine. It's a proper application with a modern,
themed interface, not a script you squint at in a terminal.

It's not a magic speed-doubler or a snake-oil cleaner. Every change it makes is
documented, most are reversible, and nothing important happens without a
confirmation. **Antidote is free for everyone — no Pro version, no feature
gating.**

Antidote now runs on **three platforms**, each built natively for its system
and sharing the same design DNA: a phase/step model, Safe/Moderate/Aggressive
risk levels, a dry-run preview, presets, per-phase explanations, a live log, and
the full Tripartitus theming.

---

## Pick your platform

| Platform | Edition | Built with | Status |
|---|---|---|---|
| 🪟 **Windows 10 / 11** | Antidote | C# / .NET 9, WinForms | Mature — the original |
| 🐧 **Linux (Ubuntu/Debian)** | Antidote for Linux | Python + GTK4 / libadwaita, Flatpak | Active — v0.2 |
| 🤖 **Android** | Antidote for Android | Kotlin + Jetpack Compose | Active — v0.6 |

All three share the same look and the same core idea. What each can *do*
differs, because each OS allows different things — and each edition is honest in
its own UI about where the limits are.

---

# 🪟 Windows edition

The original and most complete edition. A Windows optimization tool built as a
modern themed desktop app.

**Maintenance & repair:** System Restore point, DISM + SFC repair, chkdsk,
deep cleanup (temp / Update cache / Prefetch / error reports), browser cleanup,
TRIM for SSDs and defrag for HDDs.

**Performance:** High-Performance power plan + GPU scheduling, MMCSS / latency
tweaks, Game DVR off, memory optimization, per-process priority & affinity, and
optional VBS / Memory Integrity disable for older hardware.

**Privacy & debloat:** removes AppX bloatware, disables DiagTrack, Cortana, Bing
in Start, Recall / AI snapshots, advertising ID, and location tracking; an
enterprise-level deep telemetry block; and browser hardening for Edge & Chrome.

**Standout features:** a 22-check **System Health Score** with a hardware
ceiling, **Smart Optimize**, a live animated **System Map**, **Sentinel Mode**
(re-applies privacy settings every 6 hours if Windows reverts them), a
**Privacy Leak Visualizer**, a **Game Library Optimizer** (Steam + Minecraft),
an **App Catalog** and **Uninstaller** driven by winget, an **Undo Center**, and
a GitHub auto-updater.

**Requirements:** Windows 10 (1903+) or 11, x64, administrator, .NET 9
(included). See the Windows release notes for the full phase list.

---

# 🐧 Linux edition (v0.2)

A native port for Ubuntu and Debian-based systems, written in Python with
GTK4 / libadwaita and shipped as a single **`.flatpak`**. Every Windows
operation is mapped to its real Linux equivalent — nothing is faked.

**Five tabs:**

- **Maintenance** — restore point (Timeshift + package manifest), dpkg/apt
  repair, deep cleanup (caches, `/tmp`, journal, apt, trash), `apt full-upgrade`
  + `flatpak` + `snap` + `fwupd` updates, `fstrim`, power profile, BBR network
  tweaks, debloat (disable apport/whoopsie/popcon/ubuntu-report), `/etc/hosts`
  tracker blocklist, GNOME privacy settings, dependency install, and an app
  catalog (apt + Flatpak).
- **Network** — a graphical device viewer with per-device icons (phone,
  computer, router, TV, printer, console, IoT) and an honest **internet-block**
  action (real FORWARD-drop if this machine is the gateway, otherwise router
  guidance).
- **Security** — install a firewall (UFW + gufw), install anti-malware (ClamAV +
  ClamTk + rkhunter), and run home / full / rootkit scans.
- **Drivers** — real firmware/BIOS updates via `fwupd`, GPU driver install via
  `ubuntu-drivers`, and a read-only hardware inventory (GPU, chipset, USB, CPU,
  memory, firmware). No fake "chipset driver downloader" — those live in the
  kernel.
- **Tools** — three Linux-only abilities: a **security** audit (open ports,
  failed logins, SUID binaries), **privacy** hardening (MAC randomization,
  secure free-space wipe), and a **forensics** timeline (login/USB/boot
  history).

Plus full 8-accent light/dark theming, persisted settings, the banner, the
About-the-developer page, and a GitHub updater that scans all releases for the
newest `.flatpak`.

**Install:**

```bash
flatpak install --user antidote-v0.2.0.flatpak
flatpak run com.tripartitus.Antidote
```

**Build from source:** install `flatpak` + `flatpak-builder`, add Flathub, then
run `packaging/build-flatpak.sh` (or follow the README). Needs the GNOME runtime
matching your system (47 / 48 / 50).

---

# 🤖 Android edition (v0.6)

A native Android app in Kotlin + Jetpack Compose, carrying the same Frutiger
Aero look, the 8 accent hues, light/dark/sepia/system themes, the banner, and
the About-the-developer page.

**The honest difference:** Android won't let an app host a root shell, so
Antidote for Android uses a **three-tier execution backend**, and every action
declares the privilege it needs. The UI shows your current tier and greys out
anything above it — that honesty is the product.

| Tier | How | What it unlocks |
|---|---|---|
| **T0 — No privilege** | Normal SDK APIs in the app sandbox | Own cache/files, app inventory (`PackageManager`), uninstall prompts, Settings deep-links, usage-access |
| **T1 — Shizuku / ADB** | [Shizuku](https://shizuku.rikka.app) (no root; survives reboot via wireless debugging) | Clear other apps' cache/data, disable/uninstall-for-user, `settings put`, `appops`, grant runtime perms |
| **T2 — Root** | [`libsu`](https://github.com/topjohnwu/libsu) | Everything: protected settings, `/data` cleaning, hosts-file blocking, per-app firewall |

It ships a **Shizuku onboarding** tool (no bootloader unlock needed), a guided
**de-Google history** center (Google blocks automating account-history
deletion, so the app opens each page with exact steps rather than pretending),
an **F-Droid / IzzyOnDroid** install catalog, a system/user-aware
**uninstaller**, DataStore-backed settings, live logs, and a GitHub
auto-updater that installs via `PackageInstaller`.

---

## Shared design principles (all editions)

**Reversible by default.** Reverse phases and undo paths exist so changes aren't
permanent. The few exceptions (e.g. app removal) are stated plainly in the UI
before they run.

**Nothing hidden.** Every phase has an explanation that reads like a real one,
not marketing copy. Dry-run mode shows exactly what would happen without
changing anything.

**Honest about limits.** Each edition tells you what its OS won't allow rather
than faking it — Linux's kernel-driver model, Android's privilege tiers and
Google-history restrictions, and so on.

**Safety first.** A restore point / snapshot / backup is the first recommended
step, and aggressive actions require confirmation.

---

## Theming

All three editions ship the full Frutiger Aero aesthetic in **light and dark**
with selectable accent colours, carried from the original Windows palette:
**Green-cyan** (default) · **Purple** · **Blue** · **Red** · **Pink** ·
**Red-violet** · **Yellow-green** · **Orange**. Your theme and accent persist
between launches.

---

## Support the project

Antidote is free and will stay free. If it's been useful and you'd like to
support development:

- 🪙 **Crypto** — [nowpayments.io/donation/Tripartitus](https://nowpayments.io/donation/Tripartitus)
- ☕ **Cash** — [buymeacoffee.com/tripartitus](https://buymeacoffee.com/tripartitus)

Entirely voluntary — the software never changes based on whether you donate.

---

## Find the developer

| | |
|---|---|
| 🎮 Twitch | [twitch.tv/tripartitusgaming](https://www.twitch.tv/tripartitusgaming) |
| 📺 YouTube | [youtube.com/@TripartitusGaming](https://www.youtube.com/@TripartitusGaming) |
| 🐙 GitHub | [github.com/Tripartitus](https://github.com/Tripartitus) |

---

<div align="center">

*Antidote · Windows · Linux · Android · Free for everyone, always*

</div>
