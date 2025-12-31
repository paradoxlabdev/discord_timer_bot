# Discord Timer Bot

![Node.js](https://img.shields.io/badge/Node.js-22_LTS-339933?logo=node.js&logoColor=white)
![Discord.js](https://img.shields.io/badge/Discord.js-14-5865F2?logo=discord&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue.svg)

Discord bot that provides channel timers with live updates, quick buttons, voice notifications, microphone history, and cleanup utilities.

![Screenshot](images/bot-screenshot.png)

## Features

- **Text & Slash Commands** — `!cs`, `!status`, `!stop`, `/timer`, `/set-default`, `/help`
- **Quick-action Buttons** — Start/pause/stop timers and common durations (2m/4m/5m/6m/40m)
- **Voice Notifications** — Warning + end sounds when bot is connected to voice channel
- **Microphone History** — Last 10 users who unmuted, with mute/unmute controls
- **Channel Cleanup** — Bot messages and command messages with confirmation
- **Auto-cleanup** — Prevents memory leaks (timers, intervals, histories)

## Tech Stack

- **Runtime:** Node.js 22 LTS
- **Framework:** discord.js 14
- **Voice:** @discordjs/voice 0.19.0
- **Process Manager:** PM2 (optional)

## Requirements

- Node.js 22 LTS (`@discordjs/voice@0.19.0` requires >= 22.12). Works on 20, but upgrade to avoid voice issues.
- npm 10+ (bundled with Node)

## Setup

1. **Install dependencies:**

```bash
npm install
```

2. **Create `.env` in project root:**

```env
DISCORD_TOKEN=your_bot_token
CLIENT_ID=your_application_client_id

# optional:
GUILD_ID=your_guild_id            # for guild-only command registration fallback
DEFAULT_TIMER_DURATION=300000     # ms, default 5m
ENABLE_VOICE_NOTIFICATIONS=true
ENABLE_MICROPHONE_HISTORY=true
ENABLE_AUTO_CLEANUP=true
DEBUG_MODE=false
VERBOSE_LOGGING=false
```

3. **Sound files** (already provided):
   - `sounds/cri.mp3` — warning sound
   - `sounds/end.mp3` — final sound

## Running

```bash
# Start
npm start

# Dev (nodemon)
npm run dev
```

On startup, config validation runs and slash commands attempt global registration (with guild fallback).

## Commands

### Text Commands

| Command | Description |
|---------|-------------|
| `!cs [time]` | Start/reset timer (e.g., `5m`, `30s`, `1h`; no arg = default) |
| `!stop` | Stop timer (reports remaining time) |
| `!status` | Show timer status |
| `!set cs [time]` | Set default timer for guild |
| `!start` | Show help |
| `!join` / `!connect` | Connect bot to your voice channel |
| `!leave` / `!disconnect` | Disconnect bot from voice |
| `!test1` / `!test2` | Play warning/final sound |
| `!miclog` | Show microphone unmute history |
| `!clearvoicehistory` | Clear mic history |
| `!cleanup` | Clean voice connections |

### Slash Commands

| Command | Description |
|---------|-------------|
| `/timer [duration]` | Start timer |
| `/set-default <duration>` | Set default duration |
| `/help` | Show help |
| `/voice-connect` | Connect to voice |
| `/voice-disconnect` | Disconnect from voice |
| `/sound-test typ: warning\|end` | Test sounds |
| `/mic-history` | Show mic history |
| `/clear-mic-history` | Clear mic history |
| `/clear-channel` | Clean channel messages |

### Interactive Buttons

Start/Pause/Stop timer, connect/disconnect voice, microphone history, clear history, clear channel, quick durations (2m/4m/5m/6m/40m), manual time info, help.

## Discord Setup

### Required Intents

Enable in Discord Developer Portal:
- Guilds
- GuildMessages
- MessageContent
- GuildVoiceStates
- GuildMembers

### Required Permissions

- Connect (voice)
- Speak (voice)
- Manage Messages (for cleanup)

## Smoke Test

1. **Run on Node 22:**
```bash
nvm use 22
npm install
npm start
```

2. **In Discord:**
   - Slash: `/timer 2m`, `/sound-test typ: warning`, `/sound-test typ: end`, `/help`
   - Buttons: Start timer, Pause/Stop, Connect/Disconnect voice, Quick timers

3. **Verify:** Warning and end sounds play in voice; check timer updates and cleanup buttons.

## Notes

- **Rate limits:** Per-user and global safeguards applied
- **Cleanup:** Periodic cleanup for timers, intervals, histories, orphaned messages
- **Voice:** Bot must have voice permissions; sounds play only when connected to voice channel

## License

MIT

## Author

**paradoxlab.dev**
