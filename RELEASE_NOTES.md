# WowPresence v1.1

## Changes

- Added automatic support for Modernization Tool installations.
- Standalone installs continue to use `WowPresence\` in the WoW folder.
- When `.modernization_tool\WowPresence\` already exists, the same binaries automatically use that managed data directory instead.
- No separate Modernization Tool build of WowPresence is required.
- Existing `discord_application_id` and `discord_broadcast_flags` files remain user-managed.

## Included

- `WowPresence.dll`
- `WowPresence.exe`
- `WowPresence.zip` ready-to-install standalone package

## Standalone installation

Extract `WowPresence.zip` into the WoW folder, edit `WowPresence\discord_application_id`, add `WowPresence.dll` to VanillaFixes `dlls.txt`, then launch WoW normally.
