# metaprompt

A planning skill for coding agents (Claude Code, and any agent that loads Markdown skills). It turns a one-line ask — "fix this crash", "should we switch databases", "build me an app" — into a complete, executable, evidence-tagged plan through a short sharp-question interview, then stops. The plan is the deliverable: whoever builds from it has no memory of the conversation.

## The idea

**Dry-Run Interview.** The agent rehearses building the thing station by station and asks a question only where the rehearsal stalls on a fork that's expensive to get wrong. Everything else is looked up or defaulted-and-tagged, never guessed silently.

- **Look or ask.** Every fact is looked up (via a tool or an artifact you provided) before it's asked. Questions are reserved for intent, constraints, taste, and access — things nothing can look up.
- **Evidence discipline.** Every factual claim carries one of three tags: `(user)`, `(verified: <source>)`, or `[assumed: default X — if wrong: Y]`. An untagged claim of fact is a bug. Training-memory is never a valid source.
- **Ask as many questions as accuracy needs.** No hard cap — length is governed by open forks, not a counter. But the floor is just as hard: never ask a question that doesn't change the plan.
- **Questions as popups.** Each question is delivered one at a time as a structured choice, recommended answer first, with re-rehearsal after every answer.
- **Ten track playbooks.** Bug fix, feature, from-scratch, refactor, integration, performance, migration, UI build, tech decision, quick task — each adds decisive slots and phase invariants.
- **Landmine hunting.** The highest-value output is the constraint that invalidates the obvious approach ("the factory floor has no internet"). Destructive steps earn an explicit confirmation plus a rollback path.

The output is a self-contained Markdown plan: classification, goal & success criteria, scope, requirements, key decisions, an assumptions ledger, verification steps, and numbered build phases with done-checks.

## Use

Drop `SKILL.md` into your agent's skills directory (for Claude Code: `~/.claude/skills/metaprompt/SKILL.md`). Trigger it with `/metaprompt` or by asking to plan with the dry-run interview; the accompanying message is the opening ask.

## License

MIT
