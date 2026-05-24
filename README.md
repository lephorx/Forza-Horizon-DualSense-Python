<div align="center">
  <h1>🏎️ FH DualSense — Adaptive Triggers</h1>
  <p><strong>Real adaptive trigger feedback for Forza Horizon on PC.</strong></p>
  <p>Feel the brakes lock up. Feel the engine idle. Feel every gear shift.</p>
</div>

---

## What it does

Forza Horizon streams live car telemetry over UDP. This app reads it and writes adaptive trigger effects directly to your DualSense — alongside Steam, without fighting it.

- **Left trigger (brake)** — gets stiffer the harder you brake. Pulses like ABS when tires lock. Extra resistance on the handbrake.
- **Right trigger (throttle)** — soft progressive resistance. Thumps on every gear shift. Buzzes at the rev limiter. Rumbles on wheelspin.

Steam keeps full control of rumble motors and buttons. This app only touches the adaptive trigger bytes — they never conflict.

---

## Install

### Windows / Linux — launcher (recommended)

1. Download **`win_start.bat`** (Windows) or **`linux_start.sh`** (Linux) from the [latest release](../../releases/latest).
2. Drop it in any folder and double-click it.

The launcher downloads the app, sets up the environment, and checks for updates on every run. No Python install needed.

> **Linux:** install `libhidapi` first:
> ```bash
> sudo apt install libhidapi-hidraw0   # Debian / Ubuntu
> sudo pacman -S hidapi                # Arch
> sudo dnf install hidapi              # Fedora
> ```
> Then install the udev rule from `packaging/linux/70-dualsense.rules` and replug your controller.

### Windows — standalone exe

A single `FH-DualSense.exe` is also attached to each release. No install, no Python — just run it.

### macOS

```bash
bash mac_start.sh
```

Uses the native WKWebView glassmorphism UI.

### From source

```bash
git clone https://github.com/lephorx/Forza-Horizon-DualSense-Python
cd Forza-Horizon-DualSense-Python/src
uv sync
uv run main.py
```

---

## In-game setup

Open **Settings → HUD and Gameplay** in Forza Horizon:

| Setting | Value |
|---|---|
| Data Out | **ON** |
| Data Out IP Address | **127.0.0.1** |
| Data Out IP Port | **5300** |

> If telemetry isn't arriving, try `::1` (IPv6 loopback) instead of `127.0.0.1`.

**Moonlight / remote streaming:** enable Moonlight Mode in the app so it doesn't conflict with your streaming client's controller input.

---

## Steam haptics

Steam can still run the rumble motors at the same time. To enable them:

1. Right-click Forza Horizon in Steam → **Properties → Controller → Additional Settings** → turn DualSense vibration **ON**.
2. In-game: **Settings → Advanced Controls → Vibration → ON**.

---

## Auto-launch with Steam

To have the triggers activate automatically when you press Play:

**Steam → Forza Horizon → Properties → Launch Options:**
```
"C:\Windows\System32\cmd.exe" /c ""C:\Path\To\win_start.bat" %command%"
```

Start the launcher **before** Forza Horizon if you launch manually.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Controller not found | Check USB/BT connection. If using HidHide, allowlist `python.exe`. |
| No telemetry | Data Out is off in Forza, wrong IP/port, or Windows Firewall is blocking UDP 5300. |
| SmartScreen blocks the bat | Click **More info → Run anyway**. The script only downloads dependencies. |
| Triggers too strong | Lower Brake/Throttle Max Force or the Overall Intensity slider. |
| Triggers too weak | Raise Brake/Throttle Max Force or the Overall Intensity slider. |
| No gear shift thump | Car must be moving and shifting between valid gears. |
| Controller stops working in Moonlight | Enable **Moonlight Mode** in the app (System card). |

---

## License

AGPLv3 with additional attribution terms — see [LICENSE](LICENSE).

Originally created by **[Hamza Yeşilmen (HamzaYslmn)](https://github.com/HamzaYslmn/Forza-Horizon-DualSense-Python)** · [Sponsor](https://github.com/sponsors/HamzaYslmn)

This is a fork with a redesigned glassmorphism UI, macOS support, Moonlight streaming mode, and additional trigger tuning options.
