# Security Policy

Klar handles student accounts, passwords, session cookies and saved chat
history, so we take security reports seriously.

## Supported versions

Only the latest commit on `main` and the live site at
[klar.abdulrdeveloper.me](https://klar.abdulrdeveloper.me) are supported.
Fixes are not back-ported.

## Reporting a vulnerability

**Please do not open a public issue, discussion or pull request for security
problems.**

Report privately using GitHub's
[private vulnerability reporting](../../security/advisories/new)
(Security tab → *Report a vulnerability*) on this repository.

Please include:

- A description of the issue and its impact.
- Steps to reproduce, or a proof of concept.
- The affected route, file or commit if you know it.
- Any suggested fix.

## What to expect

- We aim to acknowledge your report within **3 business days**.
- We aim to share an assessment and plan within **10 business days**.
- We will keep you updated, and credit you in the fix unless you prefer to stay
  anonymous.

## Scope

In scope: this repository's application code, including registration, email
verification, login and password reset, JWT session handling, the dashboard
middleware, access checks on conversations and messages, rate limiting, and
prompt-injection issues that expose other users' data or the system prompt.

Out of scope: social engineering, denial-of-service by volume, issues in
third-party services (Neon, Upstash, Resend, Mistral, Groq, hosting providers),
AI answers that are simply wrong, and findings that require a compromised
device or an already-compromised account.

## Good-faith research

If you act in good faith, avoid accessing other users' data, and give us
reasonable time to fix the issue before disclosure, we will not pursue action
against you.

## For contributors

- Never commit secrets (`.env.local`, API keys, `JWT_SECRET`, database URLs).
- If you accidentally commit a secret, tell a maintainer immediately so it can
  be rotated. Removing it from a later commit does not make it safe.
