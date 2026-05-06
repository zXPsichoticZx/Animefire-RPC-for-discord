

# 🔥 AnimeFire Discord RPC

Automatic Rich Presence for Discord while watching anime on AnimeFire.io.

Shows: anime title, episode, real-time progress bar, play/pause icon, and quick access buttons.

---

## 📦 Structure

```
animefire-rpc/
├── extension/          ← Chrome extension
│   ├── manifest.json
│   ├── content.js      ← Captures player data
│   ├── background.js   ← Sends to Python server
│   ├── popup.html/js   ← Extension interface
│   └── icons/          ← Add icons here (16, 48, 128px)
└── python/
    └── rpc.py          ← Local server + Discord RPC
```

---

## ⚙️ Installation

### 1. Get the Client ID

1. Go to [discord.com/developers/applications](https://discord.com/developers/applications)
2. Create a new application (e.g., "AnimeFire")
3. Copy the **Application ID** from the *General Information* tab
4. In **Rich Presence → Art Assets**, upload the images:

   * `logo_xeon` — large icon
   * `play_icon` — play icon
   * `pause_icon` — pause icon

### 2. Configure the Python script

Open `python/rpc.py` and edit the line:

```python
CLIENT_ID = "SEU_CLIENT_ID_AQUI"  # Paste your Application ID here
```

### 3. Install Python dependencies

```bash
pip install pypresence flask flask-cors
```

### 4. Run the server

```bash
python python/rpc.py
```

Keep this terminal open while watching.

### 5. Install the Chrome extension

1. Open `chrome://extensions/`
2. Enable **Developer mode** (top right corner)
3. Click **Load unpacked**
4. Select the `extension/` folder

### 6. Add icons (optional but recommended)

Place 3 PNG files in the `extension/icons/` folder:

* `icon16.png` (16×16)
* `icon48.png` (48×48)
* `icon128.png` (128×128)

If you don’t have them, you can remove the `icons` references from `manifest.json`.

---

## 🚀 How to use

1. Run `python rpc.py` in the terminal
2. Open Chrome with the extension installed
3. Access any episode on AnimeFire.io
4. The RPC updates automatically on Discord!

The extension icon shows:

* 🟢 Green = connected to Python server
* 🔴 Red = Python server is not running

---

## ❓ Common issues

**"Discord not found"**
→ Open Discord before running the script.

**Red icon in the extension**
→ The Python server is not running. Run `python rpc.py`.

**Data not showing**
→ AnimeFire may have changed HTML selectors. Open DevTools (F12) on AnimeFire, inspect the player, and update selectors in `content.js`.

**Progress bar not showing**
→ Normal if the video is paused. The bar only appears while the video is playing (Discord RPC limitation).
