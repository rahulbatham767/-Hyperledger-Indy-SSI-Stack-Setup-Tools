

# 🧪 Indy-Aries Demo: College & Organization Identity Use Case

Welcome to the **Indy-Aries Demo**!  
This project simulates a **real-world credential flow** involving three types of decentralized identity agents:

- 🏫 **CDAC** – *Issuer* (College)
- 👤 **Virat** – *Holder* (Student)
- 🏢 **iSocial** – *Verifier* (Organization)

Explore how Self-Sovereign Identity (SSI) works using Hyperledger Indy and Aries in this easy-to-run demo.

---

## 🛠️ Prerequisites

Before getting started, make sure the following components are set up and running:

- ✅ **Indy Ledger**
- ✅ **Aries Agents**
  - `CDAC` (Issuer)
  - `Virat` (Holder)
  - `iSocial` (Verifier)

> **Need help with setup?**
> - 📘 [No-Code Ledger & Agent Setup (MD)](https://github.com/rahulbatham767/-Hyperledger-Indy-SSI-Stack-Setup-Tools/blob/main/indy-ledger-setup(no-code-approach).md)
> - 📘 [Agent Setup Instructions (MD)](https://github.com/rahulbatham767/-Hyperledger-Indy-SSI-Stack-Setup-Tools/blob/main/Indy_Aries-demo_Agent_setup.md)

---

## 📦 Download the Demo Frontend

Pull the pre-built frontend Docker image:

```bash
docker pull rahulbatham/aries-agent:latest
````

---

## 🚀 Run the Frontend UI

Run the container with appropriate environment variables to connect to your agents:

```bash
docker run -p 3000:3000 \
  -e NEXT_PUBLIC_HOLDER_ENDPOINT=http://<YOUR-IP>:8001 \
  -e NEXT_PUBLIC_ISSUER_ENDPOINT=http://<YOUR-IP>:8021 \
  -e NEXT_PUBLIC_VERIFIER_ENDPOINT=http://<YOUR-IP>:8031 \
  -e NEXT_PUBLIC_HOLDER_SOCKET=ws://<YOUR-IP>:8001/ws \
  -e NEXT_PUBLIC_ISSUER_SOCKET=ws://<YOUR-IP>:8021/ws \
  -e NEXT_PUBLIC_VERIFIER_SOCKET=ws://<YOUR-IP>:8031/ws \
  rahulbatham/aries-agent:latest
```

> 💡 **Tip:**
> Replace `<YOUR-IP>` with your actual host machine’s IP address.

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




