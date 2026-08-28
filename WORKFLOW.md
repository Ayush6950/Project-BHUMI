

# 🏛️ B.H.U.M.I.

## Blockchain Hosted Unified Mutation Infrastructure

> A government-oriented hybrid Web2 + Web3 land registry platform designed to create transparent, tamper-evident, and auditable property ownership records.
>
> 
                         BHUMI PLATFORM
                              │
              ┌───────────────┴───────────────┐
              │                               │
        👤 CITIZEN/USER                 🏛️ GOVERNMENT
              │                               │
              ▼                               ▼
       USER LOGIN                         OFFICIAL LOGIN
              │                               │
              ▼                               ▼
       Property Search                 Verification Dashboard
       Buy / Transfer                  KYC Verification
       Upload Documents                Document Verification
       Payment                         Approve / Reject
              │                               │
              └───────────────┬───────────────┘
                              ▼
                     ┌─────────────────┐
                     │    BACKEND      │
                     │ Node + Express  │
                     └────────┬────────┘
                              │
              ┌───────────────┼────────────────┐
              │               │                │
              ▼               ▼                ▼
          PostgreSQL       File Storage      Payment
          / MongoDB        IPFS/S3/etc.      Gateway
              │               │                │
              └───────────────┼────────────────┘
                              │
                     Verification Complete
                              │
                              ▼
                    SHA-256 Document Hash
                              │
                              ▼
                     Authorized Registrar
                              │
                         ethers.js
                              │
                              ▼
                 ┌────────────────────────┐
                 │    LAND REGISTRY       │
                 │    SMART CONTRACT       │
                 └────────────┬───────────┘
                              │
                              ▼
                         BLOCKCHAIN
                              │
              ┌───────────────┼──────────────┐
              ▼               ▼              ▼
         Ownership       Document Hash    Audit Trail
           History          Proof          Timestamp


---

## 📌 Project Overview

**B.H.U.M.I.** is a hybrid blockchain-based digital land registry platform that connects citizens, government authorities, traditional databases, secure document storage, payment systems, and blockchain infrastructure.

The primary goal is **not to replace existing government land databases**, but to introduce a blockchain-based **proof and audit layer** for verified property records.

B.H.U.M.I. allows:

- 👤 Citizens to submit and manage property applications
- 🏛️ Government authorities to verify property and KYC documents
- 📄 Secure off-chain storage of sensitive documents
- 🔐 SHA-256 hashing of verified documents and metadata
- ⛓️ Blockchain-based ownership and audit records
- 💰 INR-based payments without requiring citizens to own cryptocurrency
- 🔄 Transparent ownership transfer history
- 🧾 Tamper-evident document verification

---

## 🎯 Problem Statement

Traditional land registry systems can face challenges such as:

- Fragmented property records
- Difficult ownership-history verification
- Document tampering concerns
- Lack of transparent audit trails
- Manual verification processes
- Complex ownership transfer workflows
- Limited interoperability between systems

B.H.U.M.I. addresses these problems by combining **existing government verification systems with blockchain-based proof**.

---

## 💡 Our Solution

B.H.U.M.I. follows a **Hybrid Web2 + Web3 Architecture**.

Sensitive information stays off-chain, while blockchain stores cryptographic proofs and registry-related information.

```mermaid
flowchart LR
    CITIZEN["👤 Citizen"] --> FRONTEND["B.H.U.M.I. Frontend"]

    GOV["🏛️ Government Authority"] --> ADMIN["Government Dashboard"]

    FRONTEND --> BACKEND["⚙️ Backend<br/>Node.js + Express"]
    ADMIN --> BACKEND

    BACKEND --> DATABASE["🗄️ Database<br/>PostgreSQL / MongoDB"]
    BACKEND --> STORAGE["📁 Secure Storage<br/>IPFS / S3"]
    BACKEND --> PAYMENT["💰 INR Payment Gateway"]

    BACKEND --> VERIFY["🔍 Verification"]
    VERIFY --> HASH["🔐 SHA-256 Hash"]

    HASH --> REGISTRAR["🏛️ Authorized Registrar"]
    REGISTRAR --> CONTRACT["⛓️ LandRegistry Smart Contract"]
    CONTRACT --> BLOCKCHAIN["Blockchain"]

    BLOCKCHAIN --> OWNERSHIP["Ownership History"]
    BLOCKCHAIN --> PROOF["Document Proof"]
    BLOCKCHAIN --> AUDIT["Audit Trail"]
```

