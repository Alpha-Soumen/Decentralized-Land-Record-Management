# Decentralized Land Record Management  

## Problem Statement  
Traditional land ownership records are vulnerable to fraud, disputes, and inefficiencies due to centralized or manual record-keeping. A blockchain-powered Land Registry System enhances security, transparency, and immutability in land registration and ownership transfers. By leveraging smart contracts, the system automates verification, eliminates forgery, and ensures that only legitimate owners can transfer property.  

## Project Description  
This project leverages blockchain technology to create a secure, decentralized, and transparent land registry system. It eliminates the need for centralized authorities, preventing fraud and unauthorized modifications of ownership records.  

### **Key Features:**  
- **Decentralized Ownership:** Eliminates reliance on centralized authorities for land registration.  
- **Immutable Records:** Blockchain ensures land data cannot be altered or forged.  
- **Smart Contract Enforcement:** Automates ownership verification and transfer processes.  
- **Fraud-Resistant System:** Prevents duplicate or unauthorized land registrations.  
- **Trustless Transactions:** Eliminates intermediaries, reducing delays and costs.  
- **Real-Time Verification:** Anyone can instantly check property details on the blockchain.  
- **Proof of Authenticity:** Only verified owners can initiate property transfers.  
- **Tamper-Proof Digital Ledger:** Ensures permanent, transparent land records.  
- **Ethereum-Based Architecture:** Uses Solidity smart contracts for security and efficiency.  
- **Global Accessibility:** Provides cross-border verification of property ownership.  

---  

## **Technologies Used**  
- **Blockchain Platform:** Ethereum  
- **Smart Contract Language:** Solidity  
- **Development Environment:** Remix IDE  

---  

## **Installation & Deployment Guide**  

### **Step 1: Clone the Repository**  
```sh  
git clone https://github.com/Alpha-Soumen/Decentralized-Land-Record-Management.git  
cd Decentralized-Land-Record-Management  
```

### **Step 2: Open Remix IDE**  
1. Visit [Remix IDE](https://remix.ethereum.org/)  
2. Create a new Solidity file (`LandRegistry.sol`)  
3. Copy and paste the provided smart contract code into the file  

### **Step 3: Compile the Smart Contract**  
- In Remix, select the Solidity compiler (version 0.8.0 or later)  
- Click the "Compile" button to ensure there are no errors  

### **Step 4: Deploy the Smart Contract**  
- Navigate to the "Deploy & Run Transactions" tab  
- Select "Injected Web3" or "JavaScript VM" as the environment  
- Click "Deploy" and confirm the transaction  

### **Step 5: Register a Land Parcel**  
- Call `registerLand(landID, "Location", area)`  
- The land will be stored on the blockchain, and an event will be emitted  

### **Step 6: Transfer Ownership**  
- Call `transferOwnership(landID, newOwnerAddress)`  
- Only the current owner can initiate the transfer  

### **Step 7: Verify Land Details**  
- Use `getLand(landID)` to fetch and verify land ownership information  

---  

## **Smart Contract Code**  
```solidity  
// SPDX-License-Identifier: MIT  
pragma solidity ^0.8.0;  

contract LandRegistry {  
    struct Land {  
        uint256 id;  
        string location;  
        uint256 area;  
        address owner;  
        bool registered;  
    }  

    mapping(uint256 => Land) public lands;  

    event LandRegistered(uint256 indexed landId, string location, uint256 area, address indexed owner);  
    event OwnershipTransferred(uint256 indexed landId, address indexed oldOwner, address indexed newOwner);  

    function registerLand(uint256 _id, string memory _location, uint256 _area) public {  
        require(!lands[_id].registered, "Land already registered");  

        lands[_id] = Land({  
            id: _id,  
            location: _location,  
            area: _area,  
            owner: msg.sender,  
            registered: true  
        });  

        emit LandRegistered(_id, _location, _area, msg.sender);  
    }  

    function transferOwnership(uint256 _id, address _newOwner) public {  
        Land storage land = lands[_id];  
        require(land.registered, "Land not registered");  
        require(land.owner == msg.sender, "Only the owner can transfer ownership");  

        address oldOwner = land.owner;  
        land.owner = _newOwner;  

        emit OwnershipTransferred(_id, oldOwner, _newOwner);  
    }  

    function getLand(uint256 _id) public view returns (uint256, string memory, uint256, address, bool) {  
        Land memory land = lands[_id];  
        require(land.registered, "Land not registered");  

        return (land.id, land.location, land.area, land.owner, land.registered);  
    }  

    function isLandRegistered(uint256 _id) public view returns (bool) {  
        return lands[_id].registered;  
    }  
}  
```

---  

## **Output Screenshots**  
  ![Screenshot 2025-02-10 101156](https://github.com/user-attachments/assets/5dc68af4-b2e3-4f3e-b4e8-9eb0b2a174bf)

  ![Screenshot 2025-02-10 102538](https://github.com/user-attachments/assets/99672756-7199-47b3-ae08-54b9a2f16e51)



---  

## 👨‍💻 Developed by
**Soumen Bhunia:** [LinkedIn ](https://www.linkedin.com/in/soumen-bhunia-2b8799293/)

---  

## **License**  
This project is licensed under the **MIT License**.  



