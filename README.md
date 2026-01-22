# Unstopify

Unstopify is a macOS application that monitors Spotify playback and automatically restarts Spotify when non-track or non-episode content (such as ads) is detected.

## Features

- Automatically restarts Spotify when ads or non-music content plays
- Restores playback and returns focus to your previous app after restart
- Automatically quits when you manually quit Spotify
- Does NOT interfere with normal pause/play when you control it manually
- Lightweight and runs entirely locally

## Installation

1. Download the latest release
2. Drag `Unstopify.app` into your Applications folder
3. Open the app and grant necessary permissions when prompted:
   - **Automation**: Allow Unstopify to control Spotify
   - **Accessibility** (if prompted)

## Setting Up the Stop Shortcut

To manually stop Unstopify without quitting Spotify, create a keyboard shortcut:

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
- Click **"Start"** to launch Spotify and begin monitoring
- Click **"Cancel"** to quit without launching Spotify
- Wait 10 seconds (no click) to auto-start with Spotify

**To stop:** 
- Quit Spotify normally (Cmd+Q on Spotify) - Unstopify will automatically quit too
- Or use your configured keyboard shortcut to stop Unstopify without quitting Spotify

**To force quit:** Open Activity Monitor, find Unstopify, and click the X button

**To check activity:** View the log file in Terminal:
```bash
tail -f ~/.unstopify.log
```

**Note:** Cmd+Q on Unstopify might not work on macOS Sequoia beta. Use the keyboard shortcut "Stop Unstopify" instead.

## How It Works

Unstopify checks Spotify's current track every 3 seconds. When it detects non-track content (ads, promotions, etc.), it automatically restarts Spotify and resumes playback in the background without interrupting your workflow.

When you manually quit Spotify (more than 10 seconds after an ad), Unstopify detects this and automatically quits too.

## Building from Source

1. Open the AppleScript in Script Editor
2. **File → Export**
3. File Format: **Application**
4. ✅ Check **"Stay open after run handler"**
5. Save as Unstopify.app

## Disclaimer

This project does not modify Spotify, inject code, or block content. It only monitors playback state and restarts the application when unexpected content is detected.

**Important:** When Unstopify detects ads or non-music content, it will automatically restart Spotify and resume playback. If you want to quit Spotify, simply quit it normally and Unstopify will stop automatically.
