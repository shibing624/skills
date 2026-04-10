# Quickstart Example

This example shows what a healthy first run should look like after installation.

## 1. Install the Skill

Use the instructions from [`docs/install.md`](../docs/install.md).

## 2. Ask the Agent to Initialize

```text
Please initialize the learn-from-experience skill.
```

## 3. Expected Runtime Tree

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

## 4. Example User Correction

```text
I prefer short answers with concrete next steps.
```

Expected effect:

- the correction is logged
- the agent treats it as a candidate pattern
- repeated confirmations can promote it into durable memory

## 5. Example Status Query

```text
memory stats
```

Example shape of the response:

```text
Learn-from-Experience Memory

HOT (always loaded):
  memory.md: 0 entries

WARM (load on demand):
  projects/: 0 files
  domains/: 0 files

COLD (archived):
  archive/: 0 files

Cross-session sync:
  Last sync: never
  Status: pending_first_sync
```