---

## 🏗️ System Architecture

The architecture is divided into six major layers:

### 1. 👤 Citizen Layer

Users can:

- Register/Login
- Search properties
- Submit property applications
- Upload documents
- Request ownership transfers
- Make payments
- Track application status
- View ownership history

### 2. 🏛️ Government Layer

Authorized officials can:

- Login securely
- View pending applications
- Verify KYC
- Verify property documents
- Verify ownership
- Approve/Reject applications
- Initiate blockchain registration
- Approve ownership transfers
- View blockchain transactions

### 3. ⚙️ Backend Layer

The backend acts as the central application and security layer.

Responsibilities:

- Authentication
- Authorization
- KYC processing
- Document validation
- Application management
- Payment verification
- Hash generation
- Blockchain interaction
- Audit logging

### 4. 🗄️ Off-Chain Data Layer

Stores sensitive and large data such as:

- Property details
- User information
- KYC information
- Documents
- Photos
- Application records
- Payment records

### 5. ⛓️ Blockchain Layer

Stores:

- Property ID
- Owner blockchain identity
- Document hash
- Owner photo hash
- Metadata hash
- Registration timestamp
- Transfer history
- Property status

### 6. 💰 Payment Layer

Users pay using Indian Rupees (₹) through a payment gateway.

Citizens do not need to purchase cryptocurrency or pay blockchain gas directly.

---

## 🔄 Complete Property Registration Flow

```mermaid
flowchart TB

    START["👤 Citizen"] --> LOGIN["🔐 Login / OTP"]

    LOGIN --> DASHBOARD["📊 Citizen Dashboard"]

    DASHBOARD --> SUBMIT["📝 Submit Property"]

    SUBMIT --> UPLOAD["📄 Upload Documents"]

    UPLOAD --> BACKEND["⚙️ B.H.U.M.I. Backend"]

    BACKEND --> APPLICATION["🆔 Create Application ID"]

    APPLICATION --> PENDING["⏳ Pending Verification"]

    PENDING --> GOV["🏛️ Government Dashboard"]

    GOV --> KYC["🔍 KYC Verification"]
    GOV --> DOC["📄 Document Verification"]
    GOV --> PROPERTY["🏠 Property Verification"]

    KYC --> DECISION{"Verification Result"}
    DOC --> DECISION
    PROPERTY --> DECISION

    DECISION -->|❌ Reject| REJECT["Application Rejected"]

    DECISION -->|✅ Approve| VERIFIED["Property Verified"]

    VERIFIED --> HASH["🔐 Generate SHA-256 Hashes"]

    HASH --> REGISTRAR["🏛️ Authorized Registrar"]

    REGISTRAR --> CONTRACT["⛓️ LandRegistry Smart Contract"]

    CONTRACT --> BLOCKCHAIN["Blockchain"]

    BLOCKCHAIN --> REGISTERED["✅ Property Registered"]

    REGISTERED --> HISTORY["📜 Ownership History"]
```

---

## 🔐 Document Verification Architecture

B.H.U.M.I. does not store complete documents directly on the blockchain.

Instead: the document remains off-chain while its cryptographic hash is recorded on-chain.

This allows an authorized system to later verify whether the document has been modified.

### 👤 Owner Photo Hash

The owner's photograph can also be represented using a cryptographic hash.

The actual photograph remains in secure off-chain storage.

