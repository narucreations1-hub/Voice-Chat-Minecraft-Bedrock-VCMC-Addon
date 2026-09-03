# VCMC Bedrock Addon 2.2

<div align="center">

<img src="https://antoic.com/icons/vcmc.png" width="110" alt="VCMC logo">

**Proximity voice chat for Minecraft Bedrock worlds and dedicated servers**

[Download VCMC](https://antoic.com/app.html) · [Documentation](https://antoic.com/docs/vcmc.html) · [Changelog](https://antoic.com/changelog/vcmc/) · [Discord](https://discord.gg/HA5gKcpsaq)

[![Version](https://img.shields.io/badge/VCMC-2.2-5865F2)](https://antoic.com/changelog/vcmc/)
[![Minecraft](https://img.shields.io/badge/Minecraft-Bedrock-62B47A)](https://www.minecraft.net/)
[![License](https://img.shields.io/badge/Price-Free-16865B)](https://antoic.com/app.html)

</div>

## What This Repository Contains

This is the official Bedrock Addon used by VCMC. The editable source is divided into:

| Pack | Use |
|---|---|
| `VCMC - WORLD` | A world hosted directly from Minecraft Bedrock |
| `VCMC - REALMS` | A Minecraft Realm connected through the VCMC app proxy |
| `VCMC - SERVER` | A dedicated Bedrock server, including Aternos or BDS |
| `VCMC - RP` | Shared icons, forms, translations, and interface resources |

Generated `.mcpack` and `.mcaddon` files are distributed through [GitHub Releases](../../releases/latest) and are intentionally excluded from source commits.

## Requirements

- Minecraft Bedrock with cheats enabled
- The VCMC app on every device that will send or receive voice
- The World or Server behavior pack
- The shared VCMC resource pack
- Internet access to the VCMC voice service

VCMC 2.2 is required for the new Realms flow and is recommended for all new features.

## Choose a Mode

### Local World

Use this mode when a player creates the world from Minecraft Bedrock.

1. Add `VCMC - WORLD` and `VCMC - RP` to the world.
2. The host enables WebSockets and disables **Encrypted WebSockets only** in Minecraft settings.
3. Everyone enters the host's room in the VCMC app.
4. The host copies the generated `/wsserver` command from VCMC and pastes it in Minecraft.
5. After the world is linked, every guest copies and pastes their own `/vcmc:verify "<code>"` command.

The host is the only player who installs the Addon and uses `/wsserver`. Each guest still verifies their own identity before joining the world's protected voice subroom.

### Dedicated Bedrock Server

Use this mode for BDS, Aternos, or another dedicated Bedrock server.

1. Upload `VCMC - SERVER` and `VCMC - RP`.
2. On non-Aternos servers, allow `@minecraft/server-net` in `config/default/permissions.json`.
3. Restart the server and join it from Minecraft.
4. Add the server in the VCMC app.
5. Copy `/vcmc:verify "<code>"` from the app and paste it in Minecraft.

The Addon creates and restores its protected room automatically. Players do not need an IP, room ID, or room token.

### Minecraft Realms

1. Install `VCMC - WORLD`, `VCMC - REALMS`, and `VCMC - RP` in the world before uploading it to Realms.
2. Open the Realms section in VCMC and sign in with the Minecraft account that can join the Realm.
3. Start the local proxy shown by the app and join through the LAN entry it creates.
4. Paste the verification command shown by VCMC when requested.

The proxy runs on the user's device; the Realm itself does not need to expose WebSockets.

## VCMC 2.2 Features

- Distance and spatial voice data
- Secure World subrooms
- Individual player verification
- Bidirectional app and Minecraft settings
- Master and per-player volume
- Self mute and administrative mute
- Public, private, and administrative groups
- Group passwords with an administrator warning before bypass
- Megaphone routing
- Built-in and custom voice effects
- Environmental effects for water, lava, caves, and dimensions
- Custom-dimension support
- Connection, mute, speaking, and megaphone indicators
- Legacy compatibility for older VCMC clients
- Minecraft Realms support
- Localized starter command books, including Korean
- `/vcmc:book` for recovering the user or administrator guide

## Player Commands

The visible commands are shared by Addon World, Addon Server, and the Java plugin.

| Command | Description |
|---|---|
| `/vcmc:verify "<code>"` | Link the Minecraft player with the personal code shown by VCMC |
| `/vcmc:menu` | Open voice settings, groups, and per-player volume |
| `/vcmc:m [true\|false]` | Toggle or set your own mute state |
| `/vcmc:groups` | Open the groups menu |
| `/vcmc:groups create <name> [password]` | Create a voice group |
| `/vcmc:groups join <group_or_name> [password]` | Join a voice group |
| `/vcmc:groups leave` | Leave the current group |
| `/vcmc:groups list` | List available groups |
| `/vcmc:groups delete [group_or_name]` | Delete a group you own |

## Administrator Commands

These commands require operator permissions.

| Command | Description |
|---|---|
| `/vcmc:admin` | Open the VCMC administration menu |
| `/vcmc:mute <player\|selector> <true\|false>` | Force or restore a player's microphone |
| `/vcmc:groups-settings <group> <global\|external\|environmental> <true\|false>` | Change group audio routing |
| `/vcmc:groups-admin create <group 1-255>` | Create an administrative group |
| `/vcmc:groups-admin move <group\|0> <player\|selector>` | Move players between groups |
| `/vcmc:groups-admin leave <player\|selector>` | Remove players from a group |
| `/vcmc:groups-admin list` | List administrative groups |
| `/vcmc:groups-admin delete <group>` | Delete an administrative group |
| `/vcmc:megaphone <player\|selector> <true\|false>` | Enable or disable megaphone |
| `/vcmc:sfx add <name> <json-string>` | Create a custom effect |
| `/vcmc:sfx delete <name>` | Delete a custom effect |
| `/vcmc:sfx list` | List custom effects |
| `/vcmc:sfx-player set <player\|selector> <effect>` | Assign a built-in effect |
| `/vcmc:sfx-player set <player\|selector> custom <name>` | Assign a custom effect |
| `/vcmc:sfx-player clear <player\|selector>` | Clear a player's effect |

### Custom SFX on Bedrock

Bedrock receives JSON as a string. Wrap the full object in quotes and escape every internal quote:

```text
/vcmc:sfx add grave "{\"base\":\"normal\",\"pitch\":-4,\"gain\":2,\"lowpass\":4200,\"highpass\":80,\"q\":0.8,\"distortion\":1.5,\"dry\":1}"
```

The Java plugin accepts the JSON object directly; only Bedrock requires this escaped format.

## Removed Commands

`/vcmc:join`, `/vcmc:room`, and `/vcmc:reconnect` are no longer public commands. VCMC now identifies, restores, and reconnects rooms automatically.

World bridge and synchronization commands are internal. Players and administrators should not execute them manually.

## Source Layout

```text
source/
├── VCMC - RP/
├── VCMC - REALMS/
├── VCMC - SERVER/
└── VCMC - WORLD/
```

## Downloads

### VCMC App

- [Android — Google Play](https://play.google.com/store/apps/details?id=com.naru.vcmc)
- [iOS — App Store](https://apps.apple.com/mx/app/vcmc-voice-chat-for-mc/id6784284005)
- [Windows — Microsoft Store](https://apps.microsoft.com/detail/9N74NFWF305Q)
- [Windows — GitHub Releases](https://github.com/NARUxd/Voice-Chat-Minecraft-PC-VCMC/releases)
- [Web app for macOS and Linux](https://antoic.com/play/vcmc/)

### Other Minecraft Components

- [Java/Geyser plugin](https://github.com/narucreations1-hub/Voice-Chat-Minecraft-Geyser-Plugin)
- [Plugin on CurseForge](https://www.curseforge.com/minecraft/bukkit-plugins/vcmc-voice-chat-for-mc-pluggin)

## Help

- [Official VCMC documentation](https://antoic.com/docs/vcmc.html)
- [VCMC changelog](https://antoic.com/changelog/vcmc/)
- [Discord support](https://discord.gg/HA5gKcpsaq)
- [Repository issues](../../issues)

VCMC is a free, independent project created by Naru. It is not affiliated with Mojang Studios. Minecraft is a trademark of Mojang AB.
