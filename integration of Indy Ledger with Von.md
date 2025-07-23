
# 🧠 VON Network UI Setup with Indy Ledger

This guide explains how to set up the **VON Network UI**—a web interface for viewing, querying, and registering DIDs on an **Indy Ledger**. The UI can run in **read-only** mode for ledger inspection or in **registration mode** to publish DIDs using a seed.

---

## ✅ Prerequisites

Ensure the following are installed:

- Python 3.8 or above
- Git
- `build-essential`, `python3-dev`
- Running Indy Ledger with access to `pool_transactions_genesis` file

---

## 📥 Step 1: Clone the VON Network Repository

```bash
git clone https://github.com/bcgov/von-network.git
cd von-network
````

---

## ⚙️ Step 2: Set Up Python Environment

```bash
cd server
python3 -m venv venv
source venv/bin/activate
```

---

## 📦 Step 3: Install Dependencies

```bash
pip install -r requirements.txt
pip install wheel
sudo apt-get install build-essential python3-dev
pip install --upgrade pip setuptools
pip install 'aiohttp>=3.9.0'
pip install -r requirements.txt
```

---

## 🌐 Step 4: Serve Genesis File (Optional HTTP Server)

If your Indy ledger stores the genesis file locally, you can expose it over HTTP:

```bash
cp /var/lib/indy/sandbox/pool_transactions_genesis /var/lib/indy/sandbox/genesis.txt
python3 -m http.server 8090 --directory /var/lib/indy/sandbox/
```

Then your genesis URL will be:

```
http://localhost:8090/genesis.txt
```

---

## 🚀 Step 5: Run the VON UI Server

### 🔹 Option 1: Run in Read-Only Mode

```bash
export PORT=9000
export GENESIS_URL=http://<your-ip>:8090/pool_transactions_genesis.txt
python3 -m server.server
```

### 🔹 Option 2: Run with Inline Environment Variables

```bash
GENESIS_URL=http://localhost:8090/pool_transactions_genesis.txt \
PORT=9000 \
python3 -m server.server
```

---

## ✍️ Step 6: Run in DID Registration Mode (Write Enabled)

To enable DID registration on the ledger, run:

```bash
LEDGER_SEED=000000000000000000000000Trustee1 \
REGISTER_NEW_DIDS=True \
GENESIS_URL=http://localhost:8090/pool_transactions_genesis.txt \
python3 -m server.server
```

> 🔐 This uses the **`Trustee1`** seed to write to the ledger. Make sure it matches a DID that has **TRUSTEE** role on your Indy network.

---

## 🌍 Access the VON UI

Once the server starts, open your browser:

```
http://localhost:9000
```

You can:

* View existing DIDs, schemas, and credential definitions
* Register new DIDs (only in registration mode)

---

## 🧾 Final Notes

* The UI reads from your Indy ledger using the genesis file
* Make sure your ledger is running and reachable via `GENESIS_URL`
* Use registration mode only with authorized seeds
* You can reverse proxy the UI using Nginx for public access

---

## 📚 References

* [VON Network GitHub](https://github.com/bcgov/von-network)
* [Hyperledger Indy](https://github.com/hyperledger/indy-node)
* [VON UI on Docker](https://github.com/bcgov/von-network#docker-setup)

