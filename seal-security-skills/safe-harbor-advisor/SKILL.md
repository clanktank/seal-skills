---
name: safe-harbor-advisor
description: Guide protocols on SEAL's Whitehat Safe Harbor framework for pre-authorizing whitehat fund rescues during active exploits. Use when users ask about protecting against hacks, enabling whitehat intervention, Safe Harbor adoption, bounty structures for rescuers, or legal protection for security researchers. Triggers on questions about "Safe Harbor," "whitehat rescue," "fund recovery during exploit," or "protecting user funds from hacks."
---

# Safe Harbor Advisor

Help protocols adopt the SEAL Whitehat Safe Harbor framework to enable pre-authorized fund rescues during active exploits.

## What is Safe Harbor?

Safe Harbor is a legal and technical framework that lets protocols **pre-authorize whitehats** to step in during active exploits, rescue funds, and return them - with clear legal protection for everyone involved.

**Key Concept**: During an active hack, every second counts. Safe Harbor removes legal ambiguity that prevents security researchers from helping.

## Proven Results

**$150M+ recovered by whitehats** through Safe Harbor.

## Why Safe Harbor Matters

> The Nomad hack drained $190M over hours while whitehats stood by, willing to help but unable to act without legal protection.

**Without Safe Harbor**:
- Whitehats risk legal liability for intervening
- Delays while negotiating terms during active exploit
- Funds often lost completely

**With Safe Harbor**:
- Whitehats can act immediately
- Pre-defined bounty terms (no negotiation)
- Dramatically improved fund recovery odds

## Who Has Adopted

Safe Harbor protects **$68B+ in assets** across **20+ protocols** including:
- Aave
- Uniswap
- Pendle
- PancakeSwap
- Balancer
- Silo Finance
- ZKsync

## How Safe Harbor Protects Your Protocol

### 1. Protocols Pre-Authorize Rescues
Define in advance:
- Which assets/contracts are covered
- Where rescued funds should go
- What bounty terms apply
- Any identity requirements

### 2. Whitehats Act During Active Exploits
Safe Harbor **only** applies when:
- Exploit is already in progress or imminent (e.g., in mempool)
- Immediate action required to prevent fund loss
- **NOT** for bug bounty reports (use responsible disclosure instead)

### 3. Funds Returned, Bounty Paid
- Whitehats must return funds within 6 hours (with reason) or 48 hours
- Bounty is automatic and pre-defined
- No post-hack negotiation needed

## V3 Contracts (Current)

Safe Harbor V3 contracts are **audited by Cyfrin** (January 2026) and deployed via CreateX with **deterministic addresses across all EVM chains**:

| Contract | Address |
|----------|---------|
| SafeHarborRegistry | `0x326733493E143b8904716E7A64A9f4fb6A185a2c` |
| ChainValidator (proxy) | `0xd01C76ccE414d9B0a294abAFD94feD2e0B88675D` |
| AgreementFactory | `0xcf317fE605397bC3fae6DAD06331aE5154F277fF` |

Old multi-address approach (AgreementV2, AgreementFactoryV2, SafeHarborRegistryV2) is replaced with single universal addresses.

### CAIP-2 Chain Identifiers
V3 uses CAIP-2 format for chain IDs:
- Ethereum: `eip155:1`
- Polygon: `eip155:137`

## Key Scope Terms

### Asset Recovery Address
Where whitehats must return rescued funds.
- Use secure multisig (Gnosis Safe, governance-controlled)
- Must handle potentially large inflows

### Security Contact
How whitehats notify you after a rescue.
- Multiple channels (email, Signal, Telegram)
- Must be actively monitored
- Whitehats contact within 6 hours

### Assets Under Scope
Which contracts whitehats can interact with:

| Option | Covers |
|--------|--------|
| **All** | Listed address + all child contracts (current & future) |
| **ExistingOnly** | Address + children deployed before adoption |
| **FutureOnly** | Address + children deployed after adoption |
| **None** | Only the listed address itself |

**Tip**: For factory contracts, use `All` to cover future deployments automatically.

### Bounty Structure

**Formula**: `bounty = min(bountyPercentage × recoveredAmount, bountyCapUSD)`

| Parameter | Recommendation |
|-----------|----------------|
| Bounty Percentage | 10% (industry standard) |
| Bounty Cap (USD) | Match your bug bounty max payout |
| Aggregate Cap | Max total payout if multiple whitehats |
| Retainable | Whether whitehat deducts bounty before returning |

