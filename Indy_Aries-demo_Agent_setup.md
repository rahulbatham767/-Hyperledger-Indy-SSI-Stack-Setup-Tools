

# 🔧 Indy-Aries Agent Setup for College Demo (Using VON Network Genesis)

This guide helps you spin up three Aries Cloud Agent Python (ACA-Py) agents for a college-based SSI demo:

* 🧑‍🏫 **CDAC** – Issuer (Organization)
* 👨‍🎓 **Virat** – Holder (Student Wallet)
* 👩‍💼 **iSocial** – Verifier (Company/Organization)

Each agent connects to a **VON Network Genesis file**, enabling decentralized credential issuance and verification.

---

## 🛠️ Step 0: Clone and Prepare Aries Cloud Agent Python (ACA-Py)

First, clone the ACA-Py repository and navigate to the scripts directory:

```bash
git clone https://github.com/hyperledger/aries-cloudagent-python.git acapy
cd acapy/scripts
chmod +x run_docker
```

> The `run_docker` script helps you quickly start ACA-Py agents inside Docker containers with pre-configured commands.

---

## 📝 Replace the Following Values:

* `10.210.13.22` → Your **VON Network Host IP** (VM/Docker host)
* `172.17.0.1` or `172.18.0.1` → Your **Localhost IP** for Docker bridge interface

---

## 👨‍🎓 Agent 1: Student Wallet (**virat**)

```bash
PORTS="8000 8001" ./run_docker start \
-l virat \
-it http 0.0.0.0 8000 \
-ot http \
--admin 0.0.0.0 8001 \
--admin-insecure-mode \
--genesis-url http://10.210.13.22:9000/genesis \
-e http://172.23.77.31:8000 \
--wallet-type askar \
--wallet-name virat_wallet \
--wallet-key virat_wallet \
--debug-webhook \
--monitor-ping \
--log-level info \
--auto-provision \
--trace-target log \
--auto-ping-connection \
--seed virat000000000000000000000000000 \
--auto-accept-invites \
--auto-accept-requests \
--auto-respond-credential-proposal \
--auto-respond-credential-offer \
--auto-respond-credential-request \
--auto-store-credential \
--requests-through-public-did \
--public-invites \
--emit-new-didcomm-prefix \
--auto-respond-presentation-proposal \
--auto-store-credential \
&
```

---

## 🧪 Agent 2: Verifier Agent (**iSocial**)

```bash
PORTS="8030 8031" ./run_docker start \
-l iSocial \
-it http 0.0.0.0 8030 \
-ot http \
--admin 0.0.0.0 8031 \
--admin-insecure-mode \
-e http://172.23.77.31:8030 \
--genesis-url http://10.210.13.22:9000/genesis \
--wallet-type askar \
--wallet-name isocial_wallet \
--wallet-key isocial_wallet \
--log-level info \
--auto-provision \
--auto-ping-connection \
--seed isocial0000000000000000000000000 \
--auto-accept-invites \
--auto-respond-credential-proposal \
--auto-respond-credential-offer \
--auto-respond-credential-request \
--auto-store-credential \
--auto-accept-requests \
--requests-through-public-did \
--public-invites \
--emit-new-didcomm-prefix \
--auto-respond-presentation-proposal \
--auto-respond-presentation-request \
&
```

---

## 🏫 Agent 3: Issuer Agent (**CDAC**)

```bash
PORTS="8020 8021" ./run_docker start \
-l CDAC \
-it http 0.0.0.0 8020 \
-ot http \
--admin 0.0.0.0 8021 \
--admin-insecure-mode \
-e http://172.23.77.31:8020 \
--genesis-url http://10.210.13.22:9000/genesis \
--wallet-type askar \
--wallet-name cdac_wallet \
--wallet-key cdac_wallet \
--log-level info \
--auto-provision \
--auto-ping-connection \
--emit-new-didcomm-prefix \
--seed cdac0000000000000000000000000000 \
--auto-accept-invites \
--auto-accept-requests \
--auto-respond-credential-proposal \
--auto-respond-credential-offer \
--auto-respond-credential-request \
--auto-store-credential \
--requests-through-public-did \
--public-invites \
&
```

---

## ✅ You're All Set!

All three agents are now running and connected to the **VON Network**.

### Use their respective **Admin APIs** to:

* 🏗️ Create schemas and credential definitions
* 🪪 Issue credentials from CDAC to Virat
* 🧾 Request proof from Virat using iSocial
* 🔐 Explore SSI workflows with full control

---

### 📘 Resources

* [Aries Cloud Agent Python (ACA-Py)](https://github.com/hyperledger/aries-cloudagent-python)
* [VON Network Info](https://vonx.io/)
* [Aries RFCs](https://github.com/hyperledger/aries-rfcs)

---

# Created by Rahul Batham


If you want, I can help with further steps, like how to interact with the agents’ admin APIs or how to issue your first credential!
