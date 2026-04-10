# Security Policy

## Supported Releases

This repository is early-stage. Security-sensitive fixes should target the latest published version or the current default branch.

## Reporting a Vulnerability

Please do not open a public issue for:

- credential leakage risks
- hidden state or silent persistence bugs
- cross-session sync bugs that may overwrite unrelated config
- privacy violations involving stored user data

Instead, contact the maintainer privately first and include:

- affected agent product
- relevant install path
- relevant global config path
- minimal reproduction steps
- observed impact

## Project Security Principles

- transparent file-based state over hidden persistence
- explicit confirmation over inferred durable preference
- narrow sync scope over broad config mutation
- auditable memory over opaque behavior

## Out of Scope

The project should not be used to store:

- API keys
- passwords
- tokens
- health records
- financial identifiers
- third-party personal data

See `boundaries.md` for the operational safety rules.
