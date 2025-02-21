# 💰 Transaction Receipt Smart Contract  

## 📜 Description  
The **Transaction Receipt Smart Contract** is a blockchain-based system that **automatically issues receipts** for transactions. Each receipt logs the **sender’s address, receiver’s address, transaction amount, and timestamp**, ensuring **transparency, immutability, and verifiability** on-chain.  

## 🚀 Features  
- **Automated Receipt Generation** for every transaction.  
- **Immutable Records** ensuring tamper-proof transaction logs.  
- **Event Emission** for real-time tracking and external monitoring.  
- **Easy Retrieval** of receipts with transaction details.  
- **No Deployment Inputs Required**, making it simple to use.  

## 📂 Smart Contract Code  
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract TransactionReceipt {
    struct Receipt {
        address sender;
        address receiver;
        uint256 amount;
        uint256 timestamp;
    }

    Receipt[] public receipts;

    event ReceiptIssued(address indexed sender, address indexed receiver, uint256 amount, uint256 timestamp);

    function issueReceipt(address _receiver) public payable {
        require(msg.value > 0, "Transaction must include value");
        
        receipts.push(Receipt(msg.sender, _receiver, msg.value, block.timestamp));
        emit ReceiptIssued(msg.sender, _receiver, msg.value, block.timestamp);
    }

    function getReceipt(uint256 index) public view returns (address, address, uint256, uint256) {
        require(index < receipts.length, "Invalid index");
        Receipt memory receipt = receipts[index];
        return (receipt.sender, receipt.receiver, receipt.amount, receipt.timestamp);
    }

    function getTotalReceipts() public view returns (uint256) {
        return receipts.length;
    }
}
