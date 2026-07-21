# Use the Silicon Valley development team

The team is platform-neutral.

The canonical behaviour lives in Agent Skills under `skills/`:

- `silicon-valley-dev-team` — master orchestrator;
- `jared` — COO and delivery lead;
- `richard-hendricks` — technical founder and CTO;
- `dinesh` — VP Engineering and application-delivery lead;
- `gilfoyle` — VP Architecture and platform lead;
- `jian-yang` — read-only adversarial product and ecosystem reviewer.

Runtime-specific folders contain only discovery, subagent, permission, and concurrency adapters. They must not redefine the team.

## Portable architecture

```text
User
  -> parent agent or main conversation
      -> silicon-valley-dev-team master skill
          -> selected specialist skills or subagents
              -> one reconciled plan
              -> one primary editor per area
              -> independent review
              -> corrected and tested result
```

The user remains product owner and final decision-maker. The parent agent remains accountable engineering lead and integration owner.

## Capability levels

### 1. Agent Skills plus named subagents

This is the fullest experience.

- Install all six team skills.
- Install the runtime's five specialist subagent definitions.
- Load the master skill in the parent conversation.
- Let the master select only the specialists needed for the task.
- Keep Jian-Yang read-only.

Supported adapters in this repository:

- [Codex](CODEX_PERSONAL_DEV_TEAM.md)
- [Claude Code](CLAUDE_CODE.md)

### 2. Agent Skills without named subagents

Install all six team skills and invoke the master skill.

The parent agent applies selected specialist skills sequentially as independent lenses. It must not claim parallel agents ran. It still separates findings, reconciles one plan, uses one editor identity, reviews the result independently, and reports one coherent outcome.

### 3. No Agent Skills support

Use [`generic/AGENT_INSTRUCTIONS.md`](../generic/AGENT_INSTRUCTIONS.md) as the runtime adapter.

Give the runtime access to:

- `skills/silicon-valley-dev-team/SKILL.md`;
- only the selected specialist `SKILL.md` files.

Do not paste all six full skills into one permanent system prompt. Load detailed role instructions only when required.

## Installation source of truth

Clone or update the repository:

### PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
if (Test-Path (Join-Path $repo ".git")) {
    git -C $repo pull --ff-only
} else {
    git clone https://github.com/wilfgrainger/agent-skills.git $repo
}
```

### Bash, WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
if [ -d "$repo/.git" ]; then
  git -C "$repo" pull --ff-only
else
  git clone https://github.com/wilfgrainger/agent-skills.git "$repo"
fi
```

Then follow the adapter guide for the runtime you use.

## Invocation

Invoke the master skill for substantial team work:

```text
silicon-valley-dev-team deliver <customer outcome>
silicon-valley-dev-team review <repository, PR, product, or plan>
silicon-valley-dev-team architecture <decision>
silicon-valley-dev-team release <release>
silicon-valley-dev-team rescue <initiative>
```

The exact prefix depends on the runtime. Examples include `$silicon-valley-dev-team` in Codex and `/silicon-valley-dev-team` in Claude Code.

Natural language triggers also work when the runtime supports automatic skill discovery:

```text
Use the Silicon Valley dev team to deliver this feature.
Bring in the team for a full repository review.
Use Jian-Yang as the adversarial reviewer after implementation.
```

## Expected orchestration

The master skill must:

1. verify the outcome, state, constraints, and authority;
2. choose the smallest relevant specialist set;
3. name one accountable lead;
4. assign one primary editor per file or bounded area;
5. give reviewers distinct questions;
6. reconcile advice before editing;
7. implement the smallest complete result;
8. run decisive checks during the work;
9. review the actual diff and evidence;
10. correct validated findings and rerun checks;
11. return one coherent outcome.

It must not spawn every specialist merely because they exist.

## Portable role boundaries

| Role | Accountable for | Editing default |
|---|---|---|
| Jared | Customer outcome, business and product operations, commitments, ownership, sequence, launch, rescue | Operating and stakeholder documents only |
| Richard | Technical strategy, architecture, algorithms, performance, pivots, technology ethics | Read-only except narrow prototype or architecture record |
| Dinesh | Application code, APIs, UI, services, integrations, migrations, tests, developer experience | Primary editor for application work |
| Gilfoyle | Platform, infrastructure, networks, CI/CD, security, reliability, observability, capacity, incidents, recovery | Primary editor for platform work |
| Jian-Yang | Competitor, loophole, incentive, ownership, dependency, claim, copyability, and metric challenge | Always read-only |

Gilfoyle and Jian-Yang are complementary:

- Gilfoyle reviews technical attack, failure, platform, and recovery paths.
- Jian-Yang reviews self-interested participants, competitor behaviour, incentives, ownership, dependencies, public claims, and gaming.

## Adding another runtime

A new adapter should be thin.

It may define:

- where skills are installed;
- where project or personal instructions live;
- how named subagents are declared;
- how a specialist skill is preloaded;
- tool restrictions and read-only enforcement;
- concurrency or nesting limits;
- invocation syntax;
- restart or discovery behaviour.

It must not copy and fork the full role definitions. Reference the canonical skills instead.

Minimum adapter files:

```text
<runtime>/
  README or setup guide
  parent-instruction template
  specialist agent definitions, when supported
```

When the runtime cannot preload skills into subagents, keep each adapter prompt short and instruct the agent to load the matching canonical `SKILL.md` before working.

## Verification

After installation, ask the runtime:

```text
List the Silicon Valley development-team skills and specialist agents available to you. Explain who is allowed to edit application files, platform files, and who must remain read-only. Do not change files.
```

A correct response identifies:

- the master orchestrator;
- all five specialists;
- Dinesh as normal application editor;
- Gilfoyle as normal platform editor;
- Jian-Yang as always read-only;
- the parent conversation as accountable integration owner;
- task-shaped selection rather than automatic full-team fan-out.
