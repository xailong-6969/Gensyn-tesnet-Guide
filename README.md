# 🚀 RL-Swarm Setup Guide

Welcome to the **RL-Swarm** setup guide! This walkthrough helps you install and run the project from scratch, restore your key, activate the virtual environment, and expose your local service using tunnels.

---

## 🧭 Prerequisites

- ✅ `swarm.pem` key (backed up)
- ✅ Git, Python 3, `screen`, and `npm` installed
- ✅ GPU (3090, 4090, or ≥24GB VRAM recommended)
- ✅ CPU (arm64 or x86 CPU with minimum 32gb ram (note that if you run other applications during training it might crash training)

---

## ⚙️ Setup Steps

### 📁 1. Backup Your Key

Secure your existing `swarm.pem` key:
```bash
cp $HOME/rl-swarm/swarm.pem $HOME/
```

---

### 🧹 2. Clean & Clone Fresh Repo

Remove old project and clone fresh:
```bash
cd $HOME && \
rm -rf rl-swarm && \
git clone https://github.com/xailong-6969/rl-swarm.git
```

---

### 🔐 3. Restore `swarm.pem`

Place the key back into the new repo:
```bash
cp $HOME/swarm.pem $HOME/rl-swarm/
```

> 💡 **Tip:** Use your file explorer or `ls` to verify its placement.

---

### 🖥️ 4. Start a Screen Session

Start a persistent session:
```bash
cd $HOME/rl-swarm
screen -S gensyn
```

---

### ⚡ 5. Enable High-VRAM Optimization

For systems with ≥24GB VRAM (e.g. 3090/4090/A100/H100), enable high-performance mode:
```bash
sed -i 's/use_vllm: false/use_vllm: true/' rgym_exp/config/rg-swarm.yaml && \
sed -i 's/fp16: false/fp16: true/' rgym_exp/config/rg-swarm.yaml
```

---

### 🐍 6. Set Up Python Environment

Inside the screen session:
```bash
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```

Wait for the message:
```
Waiting for localhost:3000...
```

Now, **detach** the screen:
```bash
Ctrl + A, then D
```

---

## 🌐 Expose Localhost Port `3000`

Choose **one** of the methods below to make your service accessible online:

---

### 🚪 Option A: LocalTunnel

```bash
npm install -g localtunnel
lt --port 3000
```

---

### ☁️ Option B: Cloudflare Tunnel

```bash
sudo apt install cloudflared           # Ubuntu/Debian
# or
brew install cloudflared               # macOS

cloudflared tunnel --url http://localhost:3000
```

Open the URL in your browser to access your service.

---

## 🔄 Reconnect to Screen

To resume your running session:
```bash
screen -r gensyn
```

---

## ✅ You're Done!

Your **RL-Swarm** instance is now running, and you can interact with it either locally or via the exposed tunnel.
