# 📘 Traction Overview - Multi-Tenant SSI Agent Platform

## 🧠 What is Traction?

**Traction** is an open-source project by the Government of British Columbia that extends **Hyperledger Aries Cloud Agent Python (ACA-Py)** to provide a multi-tenant, production-grade SSI platform. It enables issuers, verifiers, and holders to manage digital identities and verifiable credentials in a scalable, extensible, and enterprise-ready way.

---

## ⚙️ Core Features

* ✅ **Multi-Tenant Support**
* ✅ **Webhook-based Event Handling**
* ✅ **Credential Issuance & Verification**
* ✅ **Connection Management**
* ✅ **Tenant Lifecycle & Role Management**
* ✅ **NGROK / LocalTunnel Webhook Integration**
* ✅ **Wallet-based Login for Applications**
* ✅ **API-first Design**

---

## 🏗️ Architecture Overview

### 1. **Core Components**

* **Aries Agent (ACA-Py)** - The base SSI agent with multi-tenancy enabled.
* **Traction API** - Handles tenants, connections, credentials, and proofs.
* **PostgreSQL** - Persistent storage for tenant data and ACA-Py wallets.
* **Redis** - Used for caching and message queues.
* **Webhook Processor** - Listens and handles events.
* **NGROK / Tunnel** - Makes webhooks publicly accessible.

### 2. **Service Roles**

* **Endorser** - Writes schemas and credential definitions to the ledger.
* **Issuer** - Issues verifiable credentials.
* **Verifier** - Sends and verifies proof requests.
* **Holder (Tenant)** - Mobile or web user receiving credentials.

---

## 🚀 Setup Guide (Docker Compose)

### 1. Clone Repository

```bash
git clone https://github.com/bcgov/traction.git
cd traction
```

### 2. Set Environment Variables

Create and edit `.env` file with values like:

```env
NGROK_AUTHTOKEN=<Generate ngrok Auth Token and use in env>
LEDGER_URL=http://ledger:9000
ACAPY_IMAGE=bcgovimages/aries-cloudagent:py36-1.16-1
POSTGRES_USER=traction
POSTGRES_PASSWORD=tractionpw
WEBHOOK_URL=http://host.docker.internal:5000/webhook


> **⚠️ Note:**
> You can directly build and run **Traction**, but you must **add your `NGROK_AUTHTOKEN`** to the environment variables.
>
> 🚫 **Important:** Make sure you are **not connected to an organization's (restricted) network** while running the setup.

### 3. Run Docker Compose


```bash
docker-compose -f docker-compose.yml up --build
```



### 4. Access Services

* Traction tenant: `http://localhost:5101/tenant`
* Admin Swagger UI: `http://localhost:8032`
* Traction Admin: `http://localhost:5101/innkeeper`

---

## 🧪 Traction Demo Flow

### 1. Create a Tenant

```bash
POST /tenants
{
  "name": "gov-issuer",
  "wallet_key": "testkey"
}
```

### 2. Create a Connection Invitation

```bash
POST /tenants/{tenant_id}/connections/create-invitation
```

### 3. Issue a Credential

```bash
POST /tenants/{tenant_id}/issue-credential/send
{
  "connection_id": "...",
  "credential_definition_id": "...",
  "attributes": [{"name": "name", "value": "Alice"}]
}
```

### 4. Request and Verify a Proof

```bash
POST /tenants/{tenant_id}/present-proof/send-request
```

---

## 🛠️ Advanced Topics

### 🔗 Integration with Mobile Wallets

* Generate invitations
* Use QR codes for pairing
* Send credentials from issuer to wallet
* Verify proof from wallet holder

### 🧩 API & Event Hooks

* REST APIs for all tenant actions
* Webhook listener receives real-time updates on:

  * Connections
  * Issuance
  * Proofs

### 🗃️ Multi-Ledger Support

* Configure ACA-Py to use multiple Indy ledgers
* Endorser role handles DID/Schema writing to ledgers

---

## 📈 Use Cases

* Digital College ID issuance
* Employment credential verification
* eKYC/Onboarding for services
* Wallet-based login for 3rd-party portals

---

## 🔗 Resources

* GitHub: [bcgov/traction](https://github.com/bcgov/traction)
* ACA-Py: [Aries Cloud Agent Python](https://github.com/hyperledger/aries-cloudagent-python)
* Aries RFCs: [Aries Interop](https://github.com/hyperledger/aries-rfcs)
* Bifold Wallet: [Hyperledger Mobile Wallet](https://github.com/hyperledger/aries-mobile-agent-react-native)

---

## ✅ Status Summary

* 🧪 Successfully ran Traction with ACA-Py and PostgreSQL
* 🌐 Connected with mobile wallet (Bifold)
* 🧾 Issued and verified credentials
* 🔧 Integrated webhook processing
* 🛠️ Configured multi-ledger and NGROK for demos

---

> Created by Rahul Batham 
