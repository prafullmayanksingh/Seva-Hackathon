# Contributing to GVP-Guard: NightEye AI

Thank you for your interest in contributing! GVP-Guard is a human-reviewed illegal-dumping incident and evidence platform, currently a proof of concept. Contributions that make it safer, clearer and more reliable are welcome.

By participating, you agree to follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Guiding Principles

Every contribution must respect the project's core rules:

1. **Human in the loop.** The system never automatically accuses, fines or declares guilt. Officer approval is required before action.
2. **Stop time is a trigger, not proof.** Event detection must combine multiple cues.
3. **Never invent data.** If a plate is unreadable, the system must say so, never guess a registration number.
4. **Show uncertainty.** Confidence and ambiguity must be visible to the officer.
5. **Honest claims.** Do not add accuracy or impact numbers unless they come from documented tests. Targets must be labelled as targets.
6. **Privacy first.** No real CCTV footage, number plates or personal data in the repository.

## Ways to Contribute

- Report bugs or false-alert scenarios
- Improve vehicle tracking, event cues or night ANPR
- Add controlled test scenarios and evaluation scripts
- Improve the officer dashboard and UX
- Improve documentation and translations (English, Hindi, Gujarati)
- Review privacy, security and responsible-use aspects

## Getting Started

1. **Fork** the repository and clone your fork.
2. Create a branch from `main`:
   ```bash
   git checkout -b feature/short-description
   ```
3. Make your changes with clear, focused commits.
4. Test your changes (see below).
5. Push and open a **Pull Request**.

## Branch and Commit Style

- Branch names: `feature/...`, `fix/...`, `docs/...`, `test/...`
- Commit messages: short imperative summary, e.g. `Add best-frame scoring for plate crops`
- Keep pull requests small and focused on one change.

## Coding Guidelines

- **Python:** follow PEP 8; use type hints where practical; format with `black`.
- **JavaScript/TypeScript:** use ESLint and Prettier defaults.
- Write clear comments for detection thresholds and any magic numbers.
- Make thresholds (stop time, zone, confidence) **configurable**, not hard-coded.
- Document new dependencies and why they are needed.

## Testing

- Add or update tests for behaviour you change.
- Include **negative cases**: vehicle stops without depositing, waste already present, legal delivery outside the zone, object removed before the scene stabilises.
- Test poor lighting, glare and unreadable plates where relevant.
- Report the exact hardware used if you share performance numbers.

## Data and Footage Rules

- Use only **controlled recordings** from permitted locations, or **legally usable public footage**.
- **Never commit** real footage, evidence frames, plate images or personal data. These are covered by `.gitignore`.
- Do not use footage of identifiable people or vehicles without clear permission.
- Gandhidham-specific tuning requires GMC-approved footage.

## Pull Request Checklist

- [ ] Change is focused and described clearly
- [ ] Tests added or updated, including negative cases
- [ ] No secrets, footage or personal data included
- [ ] No unsupported accuracy claims added
- [ ] Documentation updated if behaviour changed
- [ ] Terminology follows the project (see below)

## Preferred Terminology

| Use | Avoid |
|---|---|
| Review-ready evidence package | Legally admissible evidence |
| Structured incident record | Proof of guilt |
| Officer-approved action | Automatic fine |
| Pilot target | Guaranteed result |
| GVP priority score | Accurate future-event prediction |

## Reporting Issues

Open a GitHub Issue with: what you expected, what happened, steps to reproduce, and screenshots (with any personal data removed). For security problems, **do not open a public issue**; see [SECURITY.md](SECURITY.md).

## Questions

Open a discussion or issue, or contact the project lead, Omkar Solat.
