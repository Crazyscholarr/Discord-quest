# Orion Discord Quest Automator

**Orion** is a specialized automation script designed to help users complete Discord Quests automatically by interacting directly with Discord's internal systems. It handles various quest types by spoofing the required activity data.

## 🛠️ Core Functionality

The script operates by hooking into Discord's internal Webpack modules and manipulating the data stores that track user activity.

### 1. Quest Detection & Filtering
- The script scans your `QuestsStore` to identify all quests you have **enrolled** in but **not yet completed**.
- It filters for quests that are still active (not expired) and fall under supported task types.

### 2. Supported Task Modules
Orion implements specific logic for different Discord Quest requirements:

#### 📺 Watch Video (`WATCH_VIDEO`)
- Calculates the time difference between enrollment and the present.
- Periodically sends `video-progress` POST requests to the Discord API.
- Increments the `timestamp` until the target video duration is reached.

#### 🎮 Play on Desktop (`PLAY_ON_DESKTOP`)
- Fakes a running game process by injecting a "fake game" object into Discord's `RunningGameStore`.
- It mocks the executable path and PID (Process ID) to make Discord believe a specific game is currently running.
- Dispatches internal events to trigger the "Now Playing" status required for quest progress.

#### 📡 Stream on Desktop (`STREAM_ON_DESKTOP`)
- Mocks the `ApplicationStreamingStore` to simulate an active stream session.
- Allows you to "stream" any window or screen while the script reports the specific Quest Application ID to Discord's servers.

#### 🕹️ Play Activity (`PLAY_ACTIVITY`)
- Identifies an available Voice Channel or Private Channel.
- Sends periodic `heartbeat` requests to the API with a `stream_key` to simulate activity within a Discord Interaction/Activity.

---

## 🚀 How to Use

1. Open Discord (Desktop App or Chrome/Edge Browser).
2. Press `Ctrl + Shift + I` to open the **Developer Tools**.
3. Go to the **Console** tab.
4. Paste the code from `index.js` and hit **Enter**.
5. Monitor the console for progress logs.

## ⚠️ Important Notes
- **Desktop Requirement**: For "Play" and "Stream" quests, Discord usually requires the Desktop app. The script includes a check for this and will notify you if you are on a browser.
- **Voice Channels**: For streaming quests, you must be in a Voice Channel with at least one other participant.
- **Safety**: This script interacts with internal APIs. Use it responsibly and understand that automated interaction carries inherent risks regarding Terms of Service.
