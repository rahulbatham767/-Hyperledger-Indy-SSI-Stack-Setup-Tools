 
# 🧪 Indy-Aries Demo: College & Organization Identity Use Case

Welcome to the **Indy-Aries Demo**!
This project simulates a **real-world credential flow** involving three types of decentralized identity agents:

* 🏫 **CDAC** – *Issuer* (College)
* 👤 **Virat** – *Holder* (Student)
* 🏢 **iSocial** – *Verifier* (Organization)

Explore how Self-Sovereign Identity (SSI) works using Hyperledger Indy and Aries in this easy-to-run demo.

---

## 🛠️ Prerequisites

Before getting started, make sure the following components are set up and running:

* ✅ **Indy Ledger**
* ✅ **Aries Agents**

  * `CDAC` (Issuer)
  * `Virat` (Holder)
  * `iSocial` (Verifier)

> **Need help with setup?**
>
> * 📘 [No-Code Ledger & Agent Setup (MD)](https://github.com/rahulbatham767/-Hyperledger-Indy-SSI-Stack-Setup-Tools/blob/main/indy-ledger-setup%28no-code-approach%29.md)
> * 📘 [Agent Setup Instructions (MD)](https://github.com/rahulbatham767/-Hyperledger-Indy-SSI-Stack-Setup-Tools/blob/main/Indy_Aries-demo_Agent_setup.md)

---

## 📦 Download the Demo Frontend

Pull the pre-built frontend Docker image:

```bash
docker pull rahulbatham/aries-agent:latest
```

---

## ✏️ Create the Environment File

Create a file named `aries-agent.env` in the same directory and paste the following content:

```env
NEXT_PUBLIC_HOLDER_ENDPOINT=http://localhost:8001
NEXT_PUBLIC_ISSUER_ENDPOINT=http://localhost:8021
NEXT_PUBLIC_VERIFIER_ENDPOINT=http://localhost:8031

NEXT_PUBLIC_HOLDER_SOCKET=ws://localhost:8001/ws
NEXT_PUBLIC_ISSUER_SOCKET=ws://localhost:8021/ws
NEXT_PUBLIC_VERIFIER_SOCKET=ws://localhost:8031/ws
```

> ⚠️ **Make sure to replace** the `localhost` values with the actual IP addresses or hostnames your Aries agents are running on.
>
> For example, if your agents are running in Docker with host IP `192.168.1.100`, replace `localhost` with `192.168.1.100`.

---

## 🚀 Run the Frontend UI

Now, run the container with the environment file:

```bash
docker run -d --env-file aries-agent.env -p 3000:3000 rahulbatham/aries-agent:latest
```

> 💡 **Tip:** Replace `<YOUR-IP>` with your actual host machine’s IP address if needed.

---

## 🌐 Access the Demo

Once the container is running, open your browser and go to:

👉 [http://localhost:3000](http://localhost:3000)

---

## 🔁 What Can You Do?

With the frontend UI, you can:

* 🔐 **Issue** credentials from the college (CDAC)
* 📱 **Store** credentials with the student (Virat)
* ✅ **Verify** credentials by the organization (iSocial)
* 🧠 **Understand** how decentralized identity flows work in practice

---

## 🧩 System Overview

```plaintext
+---------+         +---------+         +-----------+
|  CDAC   | ─────▶  |  Virat  | ─────▶  |  iSocial  |
| Issuer  |         | Holder  |         | Verifier  |
+---------+         +---------+         +-----------+
```

---

## ❓ Need Help?

If you run into issues:

* Check the linked setup guides
* Or open an issue on this repository

---

## 🚀 Happy Experimenting!

Explore decentralized identity with Hyperledger Indy & Aries – no coding required!
Enjoy building the future of trust and identity. 🎉

 
