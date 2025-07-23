Here is the GitHub-friendly **Markdown** version styled for clear documentation:

````markdown
# 🧪 Indy-Aries Demo: College & Organization Identity Use Case

## 🛠️ Prerequisites

Before running the demo, make sure the following are set up:

- ✅ **Indy Ledger**
- ✅ **Aries Agents** for:
  - **CDAC** – Issuer
  - **iSocial** – Verifier
  - **Virat** – Holder

> If not set up, follow these guides:

- 📄 [Containerized Indy Ledger and Aries Agent Setup (No-Code Approach)](https://github.com/rahulbatham767/-Hyperledger-Indy-SSI-Stack-Setup-Tools/blob/main/Containerized%20Indy%20Ledger%20and%20Aries%20Agent%20Setup(No-Code%20Approach).pdf)
- 📄 [Indy-Aries Demo Agent Setup Instructions](https://github.com/rahulbatham767/-Hyperledger-Indy-SSI-Stack-Setup-Tools/blob/main/Indy_Aries-demo_Agent_setup.txt)

---

## 📥 Download the Demo Frontend

Pull the pre-built Docker image for the Aries demo frontend:

```bash
docker pull rahulbatham/aries-agent
````

---

## 🚀 Run the Demo Frontend

Run the container with environment variables for the Holder, Issuer, and Verifier agents:

```bash
docker run -p 3000:3000 \
  -e NEXT_PUBLIC_HOLDER_ENDPOINT=http://10.210.13.22:8001 \
  -e NEXT_PUBLIC_ISSUER_ENDPOINT=http://10.210.13.22:8021 \
  -e NEXT_PUBLIC_VERIFIER_ENDPOINT=http://10.210.13.22:8031 \
  -e NEXT_PUBLIC_HOLDER_SOCKET=ws://10.210.13.22:8001/ws \
  -e NEXT_PUBLIC_ISSUER_SOCKET=ws://10.210.13.22:8021/ws \
  -e NEXT_PUBLIC_VERIFIER_SOCKET=ws://10.210.13.22:8031/ws \
  rahulbatham/aries-agent:latest
```

> 🔁 **Note:** Replace `10.210.13.22` with your machine's IP address if it's different.

---

## ✅ Ready to Go!

Access the demo UI at:
[http://localhost:3000](http://localhost:3000)

This frontend enables interaction between the issuer, holder, and verifier agents in a real-world credential flow simulation.


