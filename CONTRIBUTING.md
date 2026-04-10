# Contributing

Thanks for your interest in improving `learn-from-experience`.

## Project Shape

This repository is also the installable skill directory.

- Keep install-critical files at the repository root, including `SKILL.md`, `setup.md`, `operations.md`, `learning.md`, `scaling.md`, and `boundaries.md`
- Put explanatory material in `docs/`
- Put runnable or walkthrough-style examples in `examples/`
- Avoid adding tool-specific glue that breaks the agent-agnostic contract unless it is clearly scoped and documented

## What Good Contributions Look Like

- Clarify installation or setup behavior for a supported platform
- Improve memory safety, transparency, or auditability
- Tighten the sync protocol or runtime invariants without adding hidden state
- Add examples that make real usage easier to understand
- Fix contradictions between `README.md`, `SKILL.md`, and the operational docs

## Before Opening a Pull Request

1. Read the relevant docs before changing behavior: `SKILL.md`, `setup.md`, `operations.md`, and `boundaries.md`
2. Keep terminology consistent across public docs
3. Update `README.md` and `docs/` when behavior changes
4. Avoid placeholder text like `TODO` or vague promises
5. Never include credentials, tokens, or real personal data in examples

## Pull Request Checklist

- The root install flow still makes sense
- Any platform-specific path changes are reflected everywhere they are documented
- Safety boundaries remain explicit
- New examples use synthetic data only
- Documentation links stay valid

## Reporting Bugs

When possible, include:

- the agent product you used
- the install path
- the global config path involved
- the exact user prompt or correction that should have triggered learning
- the observed result versus the expected result

## Scope Discipline

Please do not turn this project into a generic memory store or a hidden telemetry layer.

`learn-from-experience` is intentionally narrow:

- explicit corrections over silent inference
- transparent files over opaque state
- durable execution quality over broad personal profiling
