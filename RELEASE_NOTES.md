# WowPresence v1.2

## Changes

- Reworked zone detection to use the player's real AreaTable ID.
- Zone names are now resolved from `AreaTable.dbc` instead of selecting the first plausible string from several client addresses.
- Prevents internal map/area tokens such as `H32D` and `HLVA` from being published as Discord zone names.
- Uses the client's active localized AreaTable name when available, with a safe populated-locale fallback.
- Keeps WowPresence fully standalone; ClassicAPI is not required.
- Modernization Tool installations continue to use `.modernization_tool\WowPresence\` automatically.
- Improved WoW process detection logging with a generic `WoW process detected.` message.
- Manual/debug process fallback now supports both `WoW_Modernized.exe` and `WoW.exe`.
- Documented the OctoWoW Discord Application ID for standalone configuration.

## Included

- `WowPresence.zip` — ready-to-install package containing `WowPresence.dll`, `WowPresence.exe`, and the WowPresence configuration folder.

## Commits

- [`f261c3b`](https://github.com/Dusk-92/WowPresence/commit/f261c3be298d56bc025671e22a348555157f94b3) Resolve zones through AreaTable
- [`0994fe4`](https://github.com/Dusk-92/WowPresence/commit/0994fe4e08b03ec17b09d09eb51a2e7c2b0b2db1) Document AreaTable zone resolution
- [`3c76de9`](https://github.com/Dusk-92/WowPresence/commit/3c76de9bdbcb19a45543bd09b03bbd75a2d65d8f) Document ClassicAPI technical reference
- [`8048e80`](https://github.com/Dusk-92/WowPresence/commit/8048e804f6629c75cc3b1d81f835aaa1c1f8a423) Prepare WowPresence v1.2 release
- [`4576605`](https://github.com/Dusk-92/WowPresence/commit/4576605dce59702d8f90d542e7db3dae4789e1ed) Document OctoWoW Discord Application ID
- [`fdb3126`](https://github.com/Dusk-92/WowPresence/commit/fdb3126d1fc6c09392c21d07327c21084aeeb112) Improve WoW process detection logging
- [`05dc409`](https://github.com/Dusk-92/WowPresence/commit/05dc4094a0f326699c72176ad516d3341e7be33f) Publish only the WowPresence ZIP release asset

**Full Changelog**: [v1.1...v1.2](https://github.com/Dusk-92/WowPresence/compare/v1.1...v1.2)
