# FAQ

## Does the skill need to be manually activated every session?

Usually no. Once confirmed preferences are synced into the global config, new sessions can start with the important rules already loaded.

## Can multiple agent products share the same memory?

Yes. The runtime memory directory is `~/learn-from-experience/`, and the sync step can write the compiled `### Patterns` block into every detected supported product config.

## What should the skill learn from?

It should learn from:

- explicit user corrections
- confirmed long-term preferences
- reusable self-reflections from meaningful completed work

It should not learn from:

- silence
- one-off instructions
- hypothetical discussion
- hidden inference about personal traits

## Will the memory store grow forever?

No. The design uses HOT, WARM, and COLD tiers so the always-loaded set stays small. Less active patterns can be demoted or archived instead of polluting the default working context.

## Can I edit the memory files manually?

Yes. They are plain Markdown files by design. If you manually edit `memory.md`, run or request `sync memory` so the global config cache is refreshed.

## How do I remove everything?

To fully remove the skill state:

1. Delete `~/learn-from-experience/`
2. Remove the installed skill directory or symlink
3. Remove the `### Patterns` block under `## Learnings` from your global config if you no longer want the cached rules

## Why not store richer hidden metadata?

Because transparent and auditable behavior is a core design goal. If behavior changes because of learned information, that information should be visible and inspectable.
