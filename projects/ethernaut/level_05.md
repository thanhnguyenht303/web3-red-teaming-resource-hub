# Ethernaut Token Level Attack

## Goal

The goal of this level is for you to hack the basic token contract below

---

## Vulnerable Contract
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

contract Token {
    mapping(address => uint256) balances;
    uint256 public totalSupply;

    constructor(uint256 _initialSupply) public {
        balances[msg.sender] = totalSupply = _initialSupply;
    }

    function transfer(address _to, uint256 _value) public returns (bool) {
        require(balances[msg.sender] - _value >= 0);
        balances[msg.sender] -= _value;
        balances[_to] += _value;
        return true;
    }

    function balanceOf(address _owner) public view returns (uint256 balance) {
        return balances[_owner];
    }
}
```

## Root cause

```solidity
function transfer(address _to, uint256 _value) public returns (bool) {
    require(balances[msg.sender] - _value >= 0);
    balances[msg.sender] -= _value;
    balances[_to] += _value;
    return true;
}
```

The problem cause here is `uint256` in version 0.6.0 and `balances[msg.sender] - _value >= 0`. As `balances[msg.sender]` is `uint256`, it cannot be negative, so in version 0.6.0, substract more than balance, it underflows and wraps to maximum value. 

## Attack plan
Step 1: Start with `balances[player] = 20;` then vulnerable check is `require(balances[msg.sender] - _value >= 0);` 

Step 2: Call `await contract.transfer("0xContractAddress", 21)`. Happens: 20-21 not become -1, it wraps around to `2^256 - 1`. So the balance becomes an extremely large number, much greater than 20.

Step 3: Check `(await contract.balanceOf(player)).toString()` to see a huge token balance.