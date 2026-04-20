# ⏰ PicoScheduler — Offline GPIO Task Scheduler for Raspberry Pi Pico W

![Platform](https://img.shields.io/badge/Platform-Raspberry%20Pi%20Pico%20W-c51a4a?logo=raspberrypi&logoColor=white)
![Language](https://img.shields.io/badge/Language-MicroPython-2b5b84?logo=python&logoColor=white)
![Interface](https://img.shields.io/badge/Interface-Browser%20%2F%20Access%20Point-brightgreen)
![Connectivity](https://img.shields.io/badge/Connectivity-Fully%20Offline-lightgrey)
![License](https://img.shields.io/badge/License-MIT-green)
![Stars](https://img.shields.io/github/stars/Afif718/PicoScheduler?style=social)

> **Schedule and control GPIO devices from your browser — fully offline, no router, no internet, no cloud.**

---

## 🔍 Why PicoScheduler?

Most IoT schedulers assume you have Wi-Fi, a router, or cloud access. **PicoScheduler assumes none of that.**

The Pico W acts as its own Access Point. You connect directly to it from any browser, schedule tasks, control devices, and walk away — it runs indefinitely offline with all data persisted across reboots. Perfect for **remote locations, agricultural setups, labs, and smart home projects** where network infrastructure is unavailable or unwanted.

---

## ✨ Features

- 📴 **Fully offline operation** — no internet, no router, no cloud dependency
- 🌐 **Browser-based UI** — Pico W hosts its own Wi-Fi Access Point for direct control
- 💾 **Persistent storage** — tasks, devices, and RTC time survive power loss via JSON files
- 🔌 **GPIO device control** — LEDs, relays, pumps, motors, and any GPIO-compatible device
- 🔒 **One task per device** — enforced constraint prevents overlapping or conflicting schedules
- 🗓️ **Flexible scheduling** — one-time or daily recurring tasks, created and deleted from the UI
- ➕ **Dynamic device creation** — add new devices by name and GPIO pin, no code changes needed
- 🕒 **Browser time sync** — receives local time from your browser on connect, no NTP needed
- ⏱️ **Internal time tracking** — maintains accurate time offline using MicroPython's `utime.ticks_ms()`

---

## 🕒 Time Management — How It Works

The Raspberry Pi Pico W has **no hardware RTC**. PicoScheduler solves this with a smart hybrid approach:

```
[You open the browser interface]
         │
         ▼
[Browser sends current local time to Pico W]
         │
         ▼
[Pico sets internal clock + saves to time.json]
         │
         ▼
[Pico tracks time offline using utime.ticks_ms()]
         │
         ▼
[On next boot → restores last known time from time.json]
```

> ⚡ After the initial browser sync, the Pico W tracks time entirely on its own — no NTP, no RTC module, no internet needed.

**Power loss behavior:** Time resets to `00:00` until you reconnect to the interface, at which point it restores from `time.json` and continues tracking offline.

---

## 📁 Project Structure

```
PicoScheduler/
│
├── main.py          # Web server, task scheduler, and GPIO control logic
├── devices.json     # Auto-generated — persistent device configurations
├── tasks.json       # Auto-generated — persistent scheduled tasks
├── time.json        # Auto-generated — RTC persistence across reboots
├── README.md
└── LICENSE
```

> The three JSON files are created automatically on first run — you only need to upload `main.py`.

---

## 🛠️ Hardware Requirements

| Component | Details |
|---|---|
| Microcontroller | Raspberry Pi Pico W |
| Devices | Any GPIO-compatible device (LED, relay, pump, motor) |
| Power | USB or external 5V supply |
| Client | Any device with a browser (phone, laptop, tablet) |

### Wiring Example

```
Pico W
│
├── GPIO 15 → LED / Relay signal pin
└── GND     → GND
```

---

## 🚀 Getting Started

### 1. Flash MicroPython Firmware

Download the latest [MicroPython firmware for Pico W](https://micropython.org/download/RPI_PICO_W/) and flash it using **BOOTSEL mode**.

### 2. Upload the Project

Upload `main.py` to your Pico W using [Thonny IDE](https://thonny.org/) or any MicroPython-compatible tool. The JSON files will be auto-generated on first boot.

### 3. Connect & Control

| Step | Action |
|---|---|
| Power on | Connect Pico W to power |
| Join Wi-Fi | Connect to `PicoW_Scheduler` / Password: `12345678` |
| Open browser | Navigate to `http://192.168.4.1` |
| Time sync | Browser automatically sends your local time to Pico |
| Done | System is fully operational — offline |

---

## 🖥️ Web Interface Overview

Once connected, the browser UI gives you full control:

**🕒 Time Display**
Shows the synchronized local time pushed from your browser.

**📋 Task Management**
- Create one-time or daily recurring schedules
- One task per device — overlapping schedules are blocked
- Delete tasks at any time

**🔌 Device Management**
- Add devices by name and GPIO pin number
- Toggle relays and LEDs directly
- Remove devices you no longer need

**💾 Data Persistence**
All changes are written to JSON immediately — device configs and tasks are safe even on sudden power loss.

---

## ⚙️ Example Automation Workflow

```
1. Add device → "Irrigation Pump" on GPIO 15
2. Create task → Turn ON at 06:00, Turn OFF at 06:30 (daily)
3. Disconnect from the Access Point
4. System runs indefinitely, offline, on schedule
```

---

## 🌍 Use Cases

- 🏠 **Home automation** — lighting, fans, ventilation, relay control
- 🌾 **Agricultural automation** — irrigation timers, grow room scheduling
- 🧪 **Laboratory equipment** — timed control of instruments and test rigs
- 📦 **Offline IoT projects** — automation without any network infrastructure
- 🎓 **Education & student projects** — hands-on embedded systems learning
- ⚡ **Timed relay systems** — anywhere a schedule + switch is needed

---

## 🔮 Future Development Roadmap

- [ ] Hardware RTC module support (DS3231) for power-loss time recovery
- [ ] Weekly and monthly scheduling options
- [ ] Sensor integration with conditional/trigger-based automation
- [ ] Task execution logging and history view
- [ ] Enhanced UI design with mobile-first layout
- [ ] Backup and restore utilities for JSON data

---

## 🤝 Contributing

Contributions are welcome! Open an [issue](https://github.com/Afif718/PicoScheduler/issues) or submit a pull request for bug fixes, features, or improvements.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙏 Acknowledgments

- [MicroPython](https://micropython.org/) — the runtime powering PicoScheduler
- [Raspberry Pi Foundation](https://www.raspberrypi.org/) — for the Pico W hardware

---

## 👤 Author

**M. H. A. Afif** — [@Afif718](https://github.com/Afif718)

> *Automation that works wherever you are — no cloud, no router, no compromise.* ⏰
