# Security Policy

Glyph Game Builder is an Agent Skill made of instructions and reference files. It is not itself a web service or a general-purpose runtime.

## Reporting a vulnerability

**Please do not disclose an unpatched, actionable vulnerability or a leaked credential in a public issue.**

If GitHub displays **Security → Report a vulnerability** for this repository, use that private reporting channel. Otherwise, reach out to the maintainer privately through a contact method made available on the repository owner's GitHub profile.

In a private report, include the affected file/version or commit, the impact, a minimal reproduction, and any relevant mitigation. Never send working credentials or personal data unless a secure private channel has been established.

## Relevant risks

Security-relevant findings may include:

- instructions that unexpectedly disclose files, prompts, or secrets;
- unsafe commands or destructive file changes the skill encourages without appropriate user approval;
- untrusted content being elevated to instructions by a consuming agent;
- example code or dependency advice that creates an avoidable security weakness.

Because the consuming agent and generated game live outside this repository, report vulnerabilities in those runtimes or projects to their respective maintainers as well when appropriate.

## Maintenance and disclosure

This repository has no published security support SLA or guaranteed response time. Supported versions and fix availability depend on maintainers' releases. Once a fix is available, maintainers may coordinate public disclosure through the repository.
