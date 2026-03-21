# SEAL Skills Drift Plan

Generated: 2026-03-21

## Current State

- **Local fork** (`madjin/frameworks` develop): `cf3da3e` (2025-12-08)
- **Upstream** (`security-alliance/frameworks` develop): `0314786` (latest)
- **Commits behind**: 41 commits to `docs/pages/`

## Drift Analysis by Priority

### HIGH - Substantive Content Changes (require skill updates)

| Area | Upstream PRs | What Changed |
|------|-------------|--------------|
| `incident-management` | #407, #376 | Incident response template integration; white hat frontrunning section in SEAL 911 war room guidelines |
| `safe-harbor` | #356 | Safe Harbor documentation clarity and accuracy update |
| `infrastructure` | #329, #314 | SMTP DANE section added to DNS security; DNSSEC and CAA clarifications |
| `community-management` | #305, #321 | W3OSC account configuration guides; Discord guide integration |
| `opsec` | #305 | W3OSC account configuration guides integration |
| `wallet-security` | #377 | Smart contract interaction security page added |
| `ai-security` | #397, #398 | **NEW DOMAIN** - AI Security first commit; DevSecOps sandboxing/isolation content moved here |

### MEDIUM - Structural/SEO Changes

| Area | What Changed |
|------|--------------|
| All areas | Meta descriptions added to every page (#324) |
| `opsec`, `community-management`, `devsecops` | Zoom hardening guide (#375) |
| `guides` | Account configuration guides, Zoom hardening |
| `multisig-for-protocols` | W3OSC multisig content integration (#303) |

### LOW - Cosmetic/Infra (no skill update needed)

| Area | What Changed |
|------|--------------|
| All areas | Spellchecker/linter fixes, index generator, tags, badges |
| All areas | Canonical tags (#383) |
| Config/deploy | Vercel to Cloudflare Pages migration (#395) |
| `certs` | Export All Certifications button, certification updates |
| Files | Rename `&` to `and` for URL compatibility (#372) |

## Unmapped Domains (18 paths with no skill coverage)

| Priority | Domain | Why |
|----------|--------|-----|
| **High** | `ai-security/` | New domain, high relevance to current landscape |
| Medium | `supply-chain/` | Growing attack vector |
| Medium | `vulnerability-disclosure/` | Core security practice |
| Medium | `threat-modeling/` | Foundational security methodology |
| Medium | `secure-software-development/` | SDLC security |
| Medium | `iam/` | Identity/access management |
| Low | `treasury-operations/` | Crypto-specific |
| Low | `multisig-for-protocols/` | Crypto-specific |
| Low | `encryption/` | General/overlaps other skills |
| Low | `privacy/` | General/overlaps other skills |
| Low | `monitoring/` | Operations-focused |
| Low | `front-end-web-app/` | Narrow scope |
| Low | `governance/` | Organizational |
| Low | `devsecops/` | Overlaps infrastructure |
| Low | `security-automation/` | Tooling-focused |
| Low | `user-team-security/` | HR/people-focused |
| Low | `ens/` | Crypto-niche |
| Low | `certs/` | Reference material |

## Action Plan

### Phase 1: Update existing skills (HIGH priority changes)

1. **incident-response-advisor** - Review #407 template integration and #376 frontrunning section
2. **safe-harbor-advisor** - Review #356 for clarity/accuracy updates
3. **infrastructure-security-advisor** - Review #329 (SMTP DANE) and #314 (DNSSEC/CAA)
4. **community-security-advisor** - Review #305/#321 W3OSC guides
5. **opsec-advisor** - Review #305 account configuration content
6. **wallet-security-advisor** - Review #377 smart contract interaction security

### Phase 2: New skill creation

1. **ai-security-advisor** - Create new skill from `ai-security/` domain content

### Phase 3: Evaluation for future skills

Review unmapped domains and decide which warrant skill creation based on user demand and overlap with existing skills.

### Phase 4: Merge upstream into fork

```bash
cd /home/jin/frameworks
git merge upstream/develop
```

### Phase 5: Update sync status

After completing updates, update `.sync-status` with new commit hash.

## Quick Reference Commands

```bash
# Check current drift
cd /home/jin/frameworks
git fetch upstream
git rev-list --count develop..upstream/develop -- docs/pages/

# See what changed for a specific skill
git log --oneline develop..upstream/develop -- docs/pages/incident-management/
git diff develop..upstream/develop -- docs/pages/incident-management/

# Preview upstream content for a specific area
git show upstream/develop:docs/pages/incident-management/index.mdx

# Merge upstream when ready
git merge upstream/develop
```
