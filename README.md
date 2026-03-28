# Web3 Red Teaming Resource Hub

> A beginner-friendly but serious public resource page for **Cyber Red Teaming** with an emphasis on **Web3 / smart contract security**.  
> Main community focus: **Secureum**.

## Why this page exists
I created this page to start building the hacker habit of **Research, Bookmark, Organize, Iterate/Improve, Share (RBOIS)**. My main focus area is **Cyber Red Teaming**, specifically **Web3 / smart contract security**. I am still new to this space, so I organized this page in a way that would help another beginner get started faster.

---

## Communities

### Main community
- **Secureum** — https://www.secureum.xyz/bootcamp/  
  Smart contract security learning community focused on Ethereum, Solidity, auditing, RACEs, bootcamp content, and security events.
- **Secureum YouTube Playlist** — https://www.youtube.com/playlist?list=PLiAoBT74VLnmK3Kc188fL37aviYjXeaPc  
  Public playlist with ETH 101, Solidity, security pitfalls, and audit techniques.
- **Secureum TrustX** — https://www.secureum.xyz/trustx/  
  Ethereum security event connected to the Secureum ecosystem.
- **Secureum CARE** — https://github.com/secureum/CARE  
  "Comprehensive Audit Readiness Evaluation" project for improving code readiness before audits.

### Other Web3 / smart contract security communities
- **ETHSecurity (Telegram)** — https://t.me/ETHSecurity
- **Ethereum Hackers Discord (listed by ethereum.org)** — https://ethereum.org/community/online/
- **Code4rena community** — https://docs.code4rena.com/getting-started/how-to-participate
- **Sherlock (Watsons)** — https://docs.sherlock.xyz/audits/watsons
- **Immunefi** — https://immunefi.com/
- **Smart Contract Security Alliance** — https://www.smartcontractsecurityalliance.com/

### Broader cyber / red team communities
- **Red Team Village** — https://redteamvillage.io/
- **OWASP Community / WSTG** — https://owasp.org/www-project-web-security-testing-guide/
- **MITRE ATT&CK** — https://attack.mitre.org/

---

## Researchers / Publishers / Companies worth following

### Individuals
- **Rajeev (Secureum)** — https://www.secureum.xyz/
- **samczsun** — https://samczsun.com/
- **Dominik Muhs** — https://scsfg.io/about/

### Companies / orgs / publishers
- **Trail of Bits blog** — https://blog.trailofbits.com/
- **OpenZeppelin blog & Ethernaut** — https://ethernaut.openzeppelin.com/
- **ConsenSys Diligence** — https://diligence.security/
- **Cyfrin** — https://www.cyfrin.io/blog
- **Code4rena docs** — https://docs.code4rena.com/
- **Sherlock docs** — https://docs.sherlock.xyz/
- **Smart Contract Security Field Guide** — https://scsfg.io/

### What I would track regularly
- Reentrancy writeups
- Bridge exploit analysis
- Invariant testing / fuzzing content
- Competitive audit findings
- Postmortems of major DeFi incidents

---

## Tools

### Web3 / smart contract security tools
- **Foundry** — https://getfoundry.sh/  
  Build, test, fuzz, debug, deploy, and verify smart contracts.
- **Foundry GitHub** — https://github.com/foundry-rs/foundry
- **Slither** — https://github.com/crytic/slither  
  Static analyzer for Solidity and Vyper.
- **Slither detectors** — https://github.com/crytic/slither/wiki/Detector-Documentation
- **Echidna** — https://github.com/crytic/echidna  
  Property-based fuzzer for Ethereum smart contracts.
- **Scribble** — https://diligence.security/scribble/  
  Specification language for writing properties about smart contracts.
- **Tenderly** — https://tenderly.co/
- **Smart Contract Security Field Guide (Hackers)** — https://scsfg.io/hackers/

### General red team tools / frameworks
- **MITRE ATT&CK** — https://attack.mitre.org/
- **OWASP Web Security Testing Guide** — https://owasp.org/www-project-web-security-testing-guide/
- **OWASP ASVS** — https://owasp.org/www-project-application-security-verification-standard/
- **LOLBAS** — https://lolbas-project.github.io/

---

## Writeups / Case Studies

### Topics I saw discussed or linked from the Secureum community
- **Reentrancy / DAO-style bugs** — https://0x00auditor.medium.com/the-reentrancy-riddle-dissecting-the-legendary-bug-that-changed-ethereum-forever-e450fc01def7
- **Web3Bugs knowledge base** — https://github.com/ZhangZhuoSJTU/Web3Bugs/tree/main
- **Bridge security series** — https://x.com/caliber_tweets/status/1991911741408862259
- **Uniswap mechanics explainer** — https://paragraph.com/@uniquetalash77@gmail.com/how-swaps-actually-work-in-uniswap-v1-%E2%86%92-v4

### Strong public learning resources
- **Secureum bootcamp article** — https://secureum.substack.com/p/secureum-bootcamp-for-smart-contract
- **Smart Contract Security Field Guide** — https://scsfg.io/
- **Trail of Bits blockchain posts** — https://blog.trailofbits.com/categories/blockchain/
- **samczsun research archive** — https://samczsun.com/

---

## Events / Conferences / Media Repositories

