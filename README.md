# Unstopify

Unstopify is a macOS application that monitors Spotify playback and automatically restarts Spotify when non-track or non-episode content (such as ads) is detected.

## Features

- Automatically restarts Spotify when ads or non-music content plays
- Relaunches Spotify if it quits while Unstopify is running
- Restores playback and returns focus to your previous app after restart
- Does NOT interfere with normal pause/play when you control it manually
- Lightweight and runs entirely locally

## Installation

1. Download the latest release
2. Drag `Unstopify.app` into your Applications folder
3. Open the app and grant necessary permissions when prompted:
   - **Automation**: Allow Unstopify to control Spotify
   - **Terminal**: Allow Terminal to control Spotify (if using the stop shortcut)
   - **Accessibility** (if prompted)

## Setting Up the Stop Shortcut

Since Unstopify runs continuously, you'll need a keyboard shortcut to stop it:

1. Open **Shortcuts** app (search in Spotlight)
2. Click **"+"** to create a new shortcut
3. Add action: **"Run Shell Script"**
4. Paste this code:
```bash
touch ~/.unstopify_stop
sleep 2
killall Unstopify 2>/dev/null
rm -f ~/.unstopify_lock
osascript -e 'display notification "Unstopify stopped" with title "Unstopify"'
```
5. Name it **"Stop Unstopify"**
6. Right-click the shortcut → **Add Keyboard Shortcut**
7. Set your preferred key combination (e.g., `Ctrl+Shift+Q`)

## Usage

**To start:** Double-click Unstopify.app

**To stop:** Press your configured keyboard shortcut

**To force quit:** Open Activity Monitor, find Unstopify, and click the X button

**To check activity:** View the log file in Terminal:
```bash
tail -f ~/.unstopify.log
```

**Note:** Cmd+Q might not work to quit Unstopify, so use the keyboard shortcut "Stop Unstopify" instead.

## How It Works

Unstopify checks Spotify's current track every 3 seconds. When it detects non-track content (ads, promotions, etc.) or if Spotify quits unexpectedly, it automatically restarts Spotify and resumes playback in the background without interrupting your workflow.

## Building from Source

1. Open the AppleScript in Script Editor
2. **File → Export**
3. File Format: **Application**
4. ✅ Check **"Stay open after run handler"**
5. Save as Unstopify.app

## Disclaimer

This project does not modify Spotify, inject code, or block content. It only monitors playback state and restarts the application when unexpected content is detected.

**Important:** If Unstopify is running and Spotify quits or an ad plays, Spotify will automatically relaunch and resume playback. Quit Unstopify first if you want to fully close Spotify.
