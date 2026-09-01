# WowPresence v1.2

## Changes

- Reworked zone detection to use the player's real AreaTable ID.
- Zone names are now resolved from `AreaTable.dbc` instead of selecting the first plausible string from several client addresses.
- Prevents internal map/area tokens such as `H32D` and `HLVA` from being published as Discord zone names.
- Uses the client's active localized AreaTable name when available, with a safe populated-locale fallback.
- Keeps WowPresence fully standalone; ClassicAPI is not required.
- Modernization Tool installations continue to use `.modernization_tool\WowPresence\` automatically.

## Included

- `WowPresence.dll`
- `WowPresence.exe`
- `WowPresence.zip` ready-to-install standalone package
