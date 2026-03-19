# WARP0716

WARP patches for the 2025-07-16 client build. This build of WARP **only accepts the 2025-07-16 client EXE** — it will reject any other version.

21 patches fixed for 07-16 compatibility, 20+ dead patches removed, all patch descriptions rewritten, Custom Jobs (Reforged) fully implemented with 19 binary phases, and Custom Fonts (Reforged) rewritten for modern Windows (T2Embed → AddFontResourceExA). **0 errors on all-patch test** (patches apply cleanly — does not guarantee every feature works as intended in-game; if you find something off, please [open an issue](https://github.com/CrazyBebop/WARP0716/issues)).

## Setup

1. Launch `win32/WARP.exe`
2. Load your unpacked exe
3. Select your patches and apply

## Recommended Patches

Click **"Recommended"** in the WARP GUI to select all recommended patches at once. A YAML profile is also included at `profiles/community_recommended.yml` for reference.

42 patches are marked as recommended — this is the minimal set to get a working English client.

## What's New

### Patch Fixes (21 patches fixed for 07-16)
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
- **IncreaseHairsLimit** — Fixed compatibility with CustomJobs (both patches modify same memory)
- **EnableCustomFonts** — Full rewrite: T2Embed broken on modern Windows, now loads .ttf via AddFontResourceExA with face name fixes
- **FixFontsCharset** — Fixed EDI register clobber causing crash in MultiByteToWideChar

### Custom Fonts (Reforged) — Full Rewrite
Microsoft's T2Embed font loading API is broken on modern Windows — `.eot` fonts silently fail to load. This rewrite bypasses T2Embed and loads pre-converted `.ttf` fonts via `AddFontResourceExA`. WARP prompts to copy the included `.ttf` files to your client on apply. All 9 `@font` styles work. Users can also replace any `.ttf` in `System\Font\` with their own custom font (client-side only). See [CHANGELOG.md](CHANGELOG.md) for technical details.

### Custom Jobs (Reforged) — 19 Phases, Full Rewrite
Add custom jobs to your server without binary patching — just edit 7 Lua files. Supports baby classes (0.75x scaling), multi-tier skill trees (like Night Watch), mount integration (Boarding Halter), and error display for Lua loading issues. Includes a working example with baby variant. See the [Custom Jobs Guide](docs/CustomJobs/CUSTOM_JOBS_GUIDE.html) or [view online](https://legacygamers.net/docs/public/customjobs-reforged/) for full setup instructions. For more details, read the [CHANGELOG.md](CHANGELOG.md). Please [report any issues](https://github.com/CrazyBebop/WARP0716/issues).

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

You need these to set up a working client:

1. **Client + Data GRF:** [Client+Data.grf](https://drive.google.com/file/d/1ugolNYp6vQE0Hzmwuj359LbgcwraiZgu/view?usp=drive_link) (December 4th, 2025) — Provided by Skylove
2. **Translation Project:** [llchrisll/ROenglishRE](https://github.com/llchrisll/ROenglishRE/) — Use the ClientGenerator, last option **[24] 2025-01-22**
3. **Client EXE:** [2025-07-16_Ragexe_175220998_clientinfo.zip](https://mirror2.romirrors.com/downloads/2025-07-16_Ragexe_175220998_clientinfo.zip) — Unpacked EXE, ready for WARP patching
4. **WARP** — Apply **Recommended** or use `profiles/community_recommended.yml` + your own patches

Then create a `data/` folder or GRF with your server's custom content (JobInfo Lua files, job sprites, Prontera map files, etc.) and add it to `DATA.INI`. Enable the **DataFolderFirst** patch if using loose files in `data/`, or pack into a GRF.

**Note:** The Prontera map files (`prontera.gat`, `prontera.gnd`, `prontera.rsw`) are **required** regardless of setup. They can be extracted from the GRF in step 1, or use your own if you already have them.

## Issues & Suggestions

Found a bug or have a suggestion? Post it in the [Issues](https://github.com/CrazyBebop/WARP0716/issues) section or join the [Discord](https://discord.gg/34hFYPse).

## Donate

It is never required, but if you feel the need to contribute to the project financially, you can do so by clicking the button below.

<a href="https://www.buymeacoffee.com/crazybebop"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-blue.png" height="60" width="217" alt="Buy Me A Coffee"></a>

**PayPal:** <a href="https://www.paypal.com/donate/?hosted_button_id=WW9FD6SLEZ5BN"><img src="https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif" alt="Donate via PayPal"></a>

Special thanks to the following donors so far: [saprobes](https://github.com/saprobes/), [Gerzzie](https://github.com/Gerzzie), [spike-ro](https://github.com/spike-ro), kikyam

## Credits

Built on [WARP](https://github.com/Neo-Mind/WARP) by Neo-Mind and [Warp2025](https://github.com/hiphop9/Warp2025) by hiphop9.
