# goat-routing

Model routing for Claude Code, based on the "GOAT router" pattern: rules by task type and risk, fixed model + effort per route, a verifier, and one-step escalation on failure.

## Install

```
/plugin marketplace add Rudrbdus/goat-routing
/plugin install goat@goat-routing
```

## What it adds

- Agents: `goat:triage`, `goat:quick` (sonnet·low), `goat:build` (opus·medium), `goat:deep` (opus·xhigh), `goat:escalate` (fable·high), `goat:verifier`.
- A SessionStart hook that loads `routing.md` (the routing rules) into every session. Your CLAUDE.md is not modified.
- Projects whose CLAUDE.md has its own `Model routing` section keep their own rules.
