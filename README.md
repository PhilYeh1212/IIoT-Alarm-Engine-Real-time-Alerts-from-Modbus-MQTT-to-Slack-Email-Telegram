# IIoT Alarm Engine

> Real-time alarm monitoring for Modbus and MQTT, with multi-channel notifications to Email, Webhook, Slack, Telegram, Desktop, and Log file. Replace $2,000+ commercial alarm servers with a $59 Python tool.
<img width="1280" height="720" alt="iiot_alarm_cover" src="https://github.com/user-attachments/assets/c04aa2a9-5062-43e6-9894-61487c503daf" />

**This is a commercial tool, sold on Gumroad.** Source code is included in your purchase.

---

## What it does

Watches industrial and IIoT data streams. When a value crosses a threshold for a configurable duration, fires alarms to whichever notification channels you configure.

```
┌──────────┐                                  ┌──────────┐
│  Modbus  │ ──┐                          ┌── │  Email   │
│  RTU/TCP │   │   ┌──────────────┐       │   └──────────┘
└──────────┘   │   │              │       │   ┌──────────┐
               ├──>│  IIoT Alarm  │ ──────┼── │  Slack   │
┌──────────┐   │   │    Engine    │       │   └──────────┘
│   MQTT   │ ──┘   │              │       │   ┌──────────┐
│  broker  │       └──────────────┘       └── │ Telegram │
└──────────┘                                  └──────────┘
                                              ...and more
```

## Features

- **Sources** — Modbus TCP + RTU, MQTT (with JSON auto-flatten)
- **Rule engine** — comparison operators (>, <, =, !=) with persistence duration
- **Six notification channels:**
  - **Email** (SMTP — Gmail, Outlook, custom servers)
  - **Webhook** (POST JSON to any URL)
  - **Slack** (incoming webhook)
  - **Telegram** (Bot API)
  - **Desktop notification** (native OS popup)
  - **Log file** (append-only audit trail)
- **SQLite alarm history** — every TRIGGERED + CLEARED event stored
- **Save/load configs** as JSON for deploying to multiple machines
- **Live monitor tab** — watch alarms fire in real time
- **Test channel button** — verify Email/Slack/Telegram before relying on them
- **Tkinter dark GUI** — same look-and-feel as the rest of the toolkit
- **Single-file Python** — 1200+ lines, no install hell

## Why this exists

Commercial alarm/notification servers (Win-911, AlarmDirector, FactoryTalk Alarms) cost $2,000-10,000+ per server. They require Windows, dedicated hardware, and weeks of configuration. Open-source alternatives like Apache Camel are powerful but require a Java team to maintain.

IIoT Alarm Engine is what I wished existed: small, focused, runs anywhere Python runs, sends notifications to the channels engineers actually check (Slack, Telegram, Email), and you can read every line of source.

## Real example rule

Monitor boiler temperature, alert ops team if it stays above 80°C for 30 seconds:

```
Source:    modbus:reg40001
Operator:  >
Threshold: 80.0
Duration:  30 seconds
Channels:  ops_email, slack_alerts, tg_oncall
```

That's it. No XML config files. No state machine to draw. No proprietary scripting language. Three notifications go out the moment the rule fires.

## Use cases

| Scenario | Why this tool fits |
|---|---|
| Small factory floor monitoring | Cheap, deployable in hours, not weeks |
| Edge IIoT alarm aggregation | Run on Raspberry Pi as gateway |
| Lab equipment monitoring | Watch test rigs without paying for SCADA |
| Home automation overflow | When Home Assistant isn't enough |
| Vendor demos | Quickly stand up alarms for customer presentations |
| OEM integration | Embed alarms in your own product, source included |

## What's NOT in v1.0 (planned for v2)

- Complex rule logic (AND/OR, time-window aggregation)
- Email digest mode (group multiple alarms into one email)
- HTTP API source (poll REST endpoints)
- OPC UA source (use [OPC UA Bridge Pro](https://philyeh.gumroad.com/l/opcua-bridge-pro) to bridge OPC UA → MQTT for now)
- Web dashboard

If any of these are blockers, contact me before buying — I prioritize features based on customer requests.

## Tested on

- Python 3.9, 3.10, 3.11, 3.12
- Windows 10/11, macOS 13+, Ubuntu 22.04
- pymodbus 3.5+, paho-mqtt 1.6+

## Get it

→ **[IIoT Alarm Engine on Gumroad — $59](https://philyeh.gumroad.com/l/iiot-alarm-engine)**

## What's in the purchase

- `iiot_alarm_engine.py` — Single-file Python application (1200+ lines)
- `requirements.txt` — Pinned dependencies
- `README.md` — Full setup + channel guides (5-min Telegram setup, etc.)
- `example_config.json` — Pre-made rules and channels to adapt
- Commercial use license per Gumroad EULA

## License

Commercial use license per Gumroad EULA. You may use this software at the company that purchased it for any commercial purpose. Redistribution, resale, or open-sourcing the code is not permitted.

## Support

- Reply to your Gumroad purchase email
- Bug reports / feature requests via GitHub Issues

---

I write about industrial Python and protocol internals at **[dev.to/philyeh](https://dev.to/philyeh)**, and post Chinese versions on [iThelp](https://ithelp.ithome.com.tw/users/20171204).

— Phil Yeh · Senior Automation Engineer · Industrial Python · Developer Tools
