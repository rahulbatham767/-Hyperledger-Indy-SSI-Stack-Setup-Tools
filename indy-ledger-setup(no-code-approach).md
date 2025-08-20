
## 🔧 Indy Ledger and Aries Agent Setup (No-Code Approach)

This guide will help you set up a local **Indy ledger** using `von-network` and register **three Aries agents**: `cdac`, `virat`, and `isocial`.

### 📦 Prerequisites

Ensure the following are installed on your Ubuntu/Debian-based system:

```bash
sudo apt update
sudo apt install -y docker.io docker-compose
sudo systemctl start docker
sudo systemctl enable docker
```

---

### 🚀 Step-by-Step Setup

---

### 1. Clone the `von-network` Repository

```bash
git clone https://github.com/bcgov/von-network.git
cd von-network
```

---

### 2. Build the `von-network` Docker Images

```bash
./manage build
```

---

### 3. Start the Local Indy Ledger

```bash
./manage start
```

The ledger will be available at:

* Genesis URL: `http://localhost:9000/genesis`
* Web UI (for viewing transactions): `http://localhost:9000`

---

### 4. Get the Internal Docker Host IP

This IP will be used by Aries agents to connect to the ledger inside Docker.

```bash
./manage dockerhost
```

📌 **Note the IP** — e.g., it might be `host.docker.internal` or something like `172.17.0.1`.

---

### 📝 Notes: Copy the Genesis URL for Aries Agents

When configuring Aries agents (such as ACA-Py), you need to provide the **ledger genesis transaction file URL** so the agents know how to connect and trust the ledger.

* The genesis URL is:

  ```
  http://localhost:9000/genesis
  ```

* If your Aries agent is running **inside Docker or a different host**, replace `localhost` with the internal Docker host IP you retrieved in Step 4. For example:

  ```
  http://<docker-host-ip>:9000/genesis
  ```

* Make sure this URL is **accessible from the agent’s environment**; otherwise, the agent won’t be able to fetch the genesis transactions and will fail to connect to the ledger.

---

### 5. Register Aries Agents (cdac, virat, isocial)

You can register agents using the **von-network Web UI** or with scripts.

#### Option A: Using the von-network UI (No-code)

1. Open `http://localhost:9000`
2. Under **"Create a new DID + NYM"** section:

   * Enter `cdac` as alias and click **Submit**
   * Repeat for `virat` and `isocial`

Each submission creates a new DID registered to the ledger.

---

### 🧪 Optional: View Ledger Transactions

Visit:
[http://localhost:9000](http://localhost:9000)
Use the web interface to view submitted transactions and DIDs.

---

### ✅ Done!

Your local Indy ledger is now running, and agents `cdac`, `virat`, and `isocial` are registered.

You can now configure **Aries agents** (like Aries Cloud Agent Python - ACA-Py) to connect using the ledger's genesis URL and the internal Docker host IP.
