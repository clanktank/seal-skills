# seal-skills

SEAL Security Knowledge Graph — 27 security domains from [security-alliance/frameworks](https://github.com/security-alliance/frameworks) as AI agent skills following the [Agent Skills](https://agentskills.io) open standard.

## Install

### Option 1: Copy directly

```bash
cp -r seal/ ~/.hermes/skills/seal
```

### Option 2: Clone

```bash
git clone https://github.com/clanktank/seal-skills.git ~/.hermes/skills/seal
```

### Option 3: Skills Hub (if published)

```bash
hermes skills tap add clanktank/seal-skills
hermes skills install seal-incident-management
```

## Verify installation

```bash
hermes chat --toolsets skills -q "What seal skills do you have?"
```

## Usage

Ask a security question. The agent uses `INDEX.md` to match your question to a domain, then loads that skill.

```
> My wallet was drained, what do I do?
# Agent loads seal-incident-management + seal-wallet-security + seal-safe-harbor

> How do I set up multisig for our treasury?
# Agent loads seal-multisig-for-protocols + seal-treasury-operations

> We're hiring remote devs, any security concerns?
# Agent loads seal-dprk-it-workers + seal-opsec
```

Or invoke directly:

```
/seal-wallet-security
/seal-incident-management How do I handle a drainer attack?
```

## Structure

Each skill follows the [Agent Skills spec](https://agentskills.io) + Hermes conventions:

```
~/.hermes/skills/seal/
├── INDEX.md                         # MOC trigger table (read by agent on load)
├── .baseline.json                   # Quality metrics for version tracking
├── .skill-writing-playbook.md       # Best practices for improving skills
├── README.md
│
├── awareness/
│   ├── SKILL.md                     # Frontmatter + When to Use + Key Concepts
│   └── references/                  # On-demand deep content
│       ├── threat-vectors.md
│       ├── scam-patterns.md
│       └── resources.md
│
├── incident-management/
│   ├── SKILL.md
│   └── references/
│       ├── playbooks/
│       │   ├── hacked-drainer.md
│       │   ├── malware.md
│       │   └── dprk-war-room.md
│       ├── lessons-learned.md
│       └── communication-strategies.md
│
├── ... (23 more domains)
└── wallet-security/
    ├── SKILL.md
    └── references/
        ├── seed-phrase-management.md
        ├── hardware-wallets.md
        └── ...
```

## SKILL.md format

```yaml
---
name: seal-incident-management
description: >
  Security incident lifecycle — detection, response, containment, communication,
  lessons learned, and playbooks for specific attack types. Use when someone
  reports a hack, suspicious activity, or needs IR guidance.
metadata:
  category: security
  tags: [incident-response, playbooks, detection, containment]
  related_skills: [seal-safe-harbor, seal-opsec, seal-wallet-security]
---

# Incident Management

## When to Use
- User reports a compromised wallet or protocol
- Suspicious transaction detected
- Need for IR playbook or escalation

## Related Domains
This skill connects to: seal-safe-harbor, seal-opsec, seal-wallet-security

## Key Concepts
[framework content — cleaned from security-alliance/frameworks]

## References
- Playbooks (references/playbooks/)
- Communication Strategies

## Pitfalls
[improvements planned — see versioning below]
```

## How navigation works

1. Agent reads `INDEX.md` trigger table to find matching domain
2. `skill_view("seal-incident-management")` loads the SKILL.md
3. `related_skills` in frontmatter tells agent which domains to also load
4. `skill_view("seal-incident-management", "references/playbooks/hacked-drainer.md")` for deep content
5. Agent follows cross-references until it has enough context

## Domains (27)

| Domain | Focus | Ref Files |
|---|---|---|
| awareness | Threat recognition, phishing, culture | 5 |
| certs | Certification frameworks | 10 |
| community-management | Discord/Telegram/social security | 4 |
| devsecops | Secure development pipelines | 5 |
| dprk-it-workers | DPRK worker infiltration | 5 |
| encryption | Encryption strategies | 10 |
| ens | ENS security | 5 |
| external-security-reviews | Audit management | 8 |
| front-end-web-app | Web/mobile security | 4 |
| governance | Compliance, risk, metrics | 3 |
| iam | Identity and access management | 3 |
| incident-management | Incident response, playbooks | 9 |
| infrastructure | OS, network, cloud security | 11 |
| monitoring | Alerting, thresholds | 2 |
| multisig-for-protocols | Multisig operations | 13 |
| opsec | Operational security | 62 |
| privacy | Privacy tools and practices | 7 |
| safe-harbor | Whitehat protection | 5 |
| secure-software-development | Secure coding | 4 |
| security-automation | Automated security | 3 |
| security-testing | Testing methodologies | 6 |
| supply-chain | Dependency security | 2 |
| threat-modeling | Threat modeling | 2 |
| treasury-operations | Treasury security | 4 |
| user-team-security | Team security training | 3 |
| vulnerability-disclosure | Responsible disclosure | 2 |
| wallet-security | Wallet types, seed phrases, multisig | 18 |

## Versioning

Every change is measured against `.baseline.json`. Metrics tracked:

| Metric | v1.0 (current) | Notes |
|---|---|---|
| Gotchas sections | 0/27 | Highest-signal content per playbook |
| `[[wikilinks]]` | 0 | Cross-domain navigation |
| Avg words/skill | 203 | Scope/depth indicator |
| Avg description length | 130 chars | Trigger specificity |
| Key concepts populated | 27/27 | Already done |

To compare versions:

```bash
git diff v1.0..HEAD -- .baseline.json
```

## Source

- Frameworks: https://github.com/security-alliance/frameworks
- Skill standard: https://agentskills.io
- Hermes docs: https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills
- Best practices: See `.skill-writing-playbook.md`
