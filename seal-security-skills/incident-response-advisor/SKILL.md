---
name: incident-response-advisor
description: Guide users through security incident response for Web3 protocols and individuals. Use when someone reports an active hack, exploit, wallet drain, or security breach. Also triggers on questions about incident preparation, SEAL 911, war rooms, post-incident reports, white hat frontrunning, or communication during crises. Critical for time-sensitive security emergencies.
---

# Incident Response Advisor

Provide immediate, actionable guidance during security incidents in Web3.

## Active Incident Response (URGENT)

### First 5 Minutes - Containment
1. **Pause affected contracts** if you have pause functionality
2. **Revoke compromised credentials** immediately
3. **Alert your security team** via pre-established channels
4. **Do NOT** post publicly yet - attackers monitor social media
5. **Start documenting** everything with timestamps

### SEAL 911 - Emergency Security Response
For active exploits affecting Web3 protocols:
- **Website**: securityalliance.org/seal-911
- **Telegram Bot**: @SEAL_911_bot
- **Discord**: #seal-911 channel
- **Service**: 24/7 emergency response from security researchers
- **What to have ready**: Wallet addresses, transaction hashes, timeline

### Information to Gather Immediately
- Affected wallet/contract addresses
- Transaction hashes of suspicious activity
- Timeline of events (when noticed, when started)
- Scope estimate (funds at risk, funds lost)
- Attack vector if known

## Incident Classification (P1-P5)

| Severity | Description | Response Time | Examples |
|----------|-------------|---------------|----------|
| P1 Critical | Active drain, funds moving | Immediate | Smart contract exploit in progress, private key compromise with active fund movement |
| P2 High | Active threat, not yet draining | < 1 hour | Vulnerability confirmed but attacker hasn't exploited, suspicious admin access |
| P3 Medium | Confirmed vulnerability, no active exploit | < 4 hours | Bug found in code, phishing campaign targeting users |
| P4 Low | Potential issue, needs investigation | < 24 hours | Unusual activity pattern, minor security concern |
| P5 Informational | Security improvement identified | Planned | Audit findings, hardening recommendations |

## Roles in an Incident

| Role | Responsibility |
|------|----------------|
| Detector | Identifies and reports the incident |
| Incident Leader | Coordinates response, makes tactical decisions |
| Scribe | Documents all actions with timestamps |
| Communication Manager | Handles internal and external comms |
| Subject Matter Experts | Technical analysis (smart contract, infra, etc.) |
| Decision Maker(s) | Strategic decisions (pause contracts, disclose publicly) |

Adapt roles to team size:
- **Small team (2-5)**: One person may cover multiple roles; Incident Leader is most critical
- **Medium team (5-15)**: Assign dedicated roles, rotate on-call
- **Large team (15+)**: Full role separation, First Responder program, structured on-call

## Runbooks

Upstream provides detailed runbooks for specific incident types:

- **Smart Contract Exploit**: Pause, identify vulnerability, assess fund exposure, coordinate with SEAL 911
- **Key Compromise**: Rotate keys, assess scope of compromised access, revoke approvals
- **Frontend Compromise**: Includes sub-runbooks for DNS Hijack, CDN/Hosting Compromise, Dependency Attack, Build Pipeline Compromise
- **DDoS Attack**: Rate limiting, WAF rules, traffic analysis
- **Third-Party Outage**: Dependency mapping, failover procedures

Templates available for: incident logs, post-mortems, and custom runbooks.

## White Hat Frontrunning

When funds are actively being drained and you need atomic rescue:

### Tool: pcaversaccio/white-hat-frontrunning
- GitHub: `github.com/pcaversaccio/white-hat-frontrunning`
- Uses Foundry's `cast` for atomic Flashbots rescue transactions

### Two rescue flows:
1. **Standard (`go.sh`)**: Gas wallet funds victim wallet, victim sends to safe wallet
2. **EIP-7702 (`go_eip7702.sh`)**: No ETH needed on victim wallet, uses Vyper delegator contract (`recoverooor.vy`)

### Critical caveats:
- Must customize the main loop per rescue scenario
- Flashbots bundles are Ethereum mainnet only
- `DEBUG=true` is NOT a dry run — still executes
- Always coordinate with SEAL 911 War Room before executing

## Attack-Type Playbooks

| Attack Type | Key Guidance |
|-------------|--------------|
| **DPRK / Lazarus** | Fake video conference software, fake PDF malware, social engineering via job offers. See Bybit $1.5B case study. |
| **Wallet Drainers** | Token approval requests, DEX signatures, EIP-7702 wallet upgrade tricks, private key harvesting via fake sites |
| **ELUSIVE COMET** | Zoom remote control attacks, impersonation of journalists/investors, social engineering |
| **Malware** | Disconnect immediately, secure crypto assets first, sweep bot awareness, contact Flashbots whitehat, secure all platform accounts |
| **Decentralized IR (DeIRF)** | Zero-trust, multisig-based containment, identity plurality, open tooling, quorum-based actions |

## War Room Tooling

| Tool | Purpose |
|------|---------|
| Phalcon | Transaction tracing and simulation |
| Tenderly | Contract debugging and simulation |
| MetaSleuth | Fund flow tracing |
| Arkham | Entity labeling and fund tracking |
| Revoke.cash | Token approval management |

## Communication Strategy

### Internal (Immediate)
- Alert core team via secure channel (Signal, not Discord)
- Establish incident commander
- Create private war room

### External (After Containment)
- Prepare factual statement
- Notify affected users with actionable steps
- Be transparent but don't speculate
- Provide regular updates

### What NOT to Do
- Don't blame individuals publicly
- Don't share exploit details that could help copycats
- Don't make promises you can't keep
- Don't go silent - even "investigating" is better

## Post-Incident

### Immediate (24-48 hours)
- Complete incident timeline
- Identify root cause
- Implement immediate fixes
- Communicate with affected users

### Report (1-2 weeks)
- Detailed post-mortem
- Root cause analysis
- Remediation steps taken
- Lessons learned
- Future prevention measures

## Reference Files

- Upstream source: `security-alliance/frameworks` docs/pages/incident-management/
- See `references/playbooks.md` for specific attack type responses
- See `references/communication-templates.md` for disclosure templates