### Web3 / smart contract security
- **Secureum TrustX** — https://www.secureum.xyz/trustx/
- **Trillion Dollar Security Day (Ethereum Foundation + Secureum TrustX)** — https://blog.ethereum.org/2026/02/03/1ts-day-devconnect-ba
- **DappCon** — https://dappcon.io/
- **ETHGlobal events** — https://ethglobal.com/
- **Paradigm CTF overview** — https://www.alchemy.com/dapps/paradigm-ctf

### Broader cyber / red team
- **Red Team Village** — https://redteamvillage.io/
- **Red Team Village YouTube** — https://www.youtube.com/redteamvillage
- **DEF CON Blockchain Village playlist** — https://www.youtube.com/playlist?list=PL9fPq3eQfaaDqrnDrbV-H9GBSBBtnflSw
- **Crypto & Privacy Village** — https://cryptovillage.org/

---

## Rabbit Holes

### Rabbit hole #1 — Reentrancy
Why it matters: it is one of the most famous smart contract bugs and still shapes how people think about external calls, state updates, and secure withdrawals.
- Reentrancy explainer — https://0x00auditor.medium.com/the-reentrancy-riddle-dissecting-the-legendary-bug-that-changed-ethereum-forever-e450fc01def7
- Slither detector docs — https://github.com/crytic/slither/wiki/Detector-Documentation
- Ethernaut — https://ethernaut.openzeppelin.com/

### Rabbit hole #2 — Invariants and fuzzing
Why it matters: this seems to be where Web3 security starts to feel more like real security engineering and less like simple linting.
- Echidna — https://github.com/crytic/echidna
- Scribble — https://diligence.security/scribble/
- Foundry — https://getfoundry.sh/
- Field Guide (testing) — https://scsfg.io/developers/testing/

### Rabbit hole #3 — Bridge security
Why it matters: bridges are high-value and complicated, so mistakes can become catastrophic.
- Bridge security series — https://x.com/caliber_tweets/status/1991911741408862259
- Trail of Bits blockchain posts — https://blog.trailofbits.com/categories/blockchain/

### Fun fact
When an EVM call transfers a non-zero amount of ETH, the sub-call gets an extra **2300 gas stipend**. Tiny EVM rules like this can completely change whether a fallback succeeds or fails.

---

## Obscure / surprising resources
- **ETHSecurity Telegram** — https://t.me/ETHSecurity  
  Feels more like an insider hallway conversation than a polished website.
- **Secureum CARE repo** — https://github.com/secureum/CARE  
  Useful because it shows “audit readiness” as a discipline before the audit even starts.
- **Smart Contract Security Alliance** — https://www.smartcontractsecurityalliance.com/  
  Helpful for standards and broad ecosystem thinking.
- **Smart Contract Security Field Guide** — https://scsfg.io/  
  Surprisingly comprehensive and very beginner-friendly.

---

## Starter Projects

### Project 1 — Complete Ethernaut and document solutions
Goal: learn core vulnerability classes through hands-on levels.
- Resource: https://ethernaut.openzeppelin.com/
- Deliverable: a writeup repo with one folder per level, exploit explanation, and lessons learned.

### Project 2 — Build a simple Solidity project and run Slither + Foundry fuzz tests
Goal: start thinking like a developer and an auditor at the same time.
- Resources: https://getfoundry.sh/ and https://github.com/crytic/slither
- Deliverable: one sample contract, unit tests, fuzz tests, Slither report, and short security notes.

### Project 3 — Solve 1–2 Damn Vulnerable DeFi challenges
Goal: move from toy vulnerabilities to more protocol-like logic bugs.
- Resource: https://www.damnvulnerabledefi.xyz/
- Deliverable: exploit walkthroughs and a “what invariant was broken?” reflection.

---

## My short notes on Secureum as a community
Secureum is the main community I chose for this assignment because it feels focused, technical, and serious about learning smart contract security. Based on the public Secureum ecosystem and the Discord posts I reviewed, the community is centered on Ethereum security, Solidity, audit thinking, vulnerability patterns, and practical learning. The topics that stood out most in my browsing were **reentrancy**, **bridge security**, **invariant finding**, **competitive auditing**, and understanding how protocols like **Uniswap** actually work.

What I liked most is that the community does not seem focused on random hype. Instead, it rewards people who can reason about risk, read code carefully, and understand how small implementation details lead to large financial consequences.

---

## Beginner path I would recommend
1. Read Secureum + Field Guide overview material.
2. Learn Solidity basics and EVM basics.
3. Play Ethernaut.
4. Learn Foundry.
5. Run Slither on toy contracts.
6. Learn fuzzing and invariants with Echidna / Foundry / Scribble.
7. Try Damn Vulnerable DeFi.
8. Observe Code4rena or Sherlock contests before competing.

---

## Reflection
I found this assignment more useful than I expected because the hardest part was not finding “a” resource, but finding **good** resources and organizing them into something another beginner could actually use. I started with Secureum, but while researching I found a larger Web3 security ecosystem that includes training platforms, audit contests, standards efforts, fuzzing tools, postmortem writers, and general red team communities.

I do think someone new to the field could use this page as a starting point, especially if they want a path that moves from general red teaming into Web3 security. If I keep improving this page, I would add more exploit writeups, more beginner notes, and my own walkthroughs after I finish hands-on labs.
