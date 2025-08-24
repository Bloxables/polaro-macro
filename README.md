Polaro Macro
Version: 1.0
Created by Bloxables

License: Source-available. Personal use and local modification allowed. Redistribution prohibited. See LICENSE.txt.

Overview
--------
Polaro Macro is a Windows-only helper that watches the Roblox client window,
detects items on screen via image matching, and automatically clicks the Bag,
selects a Pokéball, and uses it. It also offers a simple UI to choose which
items to hunt for and which ball to throw.

Main Features
-------------
• Item finder:
  - Scans a small “target” region of the Roblox window for item icons.
  - Uses color/shape checks to reduce false positives.
  - Supports multiple environment variants per item (grass / water / dirt / snow).

• Auto-capture flow:
  - Clicks the Bag, selects your chosen ball, then clicks Use.
  - Falls back to “Run” when the environment UI is visible but no target is found.

• Configurable:
  - Adjustable polling rate (ms) and per-action thresholds.
  - Choose items to hunt from the Find tab or via presets.
  - Choose the ball to use from the Use tab.

• Overlay HUD:
  - Shows current status, poll rate, chosen ball, and a short list of enabled items.

• Global hotkeys (works even when the window is not focused):
  - F6 = Pause / Resume
  - F7 = Exit application

Requirements
------------
• Windows 10/11 (uses Win32 APIs).
• Roblox desktop client installed and running.

Installation
------------
1) Run the EXE or launch the script with Python.
2) On first run, the app seeds its data folder from a local “assets” folder located
   next to the EXE / script (if present).

Data & Folders
--------------
All runtime data lives under:
  %APPDATA%\Polaro Macro\

Key subfolders (inside %APPDATA%\Polaro Macro\assets):
  nobg\                → Item icons for the Find tab (single, no background).
  grassbg\, waterbg\, dirtbg\, snowbg\
                       → Environment-specific templates for item detection.
                          File naming: <ItemName>_grass.png, _water.png, etc.
  other\               → UI templates such as bag.png, use.png, run.png, and
                          optional environment tiles (Grass.png, Dirt.png, ...).
  pokeballsnobg\       → Ball thumbnails shown in the Use tab.
  pokeballs\           → Ball images used for in-game matching when selecting a ball.

IMPORTANT: Ball filenames (the base name, e.g. "Ultra Ball.png") should match
between pokeballsnobg and pokeballs. The UI selection is remembered by name.

Typical folder tree:
  assets\
    nobg\                   (item icons for the Find tab)
    grassbg\                (Item_grass.png)
    waterbg\
    dirtbg\
    snowbg\
    other\                  (bag.png, use.png, run.png, Grass.png, Dirt.png, ...)
    pokeballsnobg\          (UI thumbnails of balls)
    pokeballs\              (in-game ball templates)

Settings File
-------------
File: %APPDATA%\Polaro Macro\settings.ini  (auto-created)

Key options (defaults in parentheses):
  poll_ms (150)                 → How often to grab/screen-match (ms).
  target_threshold (0.15)       → Minimum match strength for items.
  color_threshold (0.65)        → Color histogram similarity for items.
  env_threshold (0.90)          → Environment match strength.
  ball_threshold (0.35)         → Ball match strength inside the Bag.
  use_threshold (0.20)          → “Use” button threshold.
  bag_threshold (0.15)          → Bag icon threshold.
  run_threshold (0.45)          → Run button threshold.

  target_region ("0.60,0.47,0.63,0.53")
  hud_region    ("0.60,0.88,0.99,0.99")
  ball_region   ("0.20,0.16,0.28,0.785")
  use_region    ("0.35,0.785,0.44,0.825")
    → Regions are percentages of the Roblox client area: L,T,R,B in [0..1].

  enabled_targets               → Pipe-separated list of enabled item names.
  targets_order                 → Optional ordering hint for item names.

Presets
-------
Three preset slots exist in settings.ini:
  preset_1 / preset_1_name
  preset_2 / preset_2_name
  preset_3 / preset_3_name
Click “Presets” to apply one quickly.

Usage
-----
1) Start Roblox and get into an encounter area and enable ;hunt (works best with the Legendary filter option).
2) Launch Polaro Macro.
3) In the Find tab, enable the items you care about (or choose a preset).
4) In the Use tab, pick a Pokéball (optional; if none, the macro chooses pokeball as the default).
5) Click Start.
6) Watch the overlay for status updates. Use F6 to pause/resume as needed.
7) Click Stop to halt the bot; F7 exits the app.

Custom Items
------------
• Put a single, no-background icon (PNG) into assets\nobg\ as <ItemName>.png.
• Provide one or more environment templates:
    assets\grassbg\<ItemName>_grass.png
    assets\waterbg\<ItemName>_water.png
    assets\dirtbg\<ItemName>_dirt.png
    assets\snowbg\<ItemName>_snow.png
The macro uses those templates to detect the item in the target region.

Limitations
-----------
• Windows only.
• Designed for the standard Roblox UI; major UI or icon changes can break matching.
• Matching scales ~0.7x–1.3x; extreme scaling or aspect/layout changes may fail.
• Requires the Roblox window to be visible (not minimized).
• If multiple Roblox windows exist, the first visible one is used.
• False positives can happen; tune thresholds or improve your template images.

Troubleshooting
---------------
• “Roblox not found” → Make sure a visible Roblox client window is open.
• It clicks in the wrong place → Verify regions in settings.ini and that DPI scaling
  is standard; the app turns on DPI awareness but OS-level scaling or overlays can
  still interfere.
• It doesn’t stop immediately → Use the Stop button or F7. If you modified code,
  ensure long sleeps use a stop-aware wait.

Safety & Notes
--------------
• This tool simulates mouse movement and clicks. Use it responsibly and at your own risk.
• Respect the game’s Terms of Service.
• Endriu has confirmed to allow macros, you will NOT be banned for using this.
    If you are, consult a mod in the official discord: https://discord.gg/polaro

Uninstall / Reset
-----------------
• Close the app.
• Delete %APPDATA%\Polaro Macro\ to remove assets and settings.
• (Optional) Delete the EXE / script folder.

Credits (Python modules)
-------
• OpenCV (template matching), mss (fast screen capture), tkinter (UI).
