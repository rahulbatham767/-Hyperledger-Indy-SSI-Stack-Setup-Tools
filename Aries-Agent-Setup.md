

# 🚀 Hyperledger Aries Cloud Agent (ACA-Py) Setup Guide

This guide provides a step-by-step process to install and run the **Aries Cloud Agent - Python (ACA-Py)** with **Python 3.12**, virtual environment setup, required system dependencies, and basic agent startup commands.

---

## ✅ Prerequisites

Ensure the following tools and packages are installed on your system:

- Python 3.12 or later
- Pip (Python package manager)
- Docker and Docker Compose (optional for containerized flows)
- Required system packages and libraries for native modules

---

## ⚙️ Setup Steps

### 1. Clone the ACA-Py Repository

```bash
git clone https://github.com/openwallet-foundation/acapy
````

### 2. Navigate to the ACA-Py Directory

```bash
cd acapy
```

---

## 🐍 Python 3.12 Setup

### 3. Add Python 3.12 via deadsnakes PPA

```bash
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository -y ppa:deadsnakes/ppa
sudo apt update
```

### 4. Install Python 3.12 and Required System Libraries

```bash
sudo apt install -y python3.12 python3.12-venv python3.12-dev build-essential \
  libffi-dev libssl-dev libxml2-dev libxslt1-dev zlib1g-dev \
  libpq-dev libsqlite3-dev rustc cargo
```

---

## 🧪 Python Virtual Environment Setup

### 5. Create a Virtual Environment

```bash
python3.12 -m venv venv
```

### 6. Activate the Virtual Environment

```bash
source venv/bin/activate
```

### 7. Upgrade Core Python Tools

```bash
pip install --upgrade pip setuptools wheel
```

---

## 📦 Install ACA-Py and Dependencies

### 8. Install ACA-Py (Preferred Method)

```bash
pip install .
```

> 💡 **If this fails**, install dependencies manually:

```bash
pip install \
  aries-cloudagent \
  aries-askar \
  indy-vdr \
  indy-credx \
  anoncreds \
  python3_indy \
  pyparsing
```

---

## 🚀 Run ACA-Py Agent (No Ledger Mode)

```bash
aca-py start \
  --inbound-transport http 0.0.0.0 8000 \
  --outbound-transport http \
  --no-ledger \
  --admin 0.0.0.0 8001 \
  --admin-insecure-mode \
  --wallet-type askar \
  --wallet-name my_wallet \
  --wallet-key my_wallet_key
```

> ⚠️ This starts the agent in **no-ledger** mode. For production, configure `--genesis-url` and `--ledger-url`.

---

## 🧾 Final Notes

* Always run `source venv/bin/activate` before running ACA-Py.
* Add `--debug` to the `aca-py start` command for verbose output.
* Ensure Rust (`rustc`) and Cargo are properly installed, as `aries-credx` and `askar` depend on them.
* For automation, you can use a setup script (`setup-acapy.sh`).

---

## 📁 Optional: Shell Script for Automated Setup

Save the following as `setup-acapy.sh` to automate the entire process:

```bash
#!/bin/bash

set -e

echo "📁 Entering ACA-Py directory..."
cd acapy || { echo "❌ 'acapy' directory not found. Exiting."; exit 1; }

echo "➕ Adding Python 3.12 repository..."
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository -y ppa:deadsnakes/ppa
sudo apt update

echo "🐍 Installing Python 3.12 and development tools..."
sudo apt install -y python3.12 python3.12-venv python3.12-dev build-essential \
    libffi-dev libssl-dev libxml2-dev libxslt1-dev zlib1g-dev libpq-dev libsqlite3-dev rustc cargo

echo "🧪 Creating Python 3.12 virtual environment..."
python3.12 -m venv venv
source venv/bin/activate

echo "⬆️ Upgrading pip, setuptools, and wheel..."
pip install --upgrade pip setuptools wheel

echo "📦 Installing ACA-Py from current directory..."
if ! pip install .; then
  echo "⚠️ Direct install failed. Installing dependencies manually..."

  pip install \
    aries-cloudagent \
    aries-askar \
    indy-vdr \
    indy-credx \
    anoncreds

  pip install python3_indy
  pip install pyparsing

  echo "✅ Installed ACA-Py dependencies manually."
else
  echo "✅ ACA-Py installed successfully from local source."
fi

echo "🏁 Setup complete. Activate your venv and run ACA-Py agent as needed."
```

Make it executable:

```bash
chmod +x setup-acapy.sh
```

---

## 📚 References

* [ACA-Py GitHub Repository](https://github.com/openwallet-foundation/acapy)
* [Aries Framework Overview](https://hyperledger.github.io/aries/)
* [Aries RFCs](https://github.com/hyperledger/aries-rfcs)
* [Indy SDK & Indy VDR](https://github.com/hyperledger/indy-sdk)
* [Aries Askar](https://github.com/hyperledger/aries-askar)

