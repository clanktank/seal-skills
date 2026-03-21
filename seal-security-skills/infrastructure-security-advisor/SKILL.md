---
name: infrastructure-security-advisor
description: Provide guidance on securing Web3 infrastructure including DNS, domains, cloud services, email security, and DDoS protection. Use when users ask about domain hijacking, DNS security, DNSSEC, DANE, CAA records, DMARC, cloud configuration, zero-trust architecture, or protecting frontend applications. Triggers on questions about registrar security, CDN configuration, email authentication, or infrastructure attacks.
---

# Infrastructure Security Advisor

Guide Web3 projects on securing their infrastructure against common attack vectors.

## Critical Infrastructure Areas

### Priority Order (by attack frequency/impact)
1. **DNS/Domain Security** - Hijacking redirects users to phishing sites
2. **Cloud Access Controls** - Misconfigured IAM leads to breaches
3. **Email Security** - Spoofed emails enable social engineering
4. **DDoS Protection** - Availability attacks disrupt service
5. **Zero-Trust Architecture** - Reduces blast radius of compromises

## DNS & Domain Security (Highest Priority)

### DNSSEC - Foundation for Other Protocols
DNSSEC is a **prerequisite** for SMTP DANE, SSHFP records, and CAA records. Without it, these records can be spoofed.

Important nuance: Most client devices and recursive resolvers do NOT validate DNSSEC on general queries. It matters primarily for security-sensitive protocol features (DANE, SSHFP, CAA).

### Domain Hijacking Prevention
- **Registrar lock** enabled (prevents unauthorized transfers)
- **DNSSEC** configured
- **MFA on registrar account** (hardware key strongly recommended; TOTP acceptable; SMS forbidden)
- **Dedicated security contact email** on a separate domain (not a circular dependency — don't use an email on the domain you're protecting)
- **DNS monitoring** for unauthorized changes

### Registrar Account Security
1. Use strong, unique password
2. Enable MFA (hardware key > TOTP, SMS explicitly forbidden)
3. Limit account access to essential personnel
4. Use enterprise-grade registrar (MarkMonitor, AWS Route53, Cloudflare Registrar) — avoid consumer registrars like GoDaddy (cited security incidents)
5. Enable all EPP status codes:

| EPP Code | Effect |
|----------|--------|
| `clientTransferProhibited` | Blocks unauthorized transfers |
| `serverUpdateProhibited` | Registry-level update block |
| `serverDeleteProhibited` | Prevents domain deletion |
| `serverTransferProhibited` | Registry-level transfer block |

**Note**: EPP locks protect registry-level changes, NOT DNS zone edits at the provider.

### RDAP / WHOIS
- **RDAP** is the modern replacement for WHOIS: structured JSON, standardized format, RESTful APIs
- Use RDAP for security audits to verify EPP codes, nameservers, registrar info, expiration
- WHOIS privacy is available but has TLD-specific limitations (.us, .ca do not support it)

### Domain Expiration Protection
Expiration timeline (varies by TLD — gTLDs vs ccTLDs):
- **Day 0-30**: Grace period (renew at normal price)
- **Day 31-60**: Redemption period (higher fee to recover)
- **Day 61-80**: Pending delete (unrecoverable)
- **Day 81+**: Released to public

### DNS Provider Redundancy
Consider using multiple DNS providers:
- Primary: Cloudflare, AWS Route53, or similar
- Secondary: Different provider for redundancy
- Monitor both for consistency
- GitOps tools: OctoDNS, DNSControl for declarative zone management

### CAA Records (Certificate Authority Authorization)
CAA records specify which CAs can issue certificates for your domain.

- Well-behaved CAs not explicitly permitted via CAA will deny certificate requests
- Historical bypasses exist: DigiNotar (2011), Comodo (2011), Symantec Mis-Issuance (2015-2017)
- Use Common CA Database (ccadb.org) to find CA issuer domain names
- Child zones can override parent CAA records
- Advanced parameters: `accounturi` and `validationmethods` for finer control

### Monitoring and Alerting Framework

**Critical Priority Alerts** (immediate response):
- Registrar changes
- NS (nameserver) changes
- DNSSEC broken
- CAA records removed or overridden
- Unexpected TTL drops

**High Priority Alerts** (respond within hours):
- A/MX record changes
- DMARC policy weakening
- Unexpected certificate issuance (via CT log monitoring)

**Monitoring layers**:
- DNS record monitoring (continuous polling)
- Certificate Transparency (CT) log monitoring
- Passive DNS monitoring
- GitOps for zone management (OctoDNS, DNSControl)

**Incident response plan for DNS compromise**:
1. Detect via monitoring alert
2. Identify scope of unauthorized change
3. Revert changes at registrar/DNS provider
4. Rotate credentials on clean device
5. Investigate access logs
6. Notify affected users if phishing was deployed

## Email Security (SPF/DKIM/DMARC/DANE)

### SPF
Defines which servers can send email for your domain.
- Use `-all` (hard fail) not `~all` (soft fail)
- Keep under 10 DNS lookups

### DKIM
Cryptographic signing of outgoing email.
- Rotate keys annually
- Use 2048-bit minimum

### DMARC
Policy for handling SPF/DKIM failures.
- Without DMARC, providers like Gmail/Outlook may still deliver spoofed emails to inbox/spam with warning banners
- Enable **aggregate reporting** (`rua`) for visibility into who sends email on your behalf
- Forensic reporting (`ruf`) has privacy and reliability concerns — start with aggregate only
- Policy progression: `p=none` (monitor) -> `p=quarantine` -> `p=reject`

### SMTP DANE
Uses TLSA DNS records (secured via DNSSEC) to prevent MiTM and downgrade attacks on SMTP.

- Requires DNSSEC as prerequisite — without it, TLSA records can be spoofed
- TLSA record format: `_25._tcp.<mail-host>` with Usage/Selector/Match fields
- Industry support: Microsoft Exchange Online, Comcast, Protonmail, Cisco, Fastmail, Posteo, Mailbox.org
- Implementation: Exchange Online DANE docs, self-hosted Postfix tutorials

## Cloud Infrastructure

### IAM Best Practices
- Principle of least privilege
- No long-lived credentials where possible
- Service accounts for automation
- Regular access reviews
- MFA for all human users

### Key Security Configurations
- Enable CloudTrail/audit logging
- Use private subnets for sensitive services
- Implement network segmentation
- Encrypt data at rest and in transit
- Regular security group/firewall review

## DDoS Protection

### Essential Protections
- CDN in front of origin servers (Cloudflare, AWS CloudFront)
- Rate limiting on APIs
- Geographic restrictions if applicable
- Bot protection enabled
- Origin IP hidden behind CDN

### Attack Response
1. Activate "under attack" mode if available
2. Implement stricter rate limits
3. Block attacking IP ranges
4. Scale infrastructure if needed
5. Communicate with users about degraded service

## Zero-Trust Architecture

### Core Principles
- Never trust, always verify
- Assume breach mentality
- Least privilege access
- Micro-segmentation
- Continuous verification

### Implementation Priorities
1. Identity verification for all access
2. Device health verification
3. Network segmentation
4. Encrypted communications
5. Comprehensive logging

## Reference Files

- Upstream source: `security-alliance/frameworks` docs/pages/infrastructure/
- See `references/dns-checklist.md` for detailed DNS security configuration
- See `references/cloud-security.md` for cloud provider specific guidance
