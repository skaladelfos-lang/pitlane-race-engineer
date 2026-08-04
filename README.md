# PITLANE.GR / Race Engineer

**Live race telemetry for Le Mans Ultimate — shared with your whole team, from anywhere.**

![Status](https://img.shields.io/badge/status-beta-yellow) ![Version](https://img.shields.io/badge/version-v1.2-7a9e1e) ![Platform](https://img.shields.io/badge/platform-Windows-blue)

> **Beta v1.2** — this is an early release. Some fields (see [Known Limitations](#known-limitations) below) aren't available yet due to what Le Mans Ultimate itself exposes. Bug reports and feedback welcome.

---

## What is this?

Race Engineer turns Le Mans Ultimate's live session data into a real-time dashboard your whole team can watch together — whether you're the one driving, or a teammate resting between stints in a completely different country.

Built for endurance racing: your team's car keeps the same number all race, drivers rotate in and out of the seat, and everyone — driving or not — can watch the same live dashboard the whole time.

### Features

- **Live car data**: position, lap, gaps ahead/behind, fuel/energy, pit stops, penalties
- **Tyre temperatures** (all four corners) and wear, color-coded — flashes red when a tyre hits 0%
- **Damage detection**, including lost wheels and bodywork damage
- **Self-tracing track map** — learns the circuit from your own driven path (no manual track data needed), with everyone's car positions shown live
- **Sector flags** (S1/S2/S3) with a flashing indicator, so you know exactly which part of the circuit is affected
- **Weather forecast** — conditions and rain chance across the session, not just right now
- **Estimated pit stop time**, pulled directly from the game
- **Stint Strategy integration** — plan your race in the companion [Stint Strategy calculator](https://raceapp.pitlane.gr/lmu-stint-strategy.html), then push it straight to your dashboard: next pit lap, fuel to add, and a full visual race timeline, tracked automatically as pit stops actually happen
- **Live fuel projection** — laps remaining on your current fuel and pit stops still needed, recalculated in real time as the race unfolds, independent of your pre-race plan
- **Shared team rooms** — no accounts needed, just a private code your team creates and shares
- Works from any device with a browser — phone, laptop, tablet, anywhere with internet

---

## How it works

Two small pieces work together:

1. **The agent** — a small background app that runs on whichever PC is actively driving. It reads Le Mans Ultimate's local data and sends it out. Runs quietly in your system tray — no console window taking up space on your screen.
2. **The dashboard** — a web page anyone on the team can open, showing the same live data. No installation needed for anyone who's just watching.

Only the driving PC needs anything installed. Everyone else just needs a link.

---

## Installation

### Requirements

- Windows 10/11
- [Python 3.9+](https://www.python.org/downloads/) (only needed on the PC that will actually run the agent — during install, tick **"Add Python to PATH"**). Python will be installed automatically.
- Le Mans Ultimate, with **Settings → Gameplay → Enable Plugins** turned ON

### Steps

1. Download `RaceEngineer-Setup.zip` and extract it anywhere (Desktop, Downloads — doesn't matter).
2. Double-click **`install.bat`** inside the extracted folder.
3. This copies everything to `C:\PitlaneRaceEngineer`, installs the required Python packages, and creates a **"Race Engineer"** shortcut on your Desktop.
4. You can delete the extracted zip folder now — everything it needs lives in `C:\PitlaneRaceEngineer` from here on.

This install step only needs to happen once per PC. Every driver who might race from their own PC should run through this once.

---

## Setup — Creating and Joining a Room

Race Engineer uses **rooms** to keep your team's data private. Anyone with the room code can watch; nobody else can.

### Creating a room (do this once per race/event)

One person on the team visits:

```
https://raceapp.pitlane.gr/create
```
<img width="1753" height="774" alt="image" src="https://github.com/user-attachments/assets/b11ce41a-e031-4d23-beae-dd1282920ea1" />

This generates a random, private room code (e.g. `K7M2QX`) along with a ready-to-share viewer link. Share the code with your team via Discord, WhatsApp, or however you normally coordinate.

### Running the agent (whoever is currently driving)

1. Make sure Le Mans Ultimate is running.
2. Double-click the **"Race Engineer"** shortcut on your Desktop.
3. It checks for updates automatically, then starts quietly in the background — you'll see a **circle icon appear in your system tray** (bottom-right of your screen, near the clock; click the `^` arrow if it's hidden).
   - 🟢 **Green** = running and connected
   - 🔴 **Red** = stopped, or something's not right
4. **Right-click the tray icon** for a few options:
   - **Open Dashboard** — opens the local control page, where you enter your room code and tyre count for the race
   - **Restart Agent** — if something looks stuck
   - **Show Console (Troubleshooting)** — reopens the old-style visible window if you need to see exactly what's happening (useful when reporting a bug)
   - **Exit** — closes everything cleanly
5. Once you enter your room code on the local control page, your team's shared dashboard opens automatically in your browser.

If you're already running the agent and accidentally launch it again, it'll detect that and just let you know instead of starting a duplicate.

### Watching (everyone else)

No installation needed. Just open the room link shared by whoever created it:

```
https://raceapp.pitlane.gr/?room=YOUR_ROOM_CODE
```

Works from any browser, any device, any location.

---

## Stint Strategy Planning

The companion [Stint Strategy calculator](https://raceapp.pitlane.gr/lmu-stint-strategy.html) helps you plan fuel/energy consumption and pit windows before or during a race.

Open it from the **"Stint Strategy"** link on your dashboard (this keeps your room code, so it knows which race to link to), fill in your numbers, and hit **Calculate Strategy**. Once you have a plan, hit **Push Plan to Race Engineer** — it'll appear on your dashboard as a full race timeline, with the next pit lap and fuel-to-add shown live, automatically advancing each time you actually complete a pit stop.

Your inputs and results are remembered per-room, so navigating back and forth between the two pages never loses your work — but a new room always starts fresh.

---

## During a Race

- The dashboard needs the agent running and connected the whole time — if the tray icon goes red, live updates pause for everyone watching until it's green again.
- When a driver's stint ends and someone else takes over, the new driver runs the agent on their own PC with the same room code — the dashboard keeps working for everyone watching, without them needing to do anything. Car identity stays locked to your team's actual car number throughout the handoff.
- Car number detection is automatic (no need to enter it manually) — this reliably locks onto your team's actual car within the practice/qualifying window before the race starts, and stays locked even through brief data gaps during a driver change.
- Works best with 1920×1080 full screen mode.

  <img width="1753" height="774" alt="image" src="https://github.com/user-attachments/assets/b78c53a4-293d-4c67-9473-9937bb1e9153" />

---

## Known Limitations

This is a beta release. A few things aren't available yet — not bugs, but genuine gaps in what Le Mans Ultimate's data currently exposes:

- **Penalty type** (Stop-Go vs Drive-Through) — only whether a penalty is active, not which kind. Check the in-game HUD for the specific type.
- Tyre temps, damage, and driver aids require the driving PC to actually be controlling the car — a pure spectator's data won't show these fields for the car they're watching.
- Weather forecast and estimated pit stop time are newly added and still being validated against real race data — if either looks off, please report it.

---

## Support

Found a bug or have a feature request? Open an issue on this repository.

If Race Engineer has been useful to you, [consider supporting the project](https://raceapp.pitlane.gr/donate.html) — it's free to use and always will be, covered out of pocket, but donations help keep it that way.

---

© 2026 PITLANE/1821REVO — Spiro Kaladelfos. All rights reserved.
