
# ⚙️ Hyperledger Indy Production Setup Guide

This guide walks you through setting up a **production-level Hyperledger Indy network** with:

- **4 Nodes**
- **5 Clients**
- **DID creation** for Aries Agent onboarding

Each step includes detailed explanations to help you understand its purpose and outcome.

---

## 📁 Setup Configuration

### ✅ 1. Install System-Wide Dependencies

```bash
sudo apt update
sudo apt install unzip python3-venv python3-pip -y
````

---

### ✅ 2. Create & Activate Virtual Environment

```bash
mkdir indy-setup && cd indy-setup
python3 -m venv venv-indy 
source venv-indy/bin/activate
```

---

### ✅ 3. Add the Indy Repository

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9692C00E657DDE61
sudo add-apt-repository "deb https://hyperledger.jfrog.io/artifactory/indy focal stable"
```

> 💡 **Explanation**: Adds the Hyperledger Indy repo to fetch latest versions of Indy and its components.

---

## 🔐 Install Plenum Dependencies

### ✅ 4. Download & Install Libraries

```bash
wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/libssl1.0.0_1.0.2n-1ubuntu5.13_amd64.deb
wget https://repo.sovrin.org/deb/pool/bionic/master/u/ursa/ursa_0.3.2-1_amd64.deb

sudo dpkg -i libssl1.0.0_1.0.2n-1ubuntu5.13_amd64.deb
sudo dpkg -i ursa_0.3.2-1_amd64.deb
```

> ⚠️ If you get errors like `dpkg: error processing package rocksdb`, fix them using:

```bash
sudo apt --fix-broken install
```

---

## 📦 Install Indy Plenum

### ✅ 5. Download and Install

```bash
mkdir indy-plenum && cd indy-plenum

wget https://github.com/hyperledger/indy-plenum/releases/download/v1.13.1/third-party-dependencies.zip
wget https://github.com/hyperledger/indy-plenum/releases/download/v1.13.1/plenum-deb.zip

sudo apt install unzip
unzip third-party-dependencies.zip -d third-party-dependencies
cd third-party-dependencies/artifacts/third-party-dependencies
sudo dpkg -i *.deb
cd ../../../

sudo unzip plenum-deb.zip -d plenum-deb
cd plenum-deb/artifacts/plenum-deb
sudo dpkg -i *.deb
cd ../../../..

# Move ursa files
sudo mv /usr/lib/ursa/* /usr/lib
sudo rm -rf /usr/lib/ursa
```

---

## 🌐 Install Indy Node

### ✅ 6. Download and Install Dependencies

```bash
mkdir indy-node && cd indy-node

wget https://github.com/hyperledger/indy-node/releases/download/v1.13.2/third-party-dependencies.zip
unzip third-party-dependencies.zip -d third-party-dependencies
cd third-party-dependencies/artifacts/third-party-dependencies
sudo dpkg -i *.deb
cd ../../../
```

---

### ✅ 7. Install Supervisor

```bash
sudo apt-get install supervisor
```

---

### ✅ 8. Install Indy Node

```bash
wget https://github.com/hyperledger/indy-node/releases/download/v1.13.2/indy_node-deb.zip
unzip indy_node-deb.zip -d indy_node
cd indy_node/artifacts/indy_node-deb
sudo dpkg -i *.deb
```

---

## 🖧 Create a 4-Node Network

### ✅ 9. Configure Network Name

```bash
sudo nano /etc/indy/indy_config.py
```

Add the following:

```python
NETWORK_NAME = 'sandbox'  # or any custom name
```

---

### ✅ 10. Generate Pool Transactions

```bash
sudo generate_indy_pool_transactions --nodes 4 --clients 5 --nodeNum 1 2 3 4
```

---

## 🧪 Install Indy CLI (for DID & Wallet Creation)

### ✅ 11. Download and Run Indy CLI

```bash
mkdir indy-cli && cd indy-cli

wget https://github.com/hyperledger/indy-cli-rs/releases/download/v0.1.0/indy-cli-rs-0.1.0-linux-x86_64.tar.gz
tar -xf indy-cli-rs-0.1.0-linux-x86_64.tar.gz
chmod +x indy-cli-rs
./indy-cli-rs
```

---

### ✅ 12. Create and Open a Wallet

```bash
wallet create trustee key=trustee
wallet open trustee key=trustee
```

---

### ✅ 13. Generate a DID

```bash
did new seed=000000000000000000000000Trustee1
wallet close
exit
```

> 🔐 **Explanation**: The `Trustee1` seed is used by default for bootstrapping the network.

---

## 🧾 (Optional) Modify Domain Genesis Pool File

To include a custom DID:

```bash
sudo nano /var/lib/indy/sandbox/domain_transactions_genesis
```

> ✍️ Add your DID and verkey manually for custom roles (e.g., Trust Anchor, Endorser).

---

## 🚀 Start the Nodes

Run each node in background (default ports start at 9701):

```bash
sudo start_indy_node Node1 0.0.0.0 9701 0.0.0.0 9702 &
sudo start_indy_node Node2 0.0.0.0 9703 0.0.0.0 9704 &
sudo start_indy_node Node3 0.0.0.0 9705 0.0.0.0 9706 &
sudo start_indy_node Node4 0.0.0.0 9707 0.0.0.0 9708 &
```

---
**Explanation**: These commands start the 4 Indy nodes in the background, allowing them to begin processing transactions and communicating with each other.

## 16.	Check Node Logs:
```bash 
cd /var/log/indy/sandbox
tail -f Node1.log
```
**Explanation**: Checking the log files helps you verify that the nodes are running correctly and identify any issues.



## ✅ Success!

You now have a **production-grade Hyperledger Indy network** running locally with:

* Fully functional 4-node validator pool
* Wallet and DID setup via CLI
* Genesis transactions in place


## 📘 Additional Resources

* [Hyperledger Indy Documentation](https://hyperledger-indy.readthedocs.io/)
* [Aries Framework Documentation](https://aries.vonx.io/docs/)
* [Troubleshooting Indy Nodes](https://github.com/hyperledger/indy-node/issues)



Happy Building with Hyperledger Indy! 🛠️✨

```

