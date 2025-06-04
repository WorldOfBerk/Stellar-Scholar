# StellarScholar

## About me!

- **Name**: Barış Berk Şengül  
- Final-year Computer Engineering student at Maltepe University, Istanbul  
- Completed a full-year Erasmus+ program at TH Köln, Germany  
- Focused on blockchain, AI, and embedded systems  
- Built chatbot apps and real-time classroom interaction systems  
- Joined Stellar Bootcamp to explore smart contract development  
- This is my first end-to-end project using Rust and Soroban on Stellar

## Description

StellarScholar is a smart contract-based scholarship management system built on the Stellar blockchain using Soroban. It allows educational institutions to register students and associate them with GPA scores. The contract automatically distributes token-based scholarships to students who meet a minimum GPA requirement. This system reduces human error, prevents bias, and ensures that only eligible students receive financial support. Each student has a wallet address linked to their profile, and scholarship funds are sent directly to that wallet. The project also includes freeze and unfreeze functions, allowing institutions to pause payments if needed, such as during academic suspension or verification delays. StellarScholar creates a transparent, reliable, and efficient solution for managing scholarships. It is ideal for universities, NGOs, and public education foundations that want to modernize and automate their aid programs while maintaining accountability and trust.


## Vision

StellarScholar aims to transform the way scholarships are distributed globally by using blockchain technology. By automating financial aid through smart contracts, it ensures fairness, transparency, and speed. Students receive their rewards directly into their wallets based on academic performance, without human bias or delays. This project can serve as a scalable and trustable model for scholarship systems in both public and private sectors worldwide.

1. **Define core data structures and variables**
   - `students: Map<Address, StudentRecord>`  
     A mapping of wallet addresses to GPA and eligibility status.
   - `StudentRecord`: Struct with `gpa: u32`, `is_frozen: bool`, `is_registered: bool`

2. **Implement registration and GPA management functions**
   - `register_student(address: Address, gpa: u32)`  
     Only callable by admin (institution), adds student to map.
   - `update_gpa(address: Address, new_gpa: u32)`  
     Updates the GPA for an existing student.

3. **Add freeze and unfreeze functions**
   - `freeze_account(address: Address)`  
     Temporarily blocks scholarship disbursement to the given student.
   - `unfreeze_account(address: Address)`  
     Re-enables payment for the student.

4. **Implement scholarship distribution logic**
   - `distribute_scholarship(min_gpa: u32, amount: u64)`  
     Loops through registered students and transfers tokens to those who:
     - Are not frozen  
     - Have GPA >= `min_gpa`

5. **(Optional) Develop a simple frontend (React or HTML/JS)**
   - Interface for institutions to manage students and trigger `distribute_scholarship()`
   - Student wallet view showing GPA, status, and payment history

6. **Deploy to Stellar testnet and document contract address**
   - Compile with Soroban CLI, deploy to testnet
   - Record and publish contract ID in README

## Personal story:
I joined the Stellar Bootcamp to explore smart contracts, even though I had no prior experience with Rust or Soroban. While I couldn’t follow all the sessions live, I was determined to complete the final project and learn by doing. I chose to build a scholarship distribution system because I believe education should be fair and transparent. This project helped me understand how blockchain can solve real-world problems and made me more confident in developing decentralized applications.

## 🛠️ How to Install and Deploy StellarScholar

### Prerequisites

Make sure you have the following installed:

- [Rust](https://www.rust-lang.org/tools/install)
- [Soroban CLI](https://soroban.stellar.org/docs/install/soroban-cli)
- [Docker (optional, for local testing)](https://docs.docker.com/get-docker/)

### Clone the Repository

```bash
git clone https://github.com/yourusername/stellar-scholar.git
cd stellar-scholar
```

### Build The Smart Contract
```bash
soroban contract build
```
This will compile the smart contract to WASM and output it under the target/wasm32-unknown-unknown/release directory.

### Deploy to Stellar Testnet
```bash
soroban contract deploy \
  --wasm target/wasm32-unknown-unknown/release/stellar_scholar.wasm \
  --network testnet
```
You will receive a Contract ID – make sure to copy and save it for interaction.

### Interact with the Contract (Example)
Register a student (replace addresses and values):
```bash
soroban contract invoke \
  --id <your_contract_id> \
  --fn register_student \
  --arg address=<student_wallet_address> \
  --arg gpa=3
```
Distribute scholarships:
```bash
soroban contract invoke \
  --id <your_contract_id> \
  --fn distribute_scholarship \
  --arg min_gpa=2 \
  --arg amount=1000
```
