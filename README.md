# 🐈 Nanobot: Local Android/Termux Installation Guide
**Install the ultra-lightweight AI Agent on your phone.**

Nanobot is a personal AI assistant inspired by OpenClaw. It delivers core agent functionality in just ~4,000 lines of code—99% smaller than alternatives, making it perfect for mobile devices.

---

## ⚡️ Quick Stats
* **Lightweight:** ~4,000 lines of code.
* **Powerful:** Supports local LLMs via Ollama.
* **Versatile:** Connects to Telegram and Web UIs.

---

## 🛠 Step-by-Step Installation

### 1. Prepare Termux Environment
Update packages and install the Ubuntu proot container.
```bash
pkg update && pkg upgrade -y
pkg install proot-distro
proot-distro install ubuntu
proot-distro login ubuntu
```

2. System Setup (Inside Ubuntu)
Ensure your Ubuntu environment is up to date and has the necessary tools.
```
apt update && apt upgrade -y
apt install python3 python3-pip git -y
```
3. Clone & Prepare Virtual Environment
Isolate the installation to prevent system conflicts.
```
git clone [https://github.com/HKUDS/nanobot.git](https://github.com/HKUDS/nanobot.git)
cd nanobot
apt update && apt install python3-venv -y
python3 -m venv ~/nano_env
source ~/nano_env/bin/activate
```
4. Install Nanobot
``` 
pip install nanobot-ai
nanobot onboard
```

🤖 Setup Telegram Integration
Get your Bot Token
Open Telegram and search for @BotFather.

Type /newbot and follow the prompts.

Choose a Name and Username for your bot.

Copy the API Token provided.

Configure Nanobot (Ollama + Telegram)
Paste the following command (replace YOUR_TELEGRAM_TOKEN_HERE with your actual token). This configures Nanobot to use your local Ollama instance with the Kimi 2.5 Cloud model.

``` 
cat <<EOF > ~/.nanobot/config.json
{
  "providers": {
    "openai": {
      "apiKey": "ollama",
      "apiBase": "http://localhost:11434/v1"
    }
  },
  "agents": {
    "defaults": {
      "model": "openai/kimi-k2.5:cloud"
    }
  },
  "channels": {
    "telegram": {
      "enabled": true,
      "token": "YOUR_TELEGRAM_TOKEN_HERE",
      "allowFrom": []
    }
  }
}
EOF
```
🚀 Running the Agent
Start the Gateway
```
nanobot gateway
```

💡 Pro Tip: Running in the Background
To keep your bot alive even after you close the Termux app, use nohup:

```
nohup nanobot agent > nanobot.log 2>&1 &
```

🌐 Web Interface (Chrome/OpenClaw-style)
If you prefer a visual chat interface in your browser instead of a terminal or Telegram:

Install & Run WebUI
```
pip install open-webui
open-webui serve
```

Access URL
Open Chrome on your Android device and visit:
```
http://localhost:8080
```
