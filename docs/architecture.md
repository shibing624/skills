# Architecture

`learn-from-experience` is a file-first memory system for coding agents. It favors explicit corrections, transparent storage, and conservative promotion rules over silent inference.

## Runtime Data Layout

At runtime, the skill maintains state in:

```text
~/learn-from-experience/
├── memory.md
├── index.md
├── corrections.md
├── heartbeat-state.md
├── projects/
├── domains/
└── archive/
```

## Tier Model

### HOT

- File: `memory.md`
- Purpose: highest-value durable preferences
- Loaded frequently
- Should stay small and high-signal

### WARM

- Files: `projects/*.md`, `domains/*.md`
- Purpose: scoped lessons that apply only to a project or domain
- Loaded on demand
- Used to prevent global memory from becoming noisy

### COLD

- Files: `archive/*.md`
- Purpose: preserve history without keeping it active
- Loaded only for explicit queries or audits

## Learning Pipeline

```text
explicit correction or self-reflection
        |
        v
  corrections.md
        |
 repeated pattern + confirmation
        |
        v
   memory.md / scoped namespace
        |
 compile confirmed preferences
        |
        v
global config: ## Learnings > ### Patterns
```

## Cross-Session Sync

The sync model is intentionally one-way:

- `memory.md` is the source of truth
- the agent global config is a read-only cache
- only the `### Patterns` block under `## Learnings` should be modified

This makes recovery simple: if sync fails or a global config is edited incorrectly, the skill rebuilds from `memory.md`.

## Safety Invariants

- Never learn from silence
- Never store credentials or sensitive personal data
- Never hide behavior-changing state outside the visible file model
- Never let global config become the canonical memory source

## Heartbeat Role

Heartbeat is deliberately conservative. Its job is to keep the memory system tidy and trustworthy, not to rewrite user intent.

Typical heartbeat actions:

- refresh `index.md`
- compact repetitive entries
- move clearly misplaced notes when the target is unambiguous
- check whether sync has gone stale

Typical non-actions:

- deleting uncertain content
- inferring new rules
- reorganizing unrelated files
