# seal-skills

SEAL Security Knowledge Graph — 27 security domains from [security-alliance/frameworks](https://github.com/security-alliance/frameworks) packaged as AI agent skills following the [Agent Skills](https://agentskills.io) open standard.

## What is this?

A portable, dependency-free skill pack for AI agents (Hermes, Claude Code, etc.) that transforms the SEAL security frameworks into actionable, cross-referenced skills.

## Structure

```
~/.hermes/skills/seal/
├── INDEX.md                    # MOC trigger table — entry point
├── .baseline.json              # Quality metrics baseline (v1.0)
├── .skill-writing-playbook.md  # Best practices for writing skills
├── awareness/
│   ├── SKILL.md
│   └── references/
├── incident-management/
│   ├── SKILL.md
│   └── references/
│       └── playbooks/
├── ... (25 more domains)
└── wallet-security/
    ├── SKILL.md
    └── references/
```

## Domains (27)

| Domain | Focus |
|---|---|
| awareness | Threat recognition, phishing, security culture |
| certs | Certification frameworks |
| community-management | Discord/Telegram/social security |
| devsecops | Secure development pipelines |
| dprk-it-workers | DPRK worker infiltration detection |
| encryption | Encryption strategies |
| ens | ENS security |
| external-security-reviews | Audit management |
| front-end-web-app | Web/mobile security |
| governance | Compliance, risk, metrics |
| iam | Identity and access management |
| incident-management | Incident response, playbooks |
| infrastructure | OS, network, cloud security |
| monitoring | Alerting, thresholds |
| multisig-for-protocols | Multisig operations |
| opsec | Operational security |
| privacy | Privacy tools and practices |
| safe-harbor | Whitehat protection |
| secure-software-development | Secure coding |
| security-automation | Automated security |
| security-testing | Testing methodologies |
| supply-chain | Dependency security |
| threat-modeling | Threat modeling |
| treasury-operations | Treasury security |
| user-team-security | Team security training |
| vulnerability-disclosure | Responsible disclosure |
| wallet-security | Wallet types, seed phrases, multisig |

## Installation

```bash
# Copy to hermes skills directory
cp -r seal ~/.hermes/skills/seal

# Or clone directly
git clone https://github.com/clanktank/seal-skills.git ~/.hermes/skills/seal
```

## Usage

1. Agent reads `INDEX.md` to match user question → domain
2. `skill_view("seal-<domain>")` loads the skill
3. Follow `related_skills` in frontmatter for cross-references
4. `skill_view("seal-<domain>", "references/file.md")` for deeper content

## Versioning

Every improvement is measured against `.baseline.json`:
- v1.0: 27 skills, 212 reference files, 0 gotchas, 0 wikilinks, 203 avg words/skill

## Source

- Frameworks: https://github.com/security-alliance/frameworks
- Skill standard: https://agentskills.io
- Best practices: See `.skill-writing-playbook.md`
