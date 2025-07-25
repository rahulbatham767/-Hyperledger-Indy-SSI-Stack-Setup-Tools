
# 🪪 SSI Credential Flow Demo: Issuer → Wallet → Verifier

This demo walks through the flow of Self-Sovereign Identity (SSI) credentials using Aries agents and a credential portal. The flow includes:

- Issuer Agent issuing credentials
- Wallet (Holder) receiving credentials
- Verifier Agent verifying credentials

---

## ✅ Prerequisites

- Ensure **all three agents** are up and running:
  - Issuer Agent
  - Holder (Wallet) Agent
  - Verifier Agent

- Make sure the **Issuer** has already created a schema with the following attributes:

```

email
dob
address
organization
name
phone
issued_by
credential_no
issued_on

````

- The Issuer should also have:
  - A **Credential Definition ID**
  - An **Issuer DID**

---

## 📦 Docker Images

Pull the required images:

```bash
docker pull rahulbatham/isocial
docker pull rahulbatham/aries-agent
docker pull rahulbatham/ssi-portal
````

---

## ⚙️ Step 1: Aries Agent Setup

### 🔧 Create `.env` file for Aries Agent

Create a file named `aries-agent.env` with the following content:

```env
NEXT_PUBLIC_HOLDER_ENDPOINT=http://localhost:8001
NEXT_PUBLIC_ISSUER_ENDPOINT=http://localhost:8021
NEXT_PUBLIC_VERIFIER_ENDPOINT=http://localhost:8031

NEXT_PUBLIC_HOLDER_SOCKET=ws://localhost:8001/ws
NEXT_PUBLIC_ISSUER_SOCKET=ws://localhost:8021/ws
NEXT_PUBLIC_VERIFIER_SOCKET=ws://localhost:8031/ws
```

### 🚀 Start the Aries Agent

```bash
docker run -d --env-file aries-agent.env -p 3000:3000 rahulbatham/aries-agent
```

Login to the Aries Agent portal at `http://localhost:3000` with:

* **Email**: `cdac@gmail.com`
* **Password**: `password@123`

Go to **Issue Credential** section and:

1. Create a schema with the attributes listed above.
2. Create a credential definition.
3. Copy the **Credential Definition ID** and **Issuer DID**.

---

## ⚙️ Step 2: SSI Portal Setup

### 🔧 Create `.env` file for SSI Portal

Create a file named `ssi-portal.env` with the following content. Replace values accordingly:

```env
NEXT_PUBLIC_ISSUER_ENDPOINT=http://localhost:8021

NEXT_PUBLIC_ISSUER_SOCKET=ws://localhost:8021/ws
NEXT_PUBLIC_VERIFIER_SOCKET=ws://localhost:8031/ws

NEXT_PUBLIC_JWT_SECRET_KEY='rahul'
NEXT_PUBLIC_CRED_DEF_ID=WcbtnSB1anVQW6jPXAhn25:3:CL:12:ssi
NEXT_PUBLIC_ISSUER_DID=WcbtnSB1anVQW6jPXAhn25

MONGODB_URI=mongodb://localhost:27017/ssi-credentials
```

> 📌 Replace `NEXT_PUBLIC_CRED_DEF_ID` and `NEXT_PUBLIC_ISSUER_DID` with the values you copied from the Aries Agent.

### 🚀 Start the SSI Portal

```bash
docker run -d --env-file ssi-portal.env -p 3001:3000 rahulbatham/ssi-portal
```

Access the portal at `http://localhost:3001`, fill in all registration details. The portal will send the credential to the wallet (Virat).

---

## ⚙️ Step 3: iSocial Wallet Agent Setup

### 🔧 Create `isocial.env` file

```env
NEXT_PUBLIC_HOLDER_ENDPOINT=http://localhost:8001
NEXT_PUBLIC_VERIFIER_ENDPOINT=http://localhost:8031

NEXT_PUBLIC_HOLDER_SOCKET=ws://localhost:8001/ws
NEXT_PUBLIC_VERIFIER_SOCKET=ws://localhost:8031/ws

NEXT_PUBLIC_VERIFIER_ALIAS=iSocial
NEXT_PUBLIC_CRED_DEF_ID=WcbtnSB1anVQW6jPXAhn25:3:CL:12:ssi

JWT_SECRET=rahul
```

> 📌 Make sure `NEXT_PUBLIC_CRED_DEF_ID` matches the one from the Aries Agent.

### 🚀 Start the iSocial Wallet Agent

```bash
docker run -d --env-file isocial.env -p 3002:3000 rahulbatham/isocial
```

---

## 🧪 Flow Summary

1. **Issuer Agent** creates schema and credential definition.
2. **SSI Portal** uses Issuer credentials to register a user (e.g., Virat).
3. **Virat’s Wallet** receives credentials from the portal.
4. **Verifier Agent (iSocial)** can request proofs from the holder.

---

## 📝 Example Credential Attributes

```json
{
  "email": "virat@example.com",
  "dob": "1990-11-05",
  "address": "Delhi, India",
  "organization": "CDAC",
  "name": "Virat Kohli",
  "phone": "9876543210",
  "issued_by": "CDAC",
  "credential_no": "CDAC-001",
  "issued_on": "2025-07-25"
}
```

---

## 📌 Notes

* Make sure MongoDB is running for the SSI Portal.
* Update port mappings if you run on different ports.
* For production, secure JWT keys and use HTTPS tunnels for webhooks.

---

## 📬 Support

For any issues or feature requests, feel free to open an [issue](https://github.com/rahulbatham767) or reach out on GitHub.

