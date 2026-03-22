# seal-skills

SEAL Security Knowledge Graph — 27 security domains from [security-alliance/frameworks](https://github.com/security-alliance/frameworks) as AI agent skills following the [Agent Skills](https://agentskills.io) open standard.

## Install

### 1. Clone the skills

```bash
git clone https://github.com/clanktank/seal-skills.git ~/.hermes/skills/seal
```

### 2. Add slash commands (Discord)

Copy-paste these into your terminal to register slash commands via the gateway config:

```bash
hermes config set gateway.discord.commands.seal-start.description "Open SEAL Security Coach"
hermes config set gateway.discord.commands.seal-start.dispatch "/seal-start"
hermes config set gateway.discord.commands.seal-progress.description "Check your security readiness"
hermes config set gateway.discord.commands.seal-progress.dispatch "/seal-progress"
hermes config set gateway.discord.commands.seal_911.description "Emergency security help — routes to official SEAL 911"
hermes config set gateway.discord.commands.seal_911.dispatch "/seal_911"
```

Or add to `~/.hermes/config.yaml` directly:

```yaml
gateway:
  discord:
    commands:
      - name: seal-start
        description: "Open SEAL Security Coach"
        dispatch: "/seal-start"
      - name: seal-progress
        description: "Check your security readiness"
        dispatch: "/seal-progress"
      - name: seal_911
        description: "Emergency security help — routes to official SEAL 911"
        dispatch: "/seal_911"
```

### 3. Set inference provider

For private inference (recommended for sensitive security data):

```bash
# Venice.ai (no data retention)
hermes config set provider.base_url "https://api.venice.ai/v1"
hermes config set provider.model "qwen3-5-35b-a3b"

# LM Studio (local, zero leakage)
hermes config set provider.base_url "http://localhost:1234/v1"
hermes config set provider.model "qwen/qwen3.5-32b"
```

### 4. Restart

```bash
hermes restart
```

### Verify

```bash
hermes chat --toolsets skills -q "What seal skills do you have?"
```

On Discord, type `/seal-start` in any channel. On Telegram, message the bot and say "help me with security."

## Usage

### Discord

- `/seal-start` — opens the coach menu with daily tip + options
- `/seal-progress` — guided readiness check (8-10 questions)
- `/seal_911` — emergency handoff to official SEAL 911 bot
- `@mention` — ask any security question

### Telegram / CLI

- Say "check my posture" or "start coaching"
- Ask any security question naturally
- "emergency help" routes to SEAL 911

### Mention-based Q&A

Ask security questions naturally. The agent matches your question to the right skill domain and answers using the SEAL frameworks.

```
> My wallet was drained, what do I do?
# Loads seal-incident-management + seal-wallet-security + seal-safe-harbor

> How do I set up multisig for our treasury?
# Loads seal-multisig-for-protocols + seal-treasury-operations

> We're hiring remote devs, any security concerns?
# Loads seal-dprk-it-workers + seal-opsec
```

## Structure

Each skill follows the [Agent Skills spec](https://agentskills.io) + Hermes conventions:

```
~/.hermes/skills/seal/
├── INDEX.md                         # MOC trigger table (read by agent on load)
├── SECURITY.md                      # Data privacy & inference provider guide
├── .baseline.json                   # Quality metrics for version tracking
├── .skill-writing-playbook.md       # Best practices for improving skills
├── .env.example                     # Inference provider config template
├── README.md
│
├── awareness/
│   ├── SKILL.md                     # Frontmatter + When to Use + Gotchas
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

Each skill has cross-domain triggers and gotchas:

```yaml
---
name: seal-incident-management
description: >
  Handle security incidents — compromised wallets, protocol hacks, suspicious
  transactions, drainer attacks, malware. Use when someone reports a breach,
  asks 'what do I do if my wallet was hacked', or needs IR playbooks.
  Load seal-safe-harbor if whitehat involvement is possible.
  Load seal-wallet-security if wallet-specific.
  Load seal-monitoring for detection setup.
  Load seal-dprk-it-workers if DPRK-related.
metadata:
  category: security
  tags: [incident-response, playbooks, detection, containment]
  related_skills: [seal-safe-harbor, seal-opsec, seal-wallet-security, seal-monitoring, seal-threat-modeling, seal-dprk-it-workers]
---

# Incident Management

## When to Use
- User reports a compromised wallet or protocol
- Suspicious transaction detected
- Need for IR playbook or escalation

## Key Concepts
[framework content — cleaned from security-alliance/frameworks]

## Gotchas
- Evidence must be preserved BEFORE remediation — screenshot transactions, save logs, document timeline first
- Communicating during an incident is legally risky — get legal review before any public statement
- Auto-pause mechanisms can be exploited to DoS your protocol — balance protection with availability
- The SEAL 911 war room exists specifically for coordinated response — use it rather than going solo

## References
- Playbooks (references/playbooks/)
- Communication Strategies
```

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

## Security & Privacy

See [SECURITY.md](SECURITY.md) for trust assumptions, inference provider tradeoffs, and deployment patterns.

**Key rule:** These skills handle sensitive organizational security data. Choose your inference provider carefully. See [SECURITY.md](SECURITY.md) for the full comparison.

## Versioning

Every change is measured against `.baseline.json`. Metrics tracked:

| Metric | v1.0 | v2.0 |
|---|---|---|
| Gotchas sections | 0/27 | 27/27 |
| Cross-domain triggers | 0/27 | 27/27 |
| Avg description length | 130 chars | 358 chars |
| Claude Code test avg | 4.75/5 | 4.85/5 |

## Source

- Frameworks: https://github.com/security-alliance/frameworks
- Skill standard: https://agentskills.io
- Hermes docs: https://hermes-agent.nousresearch.com/docs/developer-guide/creating-skills
- Best practices: See `.skill-writing-playbook.md`
- Data security: See `SECURITY.md`
