# 🎮 WowPresence

Native Discord Rich Presence for **World of Warcraft 1.12.1 (build 5875)** and compatible clients.

Focused on a **small game-side footprint, stable character detection and native Discord IPC**.

> WowPresence targets **WoW 1.12.1 / build 5875-compatible client environments**.

## 🔌 Requirements

- **World of Warcraft 1.12.1 (build 5875)** or a compatible client
- **Discord Desktop**
- A compatible DLL loader such as **VanillaFixes**
- A free **Discord Application ID**

The DLL only samples character information from the game. Discord communication is handled by a separate companion process.

## 📦 Installation

1. Download **\`WowPresence.zip\`** from Releases.
2. Extract the ZIP directly into your WoW game directory.
3. Open:

\`\`\`text
.modernization_tool\WowPresence\discord_application_id
\`\`\`

4. Replace the placeholder text with **your numeric Discord Application ID**.
5. Add \`WowPresence.dll\` to your VanillaFixes \`dlls.txt\`.
6. Launch WoW normally through VanillaFixes.

After extraction:

\`\`\`text
<WoW folder>\
├─ WowPresence.dll
├─ WowPresence.exe
└─ .modernization_tool\
   └─ WowPresence\
      ├─ discord_application_id
      └─ discord_broadcast_flags
\`\`\`

\`WowPresence.exe\` is started automatically by the DLL and normally does **not** need to be launched manually.

## 🛰️ Discord Application ID

WowPresence intentionally does **not** include a server-specific Discord Application ID.

To create yours:

1. Open the **Discord Developer Portal**: https://discord.com/developers/applications
2. Create a **New Application**.
3. Give it the name you want Discord to display.
4. Open **General Information**.
5. Copy the **Application ID**.
6. Paste only that numeric ID into:

\`\`\`text
.modernization_tool\WowPresence\discord_application_id
\`\`\`

Example:

\`\`\`text
123456789012345678
\`\`\`

No Discord Client Secret, bot token, or bot account is used or required.

If the file is missing or invalid, WowPresence leaves Rich Presence disabled and records the reason in \`WowPresence.log\`.

## ✨ Features

- Discord Rich Presence for WoW 1.12.1.
- Character name and guild display.
- Level and class display.
- Race and faction display.
- Current zone display.
- Stable elapsed-session timer across character changes.
- Automatic companion startup.
- Exact WoW process tracking.
- Read-only game-memory sampling.
- Native Discord IPC with no bot or Client Secret required.
- Optional privacy flags for individual character fields.

## 🔧 Compatibility

### Tested

- **OctoWoW** — WoW 1.12.1 / build 5875 based client

### Expected compatible

- **World of Warcraft 1.12.1 build 5875**
- Private-server clients preserving the relevant 1.12.1 client memory layout

### Not compatible

- WoW Classic Era 1.14.x
- The Burning Crusade Classic
- Wrath of the Lich King Classic
- Retail World of Warcraft

Other modified 1.12.1 clients should be considered **untested until verified**.

## ⚙️ How it works

\`\`\`text
WoW
 └─ WowPresence.dll
      ├─ read-only character sampling
      ├─ local JSON status
      └─ starts WowPresence.exe
             └─ Discord local IPC
\`\`\`

The DLL does not communicate directly with Discord.

The companion executable does not read or write WoW memory.

Character status is written to:

\`\`\`text
.modernization_tool\WowPresence\discord_wow_status.json
\`\`\`

The companion log is written to:

\`\`\`text
.modernization_tool\WowPresence\WowPresence.log
\`\`\`

These runtime files are created automatically.

## 🔒 Privacy flags

The included file:

\`\`\`text
.modernization_tool\WowPresence\discord_broadcast_flags
\`\`\`

controls which character details are published to Discord.

| Value | Field |
| ---: | --- |
| 1 | Name |
| 2 | Guild |
| 4 | Faction |
| 8 | Class |
| 16 | Level |
| 32 | Zone |
| 63 | All fields |

The release package uses \`63\` by default.

If the file is deleted, WowPresence also defaults to all supported fields.

## 🛡️ Administrator privileges

Discord and WoW should run with matching privilege levels.

If Discord runs as administrator, WoW must also run as administrator for local Rich Presence IPC to work reliably.

Running both normally is recommended unless elevation is required by the local setup.

## 🛠️ Building

WowPresence targets **32-bit x86 Windows**, matching WoW 1.12.1.

With an x86 MSVC developer environment:

\`\`\`bat
cl /nologo /O2 /MT /W3 /LD src\WowPresence.c /Fe:WowPresence.dll /link /INCREMENTAL:NO
cl /nologo /O2 /MT /W3 src\WowPresenceLauncher.c user32.lib /Fe:WowPresence.exe /link /SUBSYSTEM:WINDOWS /INCREMENTAL:NO
\`\`\`

GitHub Actions builds:

- \`WowPresence.dll\`
- \`WowPresence.exe\`
- \`WowPresence.zip\`

The ZIP also includes the ready-to-edit configuration files.

Tags matching \`v*\` can publish these files as a GitHub Release.

## 📜 Project identity & licensing

WowPresence is an **independent community project**.

Compatibility with **World of Warcraft**, **Discord**, **OctoWoW**, **VanillaFixes**, **IchaLaunch**, or other referenced projects does not imply affiliation, endorsement, sponsorship, or ownership by their respective rights holders or maintainers.

**World of Warcraft**, **Warcraft**, **Blizzard Entertainment**, **Discord**, and related names and marks remain the property of their respective rights holders.

This repository does not currently declare a software license.

For detailed provenance and third-party information, see:

- [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)

## 🙏 Credits

WowPresence is maintained by **Dusk-92**.

The project was inspired in part by the WoW character-status / Discord Rich Presence implementation in **IchaLaunch** by **brutaliccus**.

The current WowPresence implementation is maintained separately and does not include IchaLaunch binaries.
