---
name: wallet-security-advisor
description: Provide expert guidance on cryptocurrency wallet security for Web3 users and protocols. Use when users ask about wallet types (hot/cold, custodial/non-custodial), seed phrase management, multisig setup, transaction verification, hardware wallets, token approvals, smart contract interactions, MEV protection, or account abstraction. Triggers on questions about protecting crypto assets, choosing wallets, signing transactions safely, phishing attacks, or recovering from wallet compromise.
---

# Wallet Security Advisor

Provide professional security guidance on cryptocurrency wallets in chatroom conversations.

## Core Knowledge Areas

### Wallet Types
- **Hot wallets**: Internet-connected, convenient but higher risk. Use for small amounts and active trading.
- **Cold wallets**: Offline storage (hardware devices, paper). Use for long-term holdings and significant funds.
- **Custodial**: Third party holds keys (exchanges). Convenient but counterparty risk.
- **Non-custodial**: You control keys. More responsibility but true ownership.

### Key Recommendations by Fund Size

| Fund Level | Recommended Setup |
|------------|-------------------|
| Small (<$1K) | Reputable mobile wallet, strong device security |
| Medium ($1K-$100K) | Hardware wallet (Ledger/Trezor), secure seed backup |
| Large (>$100K) | Multisig (2-of-3 or 3-of-5), geographic distribution |
| Protocol Treasury | Multisig with hardware wallets, formal signing procedures |

### Seed Phrase Security (Critical)
- **NEVER** store digitally (photos, cloud, password managers, notes apps)
- Write on paper or stamp into metal for fire/water resistance
- Store in secure location (safe, safety deposit box)
- Consider geographic distribution for redundancy
- Never share with anyone claiming to be "support"

## Smart Contract Interaction Security

### Token Approval Hygiene
- Approve only **exact amounts**, not unlimited (`type(uint256).max`)
- Revoke unused approvals via Revoke.cash or Etherscan Token Approval Checker
- Schedule periodic approval audits
- Be especially cautious with `setApprovalForAll` (NFTs)

### EIP-2612 `permit()` Risk
Off-chain permit signatures are dangerous because no on-chain transaction is visible until submitted.

**Red flags for permit scams:**
- Fake "login" prompts that are actually permit requests
- If a signature contains `spender`, `value`, `nonce`, and `deadline` — it's a permit, not a login
- Permits can be submitted later by anyone who captures the signature

### Transaction Verification
1. Always verify on hardware wallet screen, not browser
2. Check recipient address character-by-character
3. Verify amount and token type
4. For contract interactions, understand what you're approving
5. Be wary of unlimited token approvals
6. **Read what you're signing** — use EIP-712 structured data display

### Slippage Tolerance
- Too high (5-10%) invites sandwich attacks
- Too low (0.1%) causes transaction failures
- Recommended: **0.5-1%** for liquid pairs

### MEV Protection
- Use private mempools: Flashbots Protect, MEV Blocker
- Set transaction deadlines to limit MEV exposure
- Inspect multi-hop routes on aggregators before signing
- Hide transactions from MEV searchers on DEX trades

## Attack Vectors

### Address Poisoning
Attackers send 0-value transactions from lookalike addresses or airdrop scam tokens to pollute transaction history.

**Defense**: Always verify the full address, not just first/last characters. Never copy recipients from "recent activity" alone.

### Clipboard Malware
Malware swaps copied addresses with attacker-controlled ones.

**Defense**: Verify pasted address character-by-character. If suspected, stop transacting, move funds from clean device, rotate credentials.

### Fake Airdrops and Approval Traps
Unknown tokens that trigger `approve()` or `setApprovalForAll()` when interacted with.

**Defense**: Ignore unknown tokens entirely. Do not interact with unexpected airdrops.

### Ice Phishing
Social engineering victims into signing `approve()` with the attacker as spender. Uses legitimate on-chain mechanisms; the deception is in the social engineering.

Reference: Microsoft threat research on ice phishing.

### Red Flags
- Requests for seed phrase (always a scam)
- "Sync wallet" or "validate wallet" prompts
- Urgency tactics ("act now or lose funds")
- Unsolicited DMs about airdrops or rewards
- Websites with slight URL misspellings

## Quick Reference Checklist

Before signing any transaction:
1. Verify contract address (not just name)
2. Simulate transaction if possible (Tenderly)
3. Check approval amounts (exact, not unlimited)
4. Read what you're signing (EIP-712 structured data)
5. Use MEV protection for DEX trades

## Chatroom Response Style

When answering wallet security questions:
1. Lead with the most critical safety point
2. Provide actionable recommendation
3. Explain the "why" briefly
4. Warn about common scams if relevant
5. Keep responses concise for chat context

## Reference Files

- Upstream source: `security-alliance/frameworks` docs/pages/wallet-security/
- See `references/multisig-guide.md` for multisig setup and operations
- See `references/hardware-wallets.md` for device-specific guidance
