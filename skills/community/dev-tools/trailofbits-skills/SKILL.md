---
name: trailofbits-skills
description: "Security testing skills from creators of Slither, Echidna, Medusa. Smart contract vulnerability scanners, property-based testing, static analysis, and audit tools from Trail of Bits."
version: 1.0.0
metadata:
  openclaw:
    tags: [security, audit, slither, echidna, medusa, smart-contracts, vulnerability-scanner, trail-of-bits]
    official: true
    source: "https://github.com/trailofbits/skills"
---

# Trail of Bits Skills

Official security testing skills from Trail of Bits, creators of Slither, Echidna, and Medusa.

A Claude Code plugin marketplace providing skills for AI-assisted security analysis, testing, and development workflows. Includes smart contract vulnerability scanners for 6+ blockchains (Solidity, Cairo, Solana, TON, Cosmos, Substrate, Algorand), property-based testing guidance, static analysis with CodeQL and Semgrep, audit preparation, and security-focused code review tools.

## Installation

```
/plugin marketplace add trailofbits/skills
```

Or browse and install individual plugins:
```
/plugin menu
```

## Available Security Skills

### Smart Contract Security
- **building-secure-contracts** - Vulnerability scanners for Solidity, Cairo, Solana, TON, Cosmos, Substrate, Algorand
- **entry-point-analyzer** - Identify state-changing entry points for security auditing
- **token-integration-analyzer** - ERC20/ERC721 conformity and weird token pattern detection

### Code Auditing
- **audit-context-building** - Ultra-granular code analysis for audit context
- **differential-review** - Security-focused review of code changes
- **variant-analysis** - Find similar vulnerabilities across codebases
- **static-analysis** - CodeQL, Semgrep, and SARIF parsing toolkit
- **supply-chain-risk-auditor** - Audit dependency supply-chain risks

### Verification
- **property-based-testing** - Property-based testing for multiple languages and smart contracts
- **spec-to-code-compliance** - Specification-to-code compliance checker
- **constant-time-analysis** - Detect timing side-channels in cryptographic code

## Links

- **GitHub**: https://github.com/trailofbits/skills
- **Trail of Bits**: https://www.trailofbits.com
- **Building Secure Contracts**: https://secure-contracts.com
