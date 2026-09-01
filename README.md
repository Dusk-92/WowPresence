# WowPresence

Native Discord Rich Presence for **World of Warcraft 1.12.1 (build 5875)** and compatible clients.

WowPresence keeps the game-side component deliberately small: a read-only DLL samples character status from the WoW process and writes a local JSON snapshot, while a separate companion executable handles Discord IPC outside the game process.

## Features

- Character name and guild
- Level and class
- Race and faction
- Current zone
- Stable elapsed-session timer across character changes
- Automatic companion startup
- Exact WoW process tracking
- Read-only game-memory access
- No Discord bot, Client Secret, or network service required

## Compatibility

### Tested

- OctoWoW client based on WoW 1.12.1 / build 5875

### Expected compatibility

- World of Warcraft 1.12.1 build 5875
- Compatible private-server clients that preserve the same relevant client memory layout

### Not compatible

- WoW Classic Era 1.14.x
- The Burning Crusade Classic
- Wrath of the Lich King Classic
- Retail World of Warcraft

Other modified 1.12.1 clients should be considered **untested until verified**.

## Files

```text
WowPresence.dll
WowPresence.exe
```

The DLL is loaded into WoW by a compatible DLL loader such as VanillaFixes. After WoW is running, the DLL automatically starts `WowPresence.exe`.

The companion executable should normally **not** be launched manually.

## Installation

1. Download `WowPresence.dll` and `WowPresence.exe` from Releases.
2. Place both files in the WoW game directory.
3. Add this line to the VanillaFixes `dlls.txt` file:

```text
WowPresence.dll
```

4. Launch WoW normally through VanillaFixes.

WowPresence creates its runtime files under:

```text
<WoW folder>\.modernization_tool\WowPresence\
```

## Discord application

The current build includes the OctoWoW Discord Application ID as its default so it works immediately with the configuration it was originally developed and tested against.

Advanced users can override it by creating:

```text
.modernization_tool\WowPresence\discord_application_id
```

The file should contain only the numeric Discord Application ID.

No Client Secret is used or required.

## Privacy flags

The optional file:

```text
.modernization_tool\WowPresence\discord_broadcast_flags
```

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

If the file is missing, all supported fields are enabled.

## Administrator privileges

Discord and WoW should run with matching privilege levels.

If Discord is running as administrator, WoW must also run as administrator for local Discord Rich Presence IPC to work reliably.

Running both normally is recommended unless elevation is actually required by the local setup.

## Runtime design

```text
WoW
 └─ WowPresence.dll
      ├─ read-only character sampling
      ├─ local JSON status
      └─ starts WowPresence.exe
             └─ Discord local IPC
```

The DLL does not communicate directly with Discord. The companion executable does not read or write WoW memory.

Status data is written to:

```text
.modernization_tool\WowPresence\discord_wow_status.json
```

The companion log is written to:

```text
.modernization_tool\WowPresence\WowPresence.log
```

## Building

The native components target **32-bit x86 Windows**, matching WoW 1.12.1.

With an x86 MSVC developer environment:

```bat
cl /nologo /O2 /MT /W3 /LD src\WowPresence.c /Fe:WowPresence.dll /link /INCREMENTAL:NO
cl /nologo /O2 /MT /W3 src\WowPresenceLauncher.c user32.lib /Fe:WowPresence.exe /link /SUBSYSTEM:WINDOWS /INCREMENTAL:NO
```

GitHub Actions also builds both binaries automatically. Tagged versions matching `v*` publish a GitHub Release containing the DLL, EXE, and ZIP package.

## Credits and provenance

WowPresence is maintained by **Dusk-92**.

The project was inspired in part by the WoW character-status / Discord Rich Presence work in **IchaLaunch** by **brutaliccus**. The current implementation is maintained separately and does not include IchaLaunch binaries.

See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for additional provenance and trademark information.
