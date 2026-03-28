# Secureum Community Write-Up

For this assignment, I chose **Cyber Red Teaming** with a focus on **Web3 / smart contract security**. The main community I joined was **Secureum**. I chose it because I wanted a community that was technical, active, and centered on real security learning rather than only crypto news or hype.

The focus of this community is **Ethereum smart contract security**, especially learning how to think like an auditor or attacker when reviewing Solidity code and protocol logic. From both Secureum’s public materials and the posts I saw in the Discord, the community is interested in finding vulnerabilities before real attackers exploit them, understanding historic bug classes, and improving audit skills.

The main challenges and questions I saw being discussed recently were around **reentrancy**, **bridge security**, **invariant finding**, and understanding protocol mechanics in systems like **Uniswap**. I also noticed interest in using AI to help with smart contract analysis, such as finding invariants in Solidity contracts. This made the community feel current and research-driven, not just educational.

The topic that sparked my interest the most was **how small implementation details in smart contracts can create very large security risks**. In Web3, one incorrect assumption about external calls, token behavior, pricing, or cross-chain logic can put real money at risk. That makes the field feel very different from ordinary software bugs.

One fun fact I learned is that when an EVM call transfers a non-zero amount of ETH, the sub-call gets an extra **2300 gas stipend**. That tiny rule can affect whether fallback logic succeeds or fails, which shows how low-level execution details can matter a lot in smart contract security.