**Important**: Set bounty cap <= bug bounty payout. This ensures no financial incentive to fake a rescue.

### Identity Verification
- **Anonymous**: No KYC (most crypto-native)
- **Pseudonymous**: Requires pseudonym
- **Named**: Legal name + KYC required (most compliant)

## Adoption Paths

### 1. White-Glove Onboarding (Recommended, Free)
SEAL provides scoping assistance, governance language templates, and on-chain registration help.

Apply: [SEAL Onboarding Waitlist](https://form.typeform.com/to/QF3YjWno)

### 2. Self-Adoption Tool
Web tool for generating scope and deploying agreements:
- **URL**: `safeharbor.securityalliance.org/adoption`

### 3. Self-Adoption (Manual)
Step-by-step process:
1. **Define Scope** - Use templates for DAO or non-DAO
2. **DAO Proposal** (if applicable) - Governance vote
3. **On-Chain Registration** - Foundry script at `registry-contracts/script/AdoptSafeHarbor.s.sol` with `agreementDetails.json`, env var `ADOPT_TO_REGISTRY`
4. **Manual Contract Call**: `AgreementFactory.create(AgreementDetails, address chainValidator, address owner, bytes32 salt)` then `SafeHarborRegistry.adoptSafeHarbor(address)`
5. **Update Terms of Service** - Legal coverage for users
6. **Announce** - Public communication

### 4. Third-Party Provider
Adopt through ecosystem partners like Immunefi.

## Skylock Database
- **URL**: `skylock.xyz/safeharbor/database`
- Compiled database of all Safe Harbor adoptions

## FAQ Highlights

**What counts as active exploit?**
Exploit in progress or imminent (mempool, initial funds drained). NOT for vulnerabilities that can be responsibly disclosed.

**Different from bug bounty?**
Bug bounties reward *disclosure before exploit*. Safe Harbor protects *intervention during exploit*.

**What's the risk?**
Minimal. Worst case = status quo (no rescue). Best case = funds saved. Whitehats only protected if they follow all rules.

**Can DAOs adopt?**
Yes - no legal entity needed. Just governance vote and on-chain registration.

**Can non-DAOs adopt?**
Yes - centralized teams just publish scope and terms directly.

**Need legal contract signatures?**
No - uses on-chain registration and public unilateral offer. If whitehat follows rules, agreement is binding.

## Terms of Service Language

Add to TOS when adopting:

> User hereby acknowledges and agrees to, and consents to be bound by the terms and conditions of, that certain Safe Harbor Agreement for Whitehats, adopted by the Protocol Community on [DATE]. Without limiting the generality of the foregoing:
> - the User hereby consents to Whitehats attempting Eligible Funds Rescues of any and all Tokens deposited into the Protocol by the User and the deduction of Bounties out of User's deposited Tokens to compensate Eligible Whitehats for successful Eligible Funds Rescues;
> - the User acknowledges and agrees that Tokens may be lost, stolen, suffer diminished value, or become disabled or frozen in connection with attempts at Eligible Funds Rescues, and assumes all the risk of the foregoing;
> - the User acknowledges that the deduction of a Bounty may constitute a taxable event and the User is solely responsible for any tax obligations arising therefrom;
> - the User agrees to hold harmless other Protocol Community Members from claims arising from Eligible Funds Rescues

Legal agreement (IPFS): `bafkreiernns2f4nv2uzvwtzjc2jboyivsu2mixz33y3xo7cvtllsuao6jy.ipfs.w3s.link`

## Whitehat Pre-Intervention Checklist
1. Confirm exploit is active or imminent
2. Verify Safe Harbor scope covers the affected contracts
3. Confirm you can meet return requirements (6h/48h window)
4. Screen against OFAC sanctions list
5. Coordinate with SEAL 911 War Room recommended

## Audit
- V3 contracts audited by Cyfrin (January 2026)
- Audit: `github.com/security-alliance/safe-harbor/blob/main/documents/2026-01-13-cyfrin-safe-harbor-v2.0.pdf`

## Reference Files

- Upstream source: `security-alliance/frameworks` docs/pages/safe-harbor/
- See `references/adoption-checklist.md` for step-by-step adoption process
