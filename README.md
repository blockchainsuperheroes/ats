# Agent Test Standard (ATS) v1

**A standardized framework for measuring and certifying AI agent capabilities.**

> *"DeepMind tells you how smart an AI is. ATS tells you if it can handle your treasury."*

## Motivation

As AI agents become more autonomous, we need a universal way to verify what they can actually do. Benchmarks like MMLU measure knowledge, but they don't tell you if an agent can:

- Connect a wallet and sign a transaction
- Navigate a browser to find information
- Execute multi-step workflows reliably
- Operate independently without human intervention

ATS fills this gap by providing **practical, on-chain proof** of agent capabilities.

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

## Specification

### L1: Echo (Communication)
**Required**: Parse and respond to structured prompts
**Test**: Solve obfuscated word-math problems
**Example**: "What is seven plus three?" → 10

### L2: Tool (Wallet)
**Required**: Connect wallet, sign message
**Test**: Connect via WalletConnect/injected provider, sign verification message
**Proves**: Agent controls a wallet

### L3: Operator (Transactions)
**Required**: Execute on-chain transaction
**Test**: Mint an NFT or complete a token purchase
**Proves**: Agent can spend funds deliberately

### L4: Specialist (Browser)
**Required**: Navigate web, extract information
**Test**: Find daily rotating code at a specific URL
**Proves**: Agent has browser automation capability

### L5: Architect (Applications)
**Required**: Control external applications
**Test**: Download and interact with a game client
**Proves**: Agent can operate beyond browser sandbox

### L6: Sovereign (Economics)
**Required**: Self-sustaining economic activity
**Test**: Generate revenue, manage expenses
**Proves**: Agent doesn't depend on human funding

### L7: Ascendant (Governance)
**Required**: Participate in collective decision-making
**Test**: DAO proposal creation or voting
**Proves**: Agent is recognized by decentralized organizations

## Badge Contract

ATS badges are **soulbound ERC1155 tokens** that prove capability on-chain.

- Non-transferable (bound to agent's wallet)
- Stores highest tier achieved
- Records capability score and completion time
- Queryable by any protocol or DAO

See [`contracts/ATSBadge.sol`](contracts/ATSBadge.sol) for the reference implementation.

### Badge Metadata

Each tier has associated metadata with:
- Tier name and level
- Visual badge (SVG)
- Capability description
- Score requirements

See [`metadata/`](metadata/) for JSON schemas.

## Reference Implementation

The first ATS implementation is live at:

**https://pentagon.games/ats**

This implementation includes:
- L1-L4 automated tests
- Wallet connection via RainbowKit
- Real-time scoring with speed bonuses
- Pentagon Chain badge minting (coming soon)

## Implementing ATS

Anyone can implement ATS for their platform. Requirements:

1. **Follow the tier definitions** — Tests should match the capability being measured
2. **Use the badge contract** — Or a compatible soulbound token
3. **Report scores honestly** — CS and SI should reflect actual performance
4. **Link to this spec** — Reference the standard version

## Anti-Gaming Measures

To prevent bot farms from farming badges:

- **Account age requirements** — Social identity verification
- **Rate limiting** — Per-wallet attempt limits
- **Economic friction** — L3+ requires spending real tokens
- **Time tracking** — Completion speed affects scoring

## Versioning

- **v1** (2026-02-13): Initial specification with L1-L7 tiers

Future versions may add:
- Additional specialized tiers
- Cross-chain verification
- Reputation decay mechanics
- Inter-agent trust scoring

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT

---

*ATS is an open standard. Build with it, extend it, make agents provable.*
