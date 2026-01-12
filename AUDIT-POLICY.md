# Security Audit Policy

This repository is a managed fork of [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) with automated security auditing.

## Why This Fork?

External prompt/skill files can contain hidden instructions that manipulate LLM behavior (prompt injection). This fork ensures all upstream changes are audited before integration into KRS systems.

## Automated Security Checks

Every upstream sync triggers these OWASP-based security scans:

| Check | Risk Level | What It Detects |
|-------|------------|-----------------|
| Control Characters | High | Hidden control characters (0x00-0x1F) |
| Zero-Width Unicode | High | Invisible Unicode (U+200B-200F, U+FEFF, etc.) |
| Prompt Injection Keywords | Critical | Keywords that alter LLM behavior |
| HTML/Script Injection | Medium | Embedded executable code |
| Persona Switch Patterns | High | Instructions to change AI role |

## Sync Process

1. **Weekly Sync**: GitHub Action runs every Monday at 6:00 UTC
2. **Automatic Audit**: All security checks must pass
3. **PR Created**: If audit passes, a PR is created for human review
4. **Manual Merge**: A KRS team member reviews and merges

## Manual Trigger

To manually trigger a sync:

1. Go to **Actions** tab
2. Select **Sync Upstream + Security Audit**
3. Click **Run workflow**

## Branch Strategy

- `main` - Original upstream content (synced from kepano)
- `progressive-disclosure` - Default branch with split skills (from PR #5)

## References

- [OWASP LLM Top 10 2025](https://genai.owasp.org/)
- [Promptfoo: Invisible Unicode Threats](https://www.promptfoo.dev/blog/invisible-unicode-threats/)
- [Original Repository](https://github.com/kepano/obsidian-skills)

## Initial Audit

This fork was created on 2026-01-12 after a comprehensive manual audit:
- All 9 skill files reviewed
- No security issues found
- Author verified: kepano = Steph Ango, CEO of Obsidian
