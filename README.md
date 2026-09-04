# 🎮 WowPresence

Native Discord Rich Presence for **World of Warcraft 1.12.1 (build 5875)** and compatible clients.

Focused on **simple installation, read-only game sampling and native Discord IPC**.

> WowPresence targets **WoW 1.12.1 / build 5875-compatible client environments**.

## 🔌 Requirements

- **World of Warcraft 1.12.1 (build 5875)** or a compatible client
- **Discord Desktop**
- A compatible DLL loader such as **VanillaFixes**
- A free **Discord Application ID**

The DLL only reads character status from the game. Discord communication is handled by the separate `WowPresence.exe` companion process.

## 📦 Installation

1. Download **`WowPresence.zip`** from Releases.
2. Extract the ZIP directly into your WoW game directory.
3. Open:

```text
WowPresence\discord_application_id
```

4. Replace the placeholder with **your numeric Discord Application ID**.
5. Add `WowPresence.dll` to your VanillaFixes `dlls.txt`.
6. Launch WoW normally through VanillaFixes.

After extraction, the relevant files should look like this:

```text
<WoW folder>\
├─ WowPresence.dll
├─ WowPresence.exe
└─ WowPresence\
   ├─ discord_application_id
   └─ discord_broadcast_flags
```

`WowPresence.exe` is started automatically by the DLL and normally does **not** need to be launched manually.

The runtime JSON and log files are created automatically inside the same `WowPresence` folder.

When WowPresence is installed through the **[Modernization Tool](https://github.com/Dusk-92/Modernization-Tool)**, the same binaries automatically use:

```text
<WoW folder>\.modernization_tool\WowPresence\
```

instead. No separate build is required.

## 🛰️ Discord Application ID

To configure your own Discord Application ID:

1. Open the **Discord Developer Portal**: https://discord.com/developers/applications
2. Create a **New Application**.
3. Give it the name you want Discord to display.
4. Open **General Information**.
5. Copy the **Application ID**.
6. Paste only that numeric ID into:

```text
WowPresence\discord_application_id
```

Example:

```text
123456789012345678
```

For **OctoWoW**, you can use the preconfigured Discord Application ID:

```text
1544072796098011176
```

This is the same Application ID automatically configured by **Modernization Tool**.

No Discord Client Secret, bot token or bot account is used or required.

If `discord_application_id` is missing or invalid, Rich Presence remains disabled and the reason is written to `WowPresence\WowPresence.log`.

## ✨ Features

- Character name and guild display.
- Level and class display.
- Race and faction display.
- Current zone display resolved from the client AreaTable instead of heuristic text-address scanning.
- Stable elapsed-session timer across character changes.
- Automatic companion startup.
- Exact WoW process tracking.
- Read-only game-memory sampling.
- Native Discord IPC.
- Optional privacy flags for individual character fields.
- No bot, Client Secret or external service required.

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

```text
WoW
 └─ WowPresence.dll
      ├─ read-only character sampling
      ├─ Area ID → AreaTable zone resolution
      ├─ WowPresence\discord_wow_status.json
      └─ starts WowPresence.exe
             └─ Discord local IPC
```

Zone names are resolved from the player's current AreaTable ID, matching the client's own zone data and avoiding internal map tokens such as `H32D` or `HLVA`.

The DLL does not communicate directly with Discord.

The companion executable does not read or write WoW memory.

Runtime files are kept together in one of these locations:

**Standalone installation:**

```text
<WoW folder>\WowPresence\
├─ discord_application_id
├─ discord_broadcast_flags
├─ discord_wow_status.json
└─ WowPresence.log
```

**Installed through Modernization Tool:**

```text
<WoW folder>\.modernization_tool\WowPresence\
├─ discord_application_id
├─ discord_broadcast_flags
├─ discord_wow_status.json
└─ WowPresence.log
```

If the Modernization Tool managed folder exists, WowPresence automatically prefers it. Otherwise it uses the standalone `WowPresence` folder.

## 🔒 Discord Rich Presence privacy

WowPresence lets you choose exactly which character details are shown on Discord.

For a standalone installation, edit:

```text
WowPresence\discord_broadcast_flags
```

When WowPresence is installed through **Modernization Tool**, the equivalent file is stored in:

```text
.modernization_tool\WowPresence\discord_broadcast_flags
```

Modernization Tool provides checkboxes for these options, so manual bitmask editing is normally only needed for standalone WowPresence installations.

### Available fields

Each field has its own value:

| Value | Field |
| ---: | --- |
| 1 | Character Name |
| 2 | Guild |
| 4 | Faction |
| 8 | Class |
| 16 | Level |
| 32 | Zone |
| 64 | Race |

To display multiple fields, **add their values together** and put the result in `discord_broadcast_flags`.

### Examples

| Display | Value |
| --- | ---: |
| Nothing | 0 |
| Character Name only | 1 |
| Faction + Class | 12 |
| Race only | 64 |
| Race + Faction + Class | 76 |
| Character Name + Level + Zone | 49 |
| All character details | 127 |

Example — to display **Race + Faction + Class**:

```text
Race     = 64
Faction  = 4
Class    = 8

64 + 4 + 8 = 76
```

Then set:

```text
76
```

inside `discord_broadcast_flags`.

The default configuration uses `127`, which enables all supported character details.

WowPresence reads this setting while the game is running, so changes should normally appear on Discord automatically within a few seconds.

If the file is missing or contains an invalid value, WowPresence falls back to all supported fields.

## 🛡️ Administrator privileges

Discord and WoW should run with matching privilege levels.

If Discord runs as administrator, WoW must also run as administrator for local Rich Presence IPC to work reliably.

Running both normally is recommended unless elevation is required by the local setup.

## 🛠️ Building

WowPresence targets **32-bit x86 Windows**, matching WoW 1.12.1.

With an x86 MSVC developer environment:

```bat
cl /nologo /O2 /MT /W3 /LD src\WowPresence.c /Fe:WowPresence.dll /link /INCREMENTAL:NO
cl /nologo /O2 /MT /W3 src\WowPresenceLauncher.c user32.lib /Fe:WowPresence.exe /link /SUBSYSTEM:WINDOWS /INCREMENTAL:NO
```

GitHub Actions builds:

- `WowPresence.dll`
- `WowPresence.exe`
- `WowPresence.zip`

The ZIP includes the ready-to-edit `WowPresence` configuration folder.

Tags matching `v*` publish `WowPresence.zip` as the GitHub Release asset.

## 📜 Project identity

WowPresence is an **independent community project**.

Compatibility with **World of Warcraft**, **Discord**, **OctoWoW**, **VanillaFixes**, or other referenced projects does not imply affiliation, endorsement, sponsorship or ownership by their respective rights holders or maintainers.

**World of Warcraft**, **Warcraft**, **Blizzard Entertainment**, **Discord**, and related names and marks remain the property of their respective rights holders.

## 🙏 Credits

WowPresence is maintained by **Dusk-92**.