```mermaid
flowchart LR
    subgraph OFFCHAIN["Off-Chain - Sensitive"]
        AADHAAR["Aadhaar Number"]
        AADHAAR_DOC["Aadhaar Document"]
        PHOTO["Full Owner Photograph"]
        PHONE["Phone Number"]
        ADDRESS["Residential Address"]
        KYC_INFO["Other KYC Info"]
    end

    subgraph ONCHAIN["On-Chain - Public"]
        PID["Property ID"]
        OWNER_ID["Blockchain Owner Identity"]
        DOC_HASH["Document Hash"]
        PHOTO_HASH["Photo Hash"]
        META_HASH["Metadata Hash"]
        TS["Timestamp"]
        STATUS["Registry Status"]
    end

    AADHAAR_DOC -->|SHA-256| DOC_HASH
    PHOTO -->|SHA-256| PHOTO_HASH
    KYC_INFO -->|SHA-256| META_HASH
```

**❌ Never store directly on a public blockchain:**
- Aadhaar number
- Aadhaar document
- Full owner photograph
- Phone number
- Residential address
- Personal KYC information
- Other sensitive personal information

**✅ Store on-chain:**
- Property ID
- Blockchain owner identity
- Document hash
- Photo hash
- Metadata hash
- Timestamp
- Registry status

---

## 🧾 Smart Contract Architecture

The smart contract represents the blockchain registry state.

```solidity
struct Property {
    bytes32 propertyId;
    address currentOwner;
    bytes32 documentHash;
    bytes32 ownerPhotoHash;
    bytes32 metadataHash;
    uint256 registeredAt;
    uint256 lastTransferAt;
    PropertyStatus status;
    bool exists;
}

enum PropertyStatus {
    Pending,
    Verified,
    Active,
    Frozen,
    Disputed
}
```

---

## ⛓️ Blockchain Interaction Flow

The frontend should not directly interact with the blockchain.

Instead, B.H.U.M.I. follows a backend-first architecture.

### Core Principle

```mermaid
flowchart TB
    A["Frontend"] --> B["Backend"]
    B --> C["Verification"]
    C --> D["Hash Generation"]
    D --> E["Authorized Registrar"]
    E --> F["Smart Contract"]
    F --> G["Blockchain"]
```

---

## 💰 INR Payment Architecture

Citizens should not have to understand cryptocurrency or blockchain gas.

The user sees a simple checkout:

> **Property Transfer Fee**
> ₹25,000
> **[ Pay Now ]**

The backend handles the blockchain infrastructure.

### ⛽ Blockchain Gas Model

Citizens should **not** be required to do this:

```mermaid
flowchart LR
    A["Buy ETH"] --> B["Connect MetaMask"]
    B --> C["Pay Gas"]
    C --> D["Register Property"]
```

Instead, this happens behind the scenes:

```mermaid
flowchart LR
    A["Citizen Pays ₹ via Gateway"] --> B["Backend Confirms Payment"]
    B --> C["Backend-Managed Wallet Pays Gas"]
    C --> D["Property Registered On-Chain"]
```

This creates a Web2-like experience for citizens while blockchain operates as the underlying infrastructure.

---

## 🏛️ Government Verification Workflow

```mermaid
flowchart TB
    A["🏛️ Government Official Login"] --> B["📋 View Pending Applications"]
    B --> C["🔍 Open Application"]
    C --> D["🪪 Verify KYC"]
    C --> E["📄 Verify Documents"]
    C --> F["🏠 Verify Property Records"]

    D --> G{"All Checks Passed?"}
    E --> G
    F --> G

    G -->|❌ No| H["Reject / Request Resubmission"]
    G -->|✅ Yes| I["Approve Application"]

    I --> J["🔐 Trigger Hash Generation"]
    J --> K["🏛️ Authorized Registrar Signs Transaction"]
    K --> L["⛓️ Recorded on Blockchain"]
```

---

## 🔄 Ownership Transfer Flow

Once a property is registered, ownership transfer can follow this process:

```mermaid
flowchart TB
    A["👤 Current Owner Initiates Transfer"] --> B["📝 Submit Transfer Request"]
    B --> C["👤 New Owner KYC"]
    C --> D["📄 Upload Transfer Documents"]
    D --> E["💰 Pay Transfer Fee (INR)"]
    E --> F["🏛️ Government Verification"]
    F --> G{"Approved?"}
    G -->|❌ No| H["Transfer Rejected"]
    G -->|✅ Yes| I["🔐 Generate New Hashes"]
    I --> J["🏛️ Authorized Registrar"]
    J --> K["⛓️ Smart Contract Updates Owner"]
    K --> L["📜 Ownership History Updated"]
```

