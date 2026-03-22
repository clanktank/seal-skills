# SEAL Security Coach

**An AI-powered security coach that helps open source projects and DAOs harden their security posture using the Security Alliance (SEAL) Frameworks.**

*Synthesis Hackathon Submission*

---

## The Problem

Open source projects and DAOs handle real value — treasury funds, smart contracts, user data, production infrastructure. But most operate without security expertise:

- **Can't afford consultants.** Professional security assessments cost $10K-$50K+. Open source projects run on grants and donations.
- **Frameworks are static docs.** SEAL publishes 27 security domains with 213+ controls. That's comprehensive, but nobody reads a 200-page framework and knows where to start.
- **Security is reactive.** Teams only care about security after they get drained. By then it's too late.

## The Solution

A conversational security coach that turns the SEAL Frameworks into an interactive assessment and improvement plan.

**What makes it different:**

| Generic AI Security Advice | SEAL Coach |
|---|---|
| "Enable MFA" (no context) | "Your multisig uses 2-of-3, but two signers share a laptop — if it's compromised, attacker has 2 of 3 keys. Move one signer to a hardware wallet." |
| One-size-fits-all list | Adapts to your team size, role, tech stack, and urgency level |
| No memory between sessions | Tracks readiness bands, completed actions, and avoids repeating tips |
| No domain expertise | Maps every recommendation to specific SEAL framework controls |

## How It Works

### Three Entry Points

**1. "I'm worried we're going to get hacked"** (Urgency)
- Triage in 2 exchanges: wallet vs infrastructure concern
- 3-5 targeted questions focused on "can an attacker exploit this TODAY?"
- Immediate actions before a full assessment
- Then broadens to full readiness check

**2. "Check our security posture"** (Assessment)
- Pre-assessment: org type, role, team size, past incidents
- Quick scan: 5 questions mapping to priority domains
- Domain deep-dive: 3-4 targeted questions per area
- Readiness bands: Critical -> Developing -> Established -> Advanced

**3. "Give me a security tip"** (Daily)
- Rotates across all 27 SEAL domains
- Tracks delivered tips to avoid repeats
- Links each tip to specific framework controls

### From Assessment to Action

After assessment, the coach generates a phased hardening plan:

```
Phase 1: Quick Wins (Week 1-2)
  - Split multisig keys across hardware wallets
  - Enable MFA on all admin accounts
  - Save SEAL 911 emergency contact

Phase 2: Foundation (Week 3-6)
  - Write incident response playbook
  - Add semgrep to CI/CD pipeline
  - Set up transaction monitoring alerts

Phase 3: Strengthen (Week 7-12)
  - Formal threat model
  - Automated compliance checks
  - Tabletop incident exercises
```

Every action maps to specific SEAL framework controls — no vague advice like "improve your security posture."

### Memory Across Sessions

The coach remembers:
- Your readiness bands per domain
- Completed improvement actions
- Tips already delivered
- Current focus area

When you come back, it picks up where you left off. "Last time we identified incident-management as Critical. Want to pick up there?"

## Architecture

```
seal-coach/
├── SKILL.md                    # Core coaching logic, triggers, urgency flow
├── references/
│   ├── assessment.md           # Flexible assessment questions + readiness bands
│   ├── gotchas.md              # Common coaching failures & how to avoid them
│   ├── plans/
│   │   └── hardening-template.md  # Actionable plans by readiness band
│   └── tips/
│       └── security-tips.md    # Rotating tips across 27 domains
├── scripts/
│   └── score_assessment.py     # Scorer: maps answers to readiness bands
└── templates/
    └── state-log.json          # Per-user progress tracking
```

**Built on:**
- [SEAL Security Alliance Frameworks](https://github.com/security-alliance/frameworks) — 27 domains, 213+ controls
- [Hermes Agent](https://github.com/m3-org/hermes-agent) — autonomous agent platform with memory, tool use, and multi-platform delivery
- Skill-based architecture — the coach is a portable skill that works with any agent platform supporting the skills spec

## Privacy

- **Zero data retention.** No conversation logs stored server-side.
- **Local-first.** Assessment state stored in local JSON, not cloud.
- **No PII collection.** The coach asks about your security setup, not your identity.

## Demo

*[Recording coming — shows the urgency flow: worried about drainage -> rapid triage -> immediate actions -> full assessment -> hardening plan]*

## Try It

```bash
# With Hermes Agent
hermes skills install seal-coach
hermes

# Or install manually:
# Copy the seal-coach directory into your agent's skills folder
```

## Built For

The [Synthesis Hackathon](https://synthesis.devfolio.co/) — Open source sustainability and agent-DAO problem spaces.

**Team:** jin, cyberWarlock, emotionull, peepo
