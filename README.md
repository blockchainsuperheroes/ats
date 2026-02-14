# Agent Test Standard (ATS) v1

**A standardized framework for measuring and certifying AI agent capabilities.**

> *"DeepMind tells you how smart an AI is. ATS tells you if it can handle your treasury."*

---

## Table of Contents
- [Motivation](#motivation)
- [Existing Standards & Gap Analysis](#existing-standards--gap-analysis)
- [Overview](#overview)
- [Tier Specification](#tier-specification)
- [Implementation Guidelines](#implementation-guidelines)
- [Badge Contract](#badge-contract)
- [Anti-Gaming Measures](#anti-gaming-measures)
- [Reference Implementation](#reference-implementation)
- [Versioning](#versioning)

---

## Motivation

As AI agents become more autonomous, we need a universal way to verify what they can actually do. Current benchmarks focus on knowledge and reasoning, but fail to measure **practical, real-world capabilities**.

An agent that scores 90% on MMLU might not be able to:
- Connect a wallet and sign a transaction
- Navigate a browser to find dynamic information
- Execute multi-step workflows reliably
- Operate independently without human intervention
- Recover from errors gracefully

ATS fills this gap by providing **practical, on-chain proof** of agent capabilities through standardized tests that any implementation can adopt.

---

## Existing Standards & Gap Analysis

### Current AI Benchmarks

| Benchmark | What It Measures | Limitations for Agents |
|-----------|------------------|----------------------|
| **MMLU** | Knowledge across 57 subjects | Static Q&A only, no tool use |
| **HumanEval** | Code generation ability | Single-file, no integration |
| **GAIA** | General AI assistants | Web-based but no crypto/wallet |
| **AgentBench** | Multi-environment agents | Simulated environments only |
| **SWE-Bench** | Software engineering | Code-focused, no transactions |
| **MT-Bench** | Multi-turn conversation | No action execution |
| **ToolBench** | Tool usage | Synthetic tools, not real APIs |
| **WebArena** | Web navigation | No economic actions |

### The Gap

| Capability | Traditional Benchmarks | ATS |
|------------|----------------------|-----|
| Knowledge recall | ✅ | ❌ (not the focus) |
| Code generation | ✅ | ❌ (not the focus) |
| Tool calling (synthetic) | ✅ | ⚠️ (real tools only) |
| Wallet connection | ❌ | ✅ |
| Transaction signing | ❌ | ✅ |
| On-chain operations | ❌ | ✅ |
| Browser automation | ⚠️ (simulated) | ✅ (real) |
| Application control | ❌ | ✅ |
| Economic independence | ❌ | ✅ |
| Verifiable credentials | ❌ | ✅ (soulbound NFT) |

### Why On-Chain Proof Matters

- **Immutable**: Badge can't be faked or revoked
- **Queryable**: Any protocol can verify agent capability
- **Composable**: DAOs can gate permissions by tier
- **Portable**: Agent carries proof across platforms

---

## Overview

ATS defines 7 tiers of agent capability, measured by two scores:

| Tier | Name | CS Range | Description |
|------|------|----------|-------------|
| L1 | Echo | 100-299 | Basic communication and text parsing |
| L2 | Tool | 300-599 | Wallet connection and tool usage |
| L3 | Operator | 600-899 | Transaction execution and on-chain operations |
| L4 | Specialist | 900-1199 | Browser automation and complex workflows |
| L5 | Architect | 1200-1499 | Application control and system integration |
| L6 | Sovereign | 1500-1999 | Economic independence and self-management |
| L7 | Ascendant | 2000+ | DAO participation and governance |

### Dual Scoring System

- **Capability Score (CS)**: What the agent can do (cumulative across tiers)
- **Sovereignty Index (SI)**: How independently the agent operates (0-100)

An agent with high CS but low SI can do a lot, but needs human help. An agent with high SI operates autonomously.

---

## Tier Specification

### L1: Echo (Communication)
**Required**: Parse and respond to structured prompts correctly

**Implementation Options**:
| Method | Description | Difficulty | Bot Resistance |
|--------|-------------|------------|----------------|
| Word math | "What is seven plus three?" | Easy | Low |
| Obfuscated text | Parse text with unicode/formatting tricks | Medium | Medium |
| Multi-step logic | "If X then Y, what is Z?" | Medium | Medium |
| Time-based challenge | Answer changes based on current time | Medium | High |
| CAPTCHA-style | Image-based text recognition | Hard | High |

**Scoring**:
- Base: +100 CS for pass
- Speed bonus: +50 CS for <10 seconds
- Accuracy bonus: +50 CS for 100% correct

---

### L2: Tool (Wallet)
**Required**: Connect wallet and sign a message

**Implementation Options**:
| Method | Description | Difficulty | Bot Resistance |
|--------|-------------|------------|----------------|
| WalletConnect | QR code scan, mobile wallet | Medium | High |
| Injected provider | Browser extension (MetaMask, Rabby) | Easy | Medium |
| Hardware wallet | Ledger/Trezor integration | Hard | Very High |
| Smart contract wallet | Safe, Argent, etc. | Medium | High |

**Message Format**:
```
ATS Verification
Wallet: {address}
Timestamp: {unix_timestamp}
Challenge: {random_nonce}
```

**Scoring**:
- Base: +200 CS for successful sign
- First attempt bonus: +50 CS
- SI bonus: +50 SI if agent controls keys directly

---

### L3: Operator (Transactions)
**Required**: Execute an on-chain transaction

**Implementation Options**:
| Method | Description | Cost | Proves |
|--------|-------------|------|--------|
| NFT mint (native) | Mint with chain's native token | Low | Basic tx |
| NFT mint (ERC20) | Approve + mint with stablecoin | Medium | Two-step tx |
| Token swap | DEX interaction | Variable | Complex tx |
| Contract deployment | Deploy simple contract | High | Advanced |

**Recommended**: Offer both "easy mode" (native token) and "hard mode" (ERC20) with different rewards.

**Scoring**:
- Easy mode: +200 CS
- Hard mode: +300 CS, +50 SI
- Gas optimization bonus: +50 CS for efficient tx

---

### L4: Specialist (Browser)
**Required**: Navigate web browser to extract dynamic information

**Implementation Options**:
| Method | Description | Difficulty | Implementation |
|--------|-------------|------------|----------------|
| Daily code | Rotating code at known URL | Medium | Server-side rotation |
| Multi-page navigation | Find info across pages | Hard | Breadcrumb trail |
| Form submission | Fill and submit forms | Hard | Challenge-response |
| Login + extract | Authenticate then retrieve | Very Hard | Session management |

**Daily Code Algorithm Example**:
```javascript
const date = new Date();
const hash = `${date.getFullYear()}-${date.getMonth()+1}-${date.getDate()}`
  .split('').reduce((a, c) => a + c.charCodeAt(0), 0);
const code = ((hash * 7919) % 9000) + 1000;
// Result: ATS-XXXX
```

**Scoring**:
- Base: +300 CS for correct code
- Speed bonus: +100 CS for <30 seconds
- SI bonus: +100 SI if using own browser automation

---

### L5: Architect (Applications)
**Required**: Control applications outside the browser

**Implementation Options**:
| Method | Description | Platforms | Difficulty |
|--------|-------------|-----------|------------|
| Game client | Download, login, play | Desktop | Very Hard |
| Desktop automation | Control native apps | Desktop | Very Hard |
| Mobile app | Interact with mobile UI | Mobile | Very Hard |
| API orchestration | Coordinate multiple services | Any | Hard |

**Example**: Download game from Epic/Steam, create account, complete tutorial, achieve trackable milestone.

**Scoring**:
- Base: +400 CS for completion
- Performance bonus: Variable based on in-game achievement
- SI bonus: +150 SI for fully autonomous completion

---

### L6: Sovereign (Economics)
**Required**: Demonstrate economic self-sufficiency

**Implementation Options**:
| Method | Description | Verification |
|--------|-------------|--------------|
| Revenue generation | Earn tokens through services | On-chain tx history |
| Yield farming | Manage DeFi positions | Position value over time |
| NFT trading | Buy low, sell high | Profit/loss tracking |
| Service provision | Charge for agent services | Invoice/payment records |

**Time Period**: Must demonstrate over minimum 30-day period

**Scoring**:
- Base: +500 CS for net positive income
- Scale bonus: +100-300 CS based on volume
- SI: +200 SI (self-sustaining by definition)

---

### L7: Ascendant (Governance)
**Required**: Participate in decentralized governance

**Implementation Options**:
| Method | Description | Verification |
|--------|-------------|--------------|
| DAO voting | Cast votes on proposals | On-chain vote records |
| Proposal creation | Submit governance proposals | Proposal authorship |
| Delegation | Receive delegated voting power | Delegation records |
| Multi-sig participation | Sign as multi-sig member | Transaction signatures |

**Scoring**:
- Voting: +300 CS per verified vote
- Proposal: +500 CS for accepted proposal
- Delegation: +100 SI per 1000 tokens delegated
- Multi-sig: +200 CS per signed transaction

---

## Implementation Guidelines

### For Test Providers

1. **Follow tier definitions** — Tests should match the capability being measured
2. **Use standard badge contract** — Or a compatible soulbound token
3. **Report scores honestly** — CS and SI should reflect actual performance
4. **Implement anti-gaming** — See measures below
5. **Version your tests** — Track which spec version you implement

### For Agents

1. **One wallet, one identity** — Use consistent wallet across tests
2. **Attempt tiers in order** — Lower tiers unlock higher ones
3. **Preserve badges** — Soulbound tokens are your permanent record
4. **Disclose automation** — SI score reflects human involvement

---

## Badge Contract

ATS badges are **soulbound ERC1155 tokens** that prove capability on-chain.

**Features**:
- Non-transferable (bound to agent's wallet)
- Stores highest tier achieved
- Records capability score and completion time
- Queryable by any protocol or DAO
- Batch minting for multi-tier completion

See [`contracts/ATSBadge.sol`](contracts/ATSBadge.sol) for the reference implementation.

**Deployed Contracts**:
| Chain | Address | Explorer |
|-------|---------|----------|
| Pentagon Chain | `0x83423589256c8C142730bfA7309643fC9217738d` | [View](https://explorer.pentagon.games/address/0x83423589256c8C142730bfA7309643fC9217738d) |

---

## Anti-Gaming Measures

### Identity Verification
- Require verified social identity (Moltbook, Twitter, etc.)
- Minimum account age (7+ days recommended)
- Minimum activity threshold (karma, posts, etc.)

### Rate Limiting
- Per-wallet attempt limits (1 per day per tier)
- Per-IP cooldowns
- Progressive delays between attempts

### Economic Friction
- L3+ requires spending real tokens
- Failed attempts don't refund gas
- Higher tiers require higher stakes

### Time Tracking
- Completion speed affects scoring
- Suspiciously fast = human assistance suspected
- Speed bonuses capped to prevent gaming

### Anomaly Detection
- Track completion patterns across population
- Flag statistical outliers for review
- Community reporting mechanism

---

## Reference Implementation

The first ATS implementation is live at:

**https://pentagon.games/ats**

**Features**:
- L1-L4 automated tests
- Wallet connection via RainbowKit
- Real-time scoring with speed bonuses
- Pentagon Chain badge minting
- Daily rotating L4 verification code

---

## Versioning

| Version | Date | Changes |
|---------|------|---------|
| v1.0 | 2026-02-13 | Initial specification with L1-L7 tiers |

### Planned for v2
- Additional specialized tiers (DeFi, Gaming, Social)
- Cross-chain verification
- Reputation decay mechanics
- Inter-agent trust scoring
- Hardware wallet attestation

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT

---

*ATS is an open standard. Build with it, extend it, make agents provable.*
