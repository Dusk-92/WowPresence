# WowPresence v1.0

First standalone release of WowPresence.

## Included

- WowPresence.dll
- WowPresence.exe
- WowPresence.zip ready-to-install package

## Highlights

- Native Discord Rich Presence for WoW 1.12.1 build 5875 compatible clients
- Character name, guild, level, class, race, faction and zone display
- Stable elapsed-session timer across character changes
- Read-only game-memory sampling
- Separate native Discord IPC companion
- Configurable Discord Application ID through `WowPresence\discord_application_id`
- Privacy flags through `WowPresence\discord_broadcast_flags`
- Standalone `WowPresence\` runtime folder
- Automatic companion startup and exact WoW process tracking

## Installation

Extract `WowPresence.zip` into the WoW folder, edit `WowPresence\discord_application_id`, add `WowPresence.dll` to VanillaFixes `dlls.txt`, then launch WoW normally.
