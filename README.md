# WARP0716

WARP patches for the 2025-07-16 client build. This build of WARP **only accepts the 2025-07-16 client EXE** — it will reject any other version.

15 patches fixed for 07-16 compatibility, 20+ dead patches removed, all patch descriptions rewritten, and CustomJobs fully implemented. **0 errors on all-patch test** (patches apply cleanly — does not guarantee every feature works as intended in-game; if you find something off, please [open an issue](https://github.com/CrazyBebop/WARP0716/issues)).

## Setup

1. Launch `win32/WARP.exe`
2. Load your unpacked exe
3. Select your patches and apply

## Recommended Patches

Click **"Recommended"** in the WARP GUI to select all recommended patches at once. A YAML profile is also included at `profiles/community_recommended.yml` for reference.

42 patches are marked as recommended — this is the minimal set to get a working English client.

## What's New

### Patch Fixes (18 patches fixed for 07-16)
- **CallKoreaClientInfo** — Fixed pattern matching for 07-16
- **NoEarthQuake** — Fixed string match hitting wrong target
- **NoEquipWinTitle** — Window struct offsets shifted +0x20
- **CustomShields** — VS2022 compiler change workaround
- **CustomCharCreateId** — Fixed for VC14.29 stack frame layout
- **IgnoreEntryQueueErr** — Fixed for VS2022 code generation
- **MoveUpItemCount** — Fixed for VS2022 instruction changes
- **AllowSkillSpam** — Fixed step ID syntax
- **CustomMissingLauncherMsg** — Fixed pattern + validate fallback
- **LowCamAngle / MediumCamAngle / HighCamAngle** — Fixed address width for 07-16
- **HideBuildInfo** — Rewritten as plaintext .qjs (was encrypted .ejs)
- **CustomIcon** — Rewritten to support any icon size/format
- **NoGGuard** — Fixed RagHash.dat crash (stale file no longer crashes client)
- **GRFsFromIni** — Fixed crash on invalid DATA.INI entries

### CustomJobs — Implemented (Needs Testing)
All job tables are now driven by Lua files — add custom jobs without binary patching. Covers job display names, male/female sprite paths, palette tables, and head sprite tables. **This patch still needs in-game testing — please report any issues.**

### Patches Not Needed on 07-16
These are already handled or don't apply to this client version:
- **NoLoginOTP** / **EnableDnsSupport** — Already patched in the EXE before WARP
- **HidePacketsFromPEEK** — 07-16 has native anti-PEEK protection
- **NoFilenameCheck** — Gravity removed the filename check
- **NoHShield** / **NoCDefender** — Neither protection exists in 07-16
- **RestoreLoginWindow** — Login window exists natively
- 14 additional date-locked or version-specific patches removed (pre-2018/2019/2022 only)

### User-Friendly Improvements
- **Title bar** shows "WARP for 2025-07-16"
- **"Loaded Date"** renamed to **"Client Date"**
- **Patch descriptions rewritten** — Every patch now explains what it does in plain language
- **Recommend flags reviewed** — Commonly needed patches default to recommended
- **Custom\*Lub patches** — Input now shows recommended `SystemEN/` path for llchrisll Translation Project users
- **Translations_EN.yml** cleaned from 157 to 16 working entries
- **AddLuaOverrides** link updated to current documentation

### Known Conflict
**NoPassEncr** requires **UseOldLogin**. Do not enable both **UseSSOLogin** and **NoPassEncr** — the WARP GUI handles this automatically via mutex groups, but YAML profiles need manual care.

## Downloads

**Full Client:** [2025-12-04 Client](https://drive.google.com/file/d/1ugolNYp6vQE0Hzmwuj359LbgcwraiZgu/view) (Provided by Skylove) — This is the last known working 2025 client. However, **Prontera map files are still needed**, along with the client executable linked below.

**Client EXE:** [2025-07-16_Ragexe_175220998_clientinfo.zip](https://mirror2.romirrors.com/downloads/2025-07-16_Ragexe_175220998_clientinfo.zip) — Unpacked 2025-07-16 client EXE, ready for WARP patching.

**Translation Project:** [llchrisll Translation Project](https://github.com/llchrisll/ROenglishRE/) — English translation for the client. Provides translated lua files and system files.

## GRF

If you have your own client you wish to use, I recommend using this GRF:

**Download:** [GRF Pack](https://drive.google.com/file/d/1ugolNYp6vQE0Hzmwuj359LbgcwraiZgu/view?usp=drive_link) (2025-12-04 by Skylove)

Contains `data.grf` and `2025-06-04.grf` with lua files and map data. If you're using the [llchrisll Translation Project](https://llchrisll.github.io/ROTPDocs/), the lua files are **not needed** — the translation project provides its own.

However, the Prontera map files (`prontera.gat`, `prontera.gnd`, `prontera.rsw`) **are required** regardless. They can be extracted from `2025-06-04.grf`, or use your own if you already have working Prontera map files. If placing them in your `data/` folder, enable the **DataFolderFirst** patch.

## Issues & Suggestions

Found a bug or have a suggestion? Post it in the [Issues](https://github.com/CrazyBebop/WARP0716/issues) section.

## Donate

<a href="https://www.buymeacoffee.com/crazybebop"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-blue.png" height="60" width="217" alt="Buy Me A Coffee"></a>

## Credits

Built on [WARP](https://github.com/Neo-Mind/WARP) by Neo-Mind and [Warp2025](https://github.com/hiphop9/Warp2025) by hiphop9.
