# 📘 IndyScan Ledger Explorer Setup and UI Overview

## 📊 What IndyScan Shows in the UI

IndyScan is a visual explorer for Hyperledger Indy ledgers. It allows you to track and monitor:

* ✔️ Schema definitions
* ✔️ Credential definitions
* ✔️ DIDs and their roles (Trust Anchor, Endorser, etc.)
* ✔️ Transaction details (NYM, SCHEMA, CRED\_DEF, etc.)
* ✔️ Transaction types and timestamps
* ✔️ Node info and validator statuses
* ✔️ Latest block sequence and ledger synchronization status

The UI typically includes:

* 🔍 Search by DID or transaction
* 📄 List of recent ledger transactions
* 🏷️ Tabs or pages for schemas, cred defs, and DIDs
* ⏱️ Real-time updates (from daemon sync)
* 🧮 Status bar showing sync height and elapsed times

---

## ⚙️ Setting Up IndyScan Locally

Clone the repository:

```bash
git clone https://github.com/didx-xyz/indyscan.git
cd indyscan
```

Start using Docker Compose:

```bash
cd start
docker-compose up --build
```

Access the UI:

```
http://localhost:3000
```

Access the daemon API (used to sync ledger data):

```
http://localhost:3001
```

---

## 🛠️ Configuration Overview

Main configuration files:

* `start/app-configs-daemon/default.yml`: daemon config (poll intervals, logging, pool names)
* `start/app-configs-daemon/genesis/INDYSCANPOOL.txn`: genesis file of your target Indy ledger

Make sure the genesis file matches your target ledger (e.g., local VON network or BCovrin).

---

## 🔄 Connecting IndyScan to a Local Ledger

To connect IndyScan to your own local Indy Ledger, you need to replace the default genesis transaction file and reset the transaction index if needed.

### 📝 Step 1: Replace the Genesis File

Update the genesis transaction file with your local ledger's genesis content:

```bash
nano indyscan/start/app-configs-daemon/genesis/INDYSCANPOOL.txn
```

Paste the full content of your **local ledger's genesis file** here. Make sure the file is saved correctly and that the ports and IP addresses match your local nodes (e.g., use `127.0.0.1` or `internal.host.docker` if needed).

---

### 🔄 Step 2: Restart IndyScan

Rebuild and run IndyScan to apply the new genesis file:

```bash
cd indyscan/start
docker-compose down
docker-compose up --build
```

---

### ❌ Step 3: Clear Old Ledger Data (if new data is not shown)

If IndyScan still displays old or cached transaction data, clear the existing transaction index from Elasticsearch:

```bash
curl -X DELETE http://localhost:9200/txs-indyscanpool
```

Then stop and rebuild IndyScan again:

```bash
docker-compose down
docker-compose up --build
```

This will fetch and display transactions from your new local ledger.

---

### ✅ Verify

Once restarted:

* Open the IndyScan UI: [http://localhost:3000](http://localhost:3000)
* You should now see data from your local Indy network (schemas, DIDs, credential definitions, etc.)

---

### 🧠 Notes

* If your local ledger runs in Docker, make sure the `INDYSCANPOOL.txn` contains addresses accessible from within the IndyScan Docker container.
* You may also want to adjust polling intervals or startup delays in the daemon config if your ledger takes time to initialize.
