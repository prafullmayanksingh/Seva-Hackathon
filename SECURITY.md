# Security Policy

GVP-Guard: NightEye AI handles video footage, vehicle information and incident records, so security and privacy are taken seriously.

## Project Status

The project is currently a **browser-based proof of concept** using controlled recorded footage. It is **not production-ready** and should not be deployed with real CCTV data or official municipal workflows without a proper security review.

## Supported Versions

| Version | Supported |
|---|---|
| `main` (latest prototype) | ✅ |
| Older commits / forks | ❌ |

## Reporting a Vulnerability

**Please do not open a public GitHub issue for security problems.**

Report privately by either:

- Using GitHub's **"Report a vulnerability"** option under the repository's *Security* tab, or
- Emailing **`<your-security-email@example.com>`** *(replace with your team's contact email)*

Please include:

- A description of the issue and its potential impact
- Steps to reproduce
- Affected files, components or versions
- Suggested fix, if any
- **No real footage or personal data**; use synthetic or sample data only

### What to Expect

| Step | Target time |
|---|---|
| Acknowledgement of report | within 5 working days |
| Initial assessment | within 10 working days |
| Fix or mitigation plan | depends on severity |

We will keep you informed and credit you in the fix notes if you wish.

## Scope

**In scope:**

- Authentication, authorisation and role-based access flaws
- Exposure of evidence, plates or incident data
- Insecure storage or transmission of footage
- Injection, XSS, CSRF and similar web vulnerabilities
- Dependency vulnerabilities with a real exploit path
- Tampering with audit logs or officer decisions

**Out of scope:**

- Accuracy limits of detection or OCR (report these as normal issues)
- Attacks requiring physical access to a user's device
- Social engineering and denial-of-service testing
- Vulnerabilities in third-party services (report to the vendor)

## Security and Privacy Safeguards (Design Goals)

- Human approval before any enforcement action
- Role-based access in a production dashboard
- Audit log of decisions and status changes
- Policy-approved evidence-retention period
- Upload only triggered clips where practical
- Official permission before any registry or e-challan integration

## Guidance for Contributors and Users

- **Never commit** secrets, API keys, `.env` files, footage, plate images or personal data.
- Use environment variables for credentials (e.g. Supabase keys); provide `.env.example` only.
- Use synthetic or controlled, permitted recordings for development.
- Keep dependencies updated and review them before adding.
- Rotate any key that is accidentally exposed immediately.

## Responsible Disclosure

We ask researchers to give us reasonable time to fix issues before public disclosure, and to avoid accessing, modifying or deleting data that is not their own. Good-faith research following this policy will not be pursued.
