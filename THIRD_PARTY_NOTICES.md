# Third-Party Notices

WowPresence contains original project code maintained by Dusk-92 and uses compatibility knowledge related to World of Warcraft 1.12.1 and Discord local Rich Presence IPC.

## IchaLaunch

The development of WowPresence was inspired in part by the character-status / Discord Rich Presence implementation in:

- Project: IchaLaunch
- Author / maintainer: brutaliccus
- Repository: https://github.com/brutaliccus/IchaLaunch

IchaLaunch was used as a technical reference during development, particularly for understanding a working WoW 1.12.1 character-status sampling approach.

The current WowPresence implementation is maintained separately and has been independently reworked. No IchaLaunch binary is included in this repository.

At the historical IchaLaunch revision reviewed during development, no explicit LICENSE, LICENSE.md, or COPYING file was present. This notice therefore records provenance and credit; it should not be interpreted as granting rights on behalf of the IchaLaunch author.

## World of Warcraft client compatibility data

WowPresence uses client-layout information and memory offsets associated with World of Warcraft 1.12.1 build 5875. Such compatibility information has been documented in multiple community projects over the years.

These values and client structures are used solely to locate read-only character status information in a compatible running client.

## Discord

WowPresence communicates with the locally running Discord desktop client through Discord's local IPC / Rich Presence protocol.

Discord is a trademark of Discord Inc. WowPresence is not affiliated with or endorsed by Discord Inc.

## Blizzard Entertainment / World of Warcraft

World of Warcraft, Warcraft, Blizzard, and related names and marks are trademarks or registered trademarks of Blizzard Entertainment, Inc.

WowPresence is an independent community project and is not affiliated with or endorsed by Blizzard Entertainment.
