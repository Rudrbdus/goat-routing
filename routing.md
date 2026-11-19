# Model routing (goat plugin, global default)

This user's model routing rules, provided by the goat plugin:

- The rules below apply only when the project's CLAUDE.md has no `Model routing` section of its own. A project with its own section uses that instead.
- Route agents come from this plugin: `goat:quick` = sonnet·low (small, well-specified, 1–2 files), `goat:build` = opus·medium (normal feature or fix), `goat:deep` = opus·xhigh (architecture, migrations, auth, payments, data, unclear work), `goat:escalate` = fable·high (only after a failed check).
- A session whose prompt names it as a route worker (for example a herdr pane started as the `quick` worker) does the task itself and does not route it again.
1. Route choice: a ticket's `**Route:**` line sets the route. Any other coding task starts with the `goat:triage` agent. Non-coding questions are not routed.
2. The task goes to the route's agent with the full task and the triage JSON. No model or effort parameter is passed, because it would override the agent's own.
3. The `goat:verifier` agent then checks the change with the risk and checks from triage.
4. On FAIL there is one retry, one step up: a skipped file or tests not run → more effort (quick → build); full context and still wrong → bigger model (build → deep → escalate). A second FAIL stops the loop and the cause is reported to the user.
5. After any escalation, `goat:triage` saves one line to its memory: `<task pattern> → <route that worked>`.
- New tickets carry a `**Route:** quick|build|deep` line near the top.
- Superpowers skills keep their own Model Selection, review and fix-loop rules unchanged; their reviews take the place of `goat:verifier` and their task split takes the place of `goat:triage`. Their tiers map to models only: cheap = sonnet, standard = opus, most capable = fable. Effort is left unset, as superpowers leaves it.
- In a project with tests but no test gate (Stop hook), adding one is offered once, on the first coding task.
- `CLAUDE_CODE_EFFORT_LEVEL` stays unset: it would override the agents' own effort.