---

## 🗃️ Data Storage Strategy

B.H.U.M.I. follows an off-chain + on-chain storage model.

| Data | Storage |
|---|---|
| User Profile | Off-chain |
| Aadhaar / KYC | Secure Off-chain |
| Owner Photo | Secure Off-chain |
| Property Documents | Secure Off-chain |
| Property Metadata | Off-chain |
| Payment Details | Off-chain |
| Application Data | Database |
| Property ID | Blockchain |
| Owner Blockchain Address | Blockchain |
| Document Hash | Blockchain |
| Photo Hash | Blockchain |
| Metadata Hash | Blockchain |
| Registration Timestamp | Blockchain |
| Ownership History | Blockchain |

---

## 🔐 Security Model

B.H.U.M.I. follows several security principles.

**Authentication**
- JWT / secure session authentication
- OTP-based authentication
- Role-based access control
- Government official authentication

**Authorization**
- Role-based access control (Citizen / Official / Admin)
- Least-privilege API access

**Blockchain Security**
- Authorized registrar wallet
- Backend-controlled transactions
- No private keys in frontend
- Secure environment variables
- Transaction logging
- Smart contract access control

---

## 🧩 Technology Stack

**Frontend**
- React.js
- Vite
- Tailwind CSS
- Framer Motion

**Backend**
- Node.js
- Express.js
- REST API
- JWT Authentication

**Database**
- PostgreSQL / MongoDB
- Prisma / Mongoose

**Blockchain**
- Solidity
- Ethereum-compatible blockchain
- Hardhat / Foundry
- ethers.js

**Storage**
- IPFS
- Pinata
- Amazon S3

**Payments**
- INR Payment Gateway
- Razorpay or equivalent approved provider

**Infrastructure**
- Docker
- AWS
- CI/CD
- Secure Secrets Management

---

## 📁 Project Structure

```
BHUMI/
│
├── frontend/
│   ├── src/
│   ├── components/
│   ├── pages/
│   ├── hooks/
│   └── services/
│
├── backend/
│   ├── controllers/
│   ├── routes/
│   ├── models/
│   ├── middleware/
│   ├── services/
│   └── utils/
│
├── contracts/
│   ├── src/
│   │   └── LandRegistry.sol
│   ├── script/
│   └── test/
│
├── docs/
│   └── architecture/
│
├── .env.example
├── docker-compose.yml
└── README.md
```

---

## 🔁 End-to-End Architecture

The complete B.H.U.M.I. system:

```mermaid
flowchart TB

    subgraph USERS["👥 Users"]
        CITIZEN["👤 Citizen"]
        OFFICIAL["🏛️ Government Official"]
    end

    subgraph APPLICATION["💻 B.H.U.M.I. Application"]
        FRONTEND["React Frontend"]
        DASHBOARD["Government Dashboard"]
        BACKEND["Node.js + Express"]
    end

    subgraph OFFCHAIN["🗄️ Off-Chain Infrastructure"]
        DATABASE["PostgreSQL / MongoDB"]
        STORAGE["IPFS / S3"]
        PAYMENT["INR Payment Gateway"]
    end

    subgraph VERIFICATION["🔍 Verification Layer"]
        KYC["KYC Verification"]
        DOC["Document Verification"]
        PROPERTY["Property Verification"]
        HASH["SHA-256 Hash Generation"]
    end

    subgraph BLOCKCHAIN["⛓️ Blockchain Layer"]
        REGISTRAR["Authorized Registrar"]
        CONTRACT["LandRegistry.sol"]
        CHAIN["Blockchain"]
    end

    CITIZEN --> FRONTEND
    OFFICIAL --> DASHBOARD

    FRONTEND --> BACKEND
    DASHBOARD --> BACKEND

    BACKEND --> DATABASE
    BACKEND --> STORAGE
    BACKEND --> PAYMENT

    BACKEND --> KYC
    BACKEND --> DOC
    BACKEND --> PROPERTY

    KYC --> HASH
    DOC --> HASH
    PROPERTY --> HASH

    HASH --> REGISTRAR
    REGISTRAR --> CONTRACT
    CONTRACT --> CHAIN

    CHAIN --> HISTORY["📜 Ownership History"]
    CHAIN --> PROOF["🔐 Document Proof"]
    CHAIN --> AUDIT["📋 Audit Trail"]
```

