# ⚓ NigeriaPort Chain

> **Blockchain-based maritime logistics management system for Nigerian seaports — deployed on Ethereum Sepolia Testnet**

[![License: MIT](https://img.shields.io/badge/License-MIT-teal.svg)](https://opensource.org/licenses/MIT)
[![Network: Sepolia](https://img.shields.io/badge/Network-Ethereum%20Sepolia-blue.svg)](https://sepolia.etherscan.io)
[![Status: Live](https://img.shields.io/badge/Status-Live%20on%20Netlify-brightgreen.svg)](https://nigeriaportchain.netlify.app)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.19-363636.svg)](https://soliditylang.org)

-----

## 📌 Overview

NigeriaPort Chain is a decentralised application (DApp) built on the Ethereum blockchain that addresses key operational inefficiencies in Nigerian maritime logistics. The system provides tamper-proof, transparent, and automatically enforced management of:

- **Vessel registration** and status tracking
- **Port berth booking** and allocation
- **Cargo documentation** and electronic Bills of Lading (eBOL)
- **Seafarer certification** and identity management

This project was developed as the practical component of a final-year B.Sc. thesis titled:

> *“Blockchain Technology in Maritime Transport: Applications, Challenges and Future Prospects — A Case Study of Nigeria”*
> 
> **Nigeria Maritime University (NMU), Okerenkoko** — Department of Marine Transport and Logistics Management
> 
> **Author:** Ochuko Jethro Ehwarieme (U2022/TLM/124)
> **Supervisor:** Dr. Obioma Nwaogbe

-----

## 🌐 Live Demo

The DApp is live and accessible via any browser with MetaMask installed:

🔗 **<https://nigeriaportchain.netlify.app>**

> To interact with the DApp, you need:
> 
> 1. [MetaMask](https://metamask.io) browser extension or mobile app
> 1. MetaMask connected to the **Sepolia Testnet**
> 1. Some Sepolia test ETH (free from [sepoliafaucet.com](https://sepoliafaucet.com))

-----

## 📜 Deployed Smart Contracts

All four smart contracts are verified and live on the Ethereum Sepolia Testnet:

|Contract          |Address                                     |Etherscan                                                                                |
|------------------|--------------------------------------------|-----------------------------------------------------------------------------------------|
|VesselRegistry    |`0x124B758750F368297c0c52c3DD1faB0B1Ae5D14C`|[View ↗](https://sepolia.etherscan.io/address/0x124B758750F368297c0c52c3DD1faB0B1Ae5D14C)|
|PortBooking       |`0x3275C9f7AFDfD1626E3173D5b162D4CF6B28d199`|[View ↗](https://sepolia.etherscan.io/address/0x3275C9f7AFDfD1626E3173D5b162D4CF6B28d199)|
|CargoDocumentation|`0x3912C71EcD2fc4897956FdE669C996f8f9Aa9C88`|[View ↗](https://sepolia.etherscan.io/address/0x3912C71EcD2fc4897956FdE669C996f8f9Aa9C88)|
|SeafarerRegistry  |`0xB8A3a784423d0f6f0D02d5Ff1F05a30c5B71169a`|[View ↗](https://sepolia.etherscan.io/address/0xB8A3a784423d0f6f0D02d5Ff1F05a30c5B71169a)|

-----

## 🏗️ System Architecture

```
NigeriaPort Chain
│
├── VesselRegistry.sol        → Vessel registration, IMO tracking, status updates
├── PortBooking.sol           → Berth booking, confirmation, completion, cancellation
├── CargoDocumentation.sol    → Electronic Bill of Lading issuance and transfer
├── SeafarerRegistry.sol      → STCW/NIMASA certificate registration and verification
└── NigeriaPortChain.html     → Single-file DApp frontend (ethers.js v6 + MetaMask)
```

The four contracts are independent but designed to work together:

- A port booking references a registered vessel ID
- An eBOL is linked to both a vessel ID and a booking ID
- A seafarer record is tied to a certificate number verified by the authority wallet

-----

## ⚙️ Smart Contract Features

### VesselRegistry.sol

- Register vessels with name, IMO number, type, flag state, and owner
- Prevent duplicate registrations (same IMO number rejected)
- Restrict registration to the port authority wallet (`onlyAuthority` modifier)
- Update vessel operational status: Registered → In Transit → At Port → Departed → Suspended
- Look up any vessel by ID or IMO number

### PortBooking.sol

- Submit port berth booking requests (open to any connected wallet)
- Automatically assign unique booking IDs
- Prevent double-booking of the same berth at the same port
- Authority functions: confirm, complete, or cancel bookings
- Check real-time berth availability

### CargoDocumentation.sol

- Issue electronic Bills of Lading (eBOL) linked to vessel and booking records
- Transfer eBOL ownership on-chain (shipper → consignee → bank)
- Update cargo status: Issued → In Transit → At Destination Port → Delivered → Disputed
- Retrieve full cargo documentation by eBOL ID

### SeafarerRegistry.sol

- Register seafarers with STCW/NIMASA certificate details
- Record certificate type, issue date, and expiry date
- Update certificate status: Valid → Expired → Suspended → Revoked
- Search seafarers by ID or certificate number
- Prevent duplicate certificate registrations

-----

## 🛠️ Technology Stack

|Layer                |Technology                     |
|---------------------|-------------------------------|
|Smart Contracts      |Solidity 0.8.19                |
|Blockchain Network   |Ethereum Sepolia Testnet       |
|Development & Testing|Hardhat, Mocha, Chai           |
|Deployment           |Remix IDE                      |
|Wallet Integration   |MetaMask                       |
|Frontend             |HTML5, CSS3, Vanilla JavaScript|
|Blockchain Library   |ethers.js v6                   |
|Hosting              |Netlify                        |

-----

## 🚀 Getting Started

### Run the DApp (no setup required)

Simply visit **<https://nigeriaportchain.netlify.app>** with MetaMask installed and connected to Sepolia.

### Run locally

```bash
# Clone the repository
git clone https://github.com/jethrosimeon2-debug/NigeriaPortChain.git

# Open the DApp directly in your browser
# (No build step required — it's a single HTML file)
open NigeriaPortChain.html
```

### Deploy your own contracts

1. Open [remix.ethereum.org](https://remix.ethereum.org)
1. Import the `.sol` files from this repository
1. Compile with Solidity compiler version `0.8.19`
1. Connect MetaMask to Sepolia Testnet
1. Deploy each contract in order: VesselRegistry → PortBooking → CargoDocumentation → SeafarerRegistry
1. Update the contract addresses in `NigeriaPortChain.html`

-----

## 🧪 Test Results

All 8 unit test cases passed during local Hardhat testing:

|Test Case                 |Contract      |Result  |
|--------------------------|--------------|--------|
|Register new vessel       |VesselRegistry|✅ PASSED|
|Retrieve vessel record    |VesselRegistry|✅ PASSED|
|Reject duplicate vessel   |VesselRegistry|✅ PASSED|
|Reject unauthorised access|VesselRegistry|✅ PASSED|
|Submit valid booking      |PortBooking   |✅ PASSED|
|Confirm booking           |PortBooking   |✅ PASSED|
|Retrieve booking record   |PortBooking   |✅ PASSED|
|Reject unregistered vessel|PortBooking   |✅ PASSED|

-----

## 🇳🇬 Nigerian Maritime Context

This system was designed specifically for Nigerian port operations, covering:

- **Apapa Port** (Lagos)
- **Tin Can Island Port** (Lagos)
- **Onne Port** (Rivers State)
- **Warri Port** (Delta State)
- **Calabar Port** (Cross River State)
- **Rivers Port** (Port Harcourt)

Regulatory context: Nigerian Ports Authority (NPA), Nigerian Maritime Administration and Safety Agency (NIMASA), Nigerian Shippers’ Council.

-----

## 📄 Research Background

This prototype was built to address five key problems in Nigerian maritime logistics:

1. **Document fraud** — falsification of Bills of Lading and vessel records
1. **Port delays** — vessel turnaround of 7–14 days vs. global best practice of 24–48 hours
1. **Opaque berth allocation** — non-transparent scheduling processes
1. **No shared tamper-proof system** — NIMASA, NPA, and Customs cannot verify documents in real time
1. **Fraudulent seafarer certificates** — fake STCW credentials posing safety risks

Blockchain smart contracts address all five by encoding enforcement rules directly at the protocol level — no human administrator can override or bypass them.

-----

## 🔮 Future Development

- [ ] Migrate to Hyperledger Fabric for lower transaction costs at national scale
- [ ] Integrate with existing NPA port management systems
- [ ] Add cargo tracking with IoT sensor data feeds
- [ ] Build mobile-native app for seafarers and port agents
- [ ] Implement multi-signature authority for consortium governance
- [ ] Legal recognition of eBOL under Nigerian maritime law

-----

## 📬 Contact

**Ochuko Jethro Ehwarieme**

- GitHub: [@jethrosimeon2-debug](https://github.com/jethrosimeon2-debug)
- Institution: Nigeria Maritime University, Okerenkoko

-----

## 📝 License

This project is licensed under the MIT License — you are free to use, modify, and distribute it with attribution.

-----

*Built with ⚓ for Nigerian maritime logistics — NMU Final Year Project, 2025/2026*
