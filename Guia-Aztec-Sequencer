# Guia-Aztec.-Sequencer

> Full step-by-step guide to run an Aztec Sequencer node (Alpha Testnet) on Ubuntu (WSL-compatible), including real errors and fixes.

## Table of Contents

1. Install Dependencies
2. Install Aztec Tools
3. Update Aztec
4. Enable WSL Integration (if using WSL)
5. Run the Node
6. Common Errors and Fixes
7. IP Configuration and Firewall

---

## 1. Install Dependencies

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```

### Install Docker (run each section one by one)
```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

```bash
echo   "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu   "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```bash
sudo apt update -y && sudo apt upgrade -y
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```bash
sudo docker run hello-world
sudo systemctl enable docker
sudo systemctl restart docker
```

---

## 2. Install Aztec Tools

```bash
bash -i <(curl -s https://install.aztec.network)
```

Restart your terminal and verify installation:
```bash
aztec
```

---

## 3. Update Aztec

```bash
aztec-up alpha-testnet
```

### ❗ If you get an error like `Command not found`:
Check that you restarted the terminal after installing Aztec Tools.

---

## 4. Enable WSL Integration (WSL users only)

If Docker cannot access your Ubuntu environment (e.g., `error during connect: WSL integration`), do this:

1. Open Docker Desktop
2. Go to **Settings > Resources > WSL Integration**
3. Enable integration for **Ubuntu**

---

## 5. Run the Node

### Open screen
```bash
screen -S aztec
```

### Run Node
```bash
aztec start --node --archiver --sequencer   --network alpha-testnet   --l1-rpc-urls https://rpc.builder0x69.io/v2/your_api_key   --l1-consensus-host-urls https://rpc.builder0x69.io/v2/your_api_key   --sequencer.validatorPrivateKey 0xyourprivatekey   --sequencer.coinbase 0xyouraddress   --p2p.p2pIp your.ip.address
```

To detach screen: `CTRL + A`, then `D`  
To return: `screen -r aztec`

---

## 6. Common Errors and Fixes

### ❌ Error: `Genesis archive root mismatch`
**Fix:** Make sure you ran `aztec-up alpha-testnet`.

---

### ❌ Docker port 8080 already in use
**Fix:** Stop the container or choose a different port.

```bash
docker ps -a
docker stop CONTAINER_ID
```

---

### ❌ NoBlobBodiesFoundError
**Fix:** Wait for network sync or try restarting the node.

---

## 7. Find IP & Enable Firewall

### Find your public IP:
```bash
curl ipv4.icanhazip.com
```

### Enable UFW firewall and open required ports:
```bash
sudo ufw allow 22
sudo ufw allow ssh
sudo ufw allow 40400
sudo ufw allow 8080
sudo ufw enable
```

---

## ✅ Finished!

You should now have your Aztec Sequencer running.  
Check logs with `docker ps` or use `screen` to interact with the session.

---
