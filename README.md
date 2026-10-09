# Ping Monitor with Discord Notifications

A Python utility that monitors your network ping in real time and has a Discord bot alert you when latency exceeds a configurable threshold.

<p align="center">
  <i>Made this out of boredom from high ping, which made me rage in competitive games.</i>
</p>

<p align="center">
  Total time spent on this project:
</p>
<p align="center">
  <a href="https://wakatime.com/badge/github/Kexe-Dev/ping-monitor-x-discord"><img src="https://wakatime.com/badge/github/Kexe-Dev/ping-monitor-x-discord.svg?style=for-the-badge" alt="wakatime"></a>
</p>


## 🌟 Features

- **Real-time ping monitoring** of a configurable host (default: `google.com`)
- **Discord alerts** as a rich embed in a channel of your choice when ping stays above the threshold
- **Live bot status** that switches to Do Not Disturb while your ping is high and back to Online when it recovers
- **Configurable** host, check interval and threshold
- **Error handling** – failed pings and failed messages are logged instead of crashing the monitor
- **Simple setup and startup** on Windows with `setup.bat` and `start.bat`

## 📋 Requirements

- Python 3.11+ (recommended)
- A Discord bot token, with the bot added to your server and allowed to view and send messages in the alert channel
- Internet connection

## 🚀 Installation

1. Download the [**latest release**](https://github.com/Kexe-Dev/ping-monitor-x-discord/releases/latest) zip (named after the version, e.g. `v1.4.0`)
   - Unzip it into your desired directory

2. Install dependencies:
   - Open the `ping-monitor-x-discord` folder
   - Double-click `setup.bat`

   Not on Windows? Run `pip install -r requirements.txt` instead.

## 💻 Usage

- Double-click `start.bat` (or run `python sc.py`)
   - On the first run, a `.env_vars` file is created and the program exits. Open it with a text editor, fill in `DISCORD_TOKEN`, `CHANNEL_ID` and optionally `USER_NAME`, then start it again.

> [!TIP]
> To copy a channel ID, enable **Developer Mode** in Discord (User Settings → Advanced), then right-click the channel → **Copy Channel ID**.

## ⚙️ Configuration

Edit these variables in `.env_vars`:

```dotenv
DISCORD_TOKEN=xxx.yyy.zzz  # Your bot token
CHANNEL_ID=1234567890      # ID of the channel that receives alerts
USER_NAME=xxxxxx           # Your username, shown in the bot status (optional, without the @)
HOST_TO_PING=google.com    # The host to monitor
PING_INTERVAL=5            # Check interval in seconds
PING_THRESHOLD=120         # Alert threshold in milliseconds (ms)
```

> [!WARNING]
> Never share or commit `.env_vars` – it contains your bot token. It is already listed in `.gitignore`.

## 📊 How It Works

1. The bot logs in to Discord and sets its status to *Watching ping for @USER_NAME*
2. Every `PING_INTERVAL` seconds, the [`ping3`](https://github.com/kyan001/ping3) library measures latency to `HOST_TO_PING`
3. If ping stays above `PING_THRESHOLD` for at least 5 seconds, the bot posts a **⚠️ High Ping Alert** embed (current ping, threshold, time) to `CHANNEL_ID` and switches its status to Do Not Disturb – *Watching @USER_NAME experience high ping*
4. Only one alert is sent per high-ping episode
5. Once ping stays below the threshold for at least 5 seconds, the status goes back to Online

## 📜 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Feel free to open [issues](https://github.com/Kexe-Dev/ping-monitor-x-discord/issues) or submit [pull requests](https://github.com/Kexe-Dev/ping-monitor-x-discord/pulls).

## 🙏 Acknowledgements

- [ping3](https://github.com/kyan001/ping3) for the ping implementation
- [discord.py](https://github.com/Rapptz/discord.py) for the Discord API wrapper

## 🔮 Future Goals

Planned features and improvements for upcoming releases:

- [x] More user friendly setup and startup
- [ ] Bot mentions Discord user in high ping alert message
- [ ] Docker container support
- [ ] Cross-platform compatibility (Linux, Windows)

Got an idea or feature request? Feel free to open an [issue](https://github.com/Kexe-Dev/ping-monitor-x-discord/issues/new/choose).

---

Made with ❤️ by [Kexe](https://github.com/Kexe-Dev) while waiting for better ping.