---

## 📊 Property Lifecycle

```mermaid
stateDiagram-v2
    [*] --> Pending
    Pending --> Verified: Government approves
    Pending --> Rejected: Government rejects
    Verified --> Active: Registered on blockchain
    Active --> Disputed: Dispute raised
    Disputed --> Active: Dispute resolved
    Active --> Frozen: Frozen by authority
    Frozen --> Active: Unfrozen
    Active --> Active: Ownership transferred
    Rejected --> [*]
```

### 🆔 Example Property Record

**Off-chain database**

```json
{
  "propertyId": "PROP-MP-BPL-001",
  "surveyNumber": "123/4",
  "district": "Bhopal",
  "tehsil": "Huzur",
  "village": "Example Village",
  "area": "1500 sq.ft",
  "landType": "Residential",
  "status": "VERIFIED"
}
```

**Blockchain record**

| Field | Value |
|---|---|
| Property ID | `PROP-MP-BPL-001` |
| Current Owner | `0x1234...ABCD` |
| Document Hash | `8e7d...a93f` |
| Owner Photo Hash | `91ab...73cd` |
| Metadata Hash | `a821...9d72` |
| Registered At | Blockchain Timestamp |
| Status | `ACTIVE` |

---

## 🧠 Why Blockchain?

B.H.U.M.I. uses blockchain specifically where it provides value.

**Traditional Database**

```mermaid
flowchart LR
    A["Record"] --> B["Can be modified by authorized database operations"]
```

**B.H.U.M.I.**

```mermaid
flowchart LR
    A["Verified Record"] --> B["SHA-256 Hash"]
    B --> C["Blockchain"]
    C --> D["Timestamp + Immutable History"]
```

Blockchain provides:

- 🔐 Tamper-evident records
- 📜 Transparent ownership history
- ⏱️ Verifiable timestamps
- 🔍 Easier auditability
- 🤝 Shared trust between authorized stakeholders

> **Important:** Blockchain does not automatically prove that a document is legally genuine. Government/authorized verification is still required before recording the verified state.

---

## 🚀 Future Scope

B.H.U.M.I. can be extended with:

- 🗺️ GIS-based land mapping
- 🤖 AI-assisted document verification
- 🧠 OCR for land documents
- 🔎 Duplicate property detection
- 📱 Mobile application
- 🏛️ Government API integration
- 🔗 Interoperability with existing land-record systems
- 🪪 Digital identity integration
- 📜 Automated mutation workflows
- 🔔 SMS / email notifications
- 📊 Government analytics dashboard
- 🧾 Automated compliance checks
- 🌐 Multi-state deployment
- 🏘️ Rural citizen support

---

## 🌱 Social & Economic Impact

B.H.U.M.I. aims to improve:

**Transparency**
Citizens and authorized authorities can track the history of verified property records.

**Trust**
Cryptographic hashes provide tamper-evident proof of recorded documents.

**Efficiency**
Digital workflows can reduce manual coordination between citizens and authorities.

**Accessibility**
Citizens can interact with the platform using INR, without needing to understand cryptocurrency.

**Auditability**
Blockchain provides a verifiable transaction history for authorized stakeholders.

---

## ⚠️ Important Design Considerations

B.H.U.M.I. is designed as a prototype / architectural model and would require integration with actual government systems, legal frameworks, identity infrastructure, payment providers, and data-protection requirements before production deployment.

Blockchain should be treated as a verification and audit layer, not as a replacement for legal land records.

---

## 🏆 Core Innovation

The key innovation of B.H.U.M.I. is the combination of:

```
Government Verification
        +
Secure Off-Chain Storage
        +
Cryptographic Hashing
        +
Authorized Blockchain Registration
        +
INR-Based Payments
        =
Transparent Hybrid Land Registry
```
