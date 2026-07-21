# Use the Silicon Valley skills as a Codex dev team

This setup gives Codex four spawnable specialist agents:

- **Jared** — COO, business advisor, product operations, and delivery lead
- **Richard** — technical founder and CTO
- **Dinesh** — VP Engineering and application-delivery lead
- **Gilfoyle** — VP Architecture, platform, security, and reliability lead

The television programme supplies memorable names and broad role inspiration. The checked-in skills and agent profiles supply professional behaviour. They do not impersonate the characters, reproduce dialogue, or import their misconduct.

This is a serious development team. The humour budget is small; the evidence standard is not.

## How the pieces fit

Codex uses three separate layers:

1. **Skills** describe each specialist's operating method. Codex discovers personal skills in `~/.agents/skills/`.
2. **Custom agents** make those specialists independently spawnable. Personal agent profiles live in `~/.codex/agents/`.
3. **AGENTS.md** tells the parent Codex thread how to act as accountable engineering lead, select a task-shaped team, control editing, reconcile findings, and report evidence.

Do not replace the skills with four long prompts. Skills use progressive loading: Codex initially sees their names and descriptions, then loads the full `SKILL.md` only when selected.

The user remains product owner and final decision-maker. The parent Codex thread remains accountable for integration and truthfulness.

## Role model

| Specialist | Accountable for | Usually read-only when |
|---|---|---|
| Jared | Customer outcome, product and business operations, commitments, ownership, sequence, launch, stakeholder communication, project rescue | The task is purely technical and already bounded |
| Richard | Technical strategy, architecture, algorithms, performance, major pivots, product-platform coherence, technology ethics | The design is conventional and already decided |
| Dinesh | Application engineering, APIs, UI, services, integrations, migrations, code quality, tests, developer experience | Another specialist owns a bounded platform-only change |
| Gilfoyle | Platform, infrastructure, networks, CI/CD, security, reliability, observability, incidents, capacity, rollback, restore | The task has no material platform, security, or operational consequence |

One specialist is not permanently “above” the others. Leadership follows the work:

- Jared leads cross-functional operating and delivery problems.
- Richard leads technical-direction problems.
- Dinesh leads application-engineering delivery.
- Gilfoyle leads platform, security, reliability, and incident work.

The parent thread chooses the lead, enforces boundaries, and makes the final synthesis.

## Recommended client

The ChatGPT desktop app provides the clearest experience because it shows subagent threads and supports Git worktrees. Codex CLI and the IDE extension use the same skills, custom agents, and `AGENTS.md` setup.

For substantial work, use a worktree per task or branch. This lets the team work without disturbing your active checkout. Keep one primary editing agent per file or tightly bounded area.

## 1. Clone or update the skills repository

### Windows PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"

if (Test-Path $repo) {
    git -C $repo pull --ff-only
} else {
    git clone https://github.com/wilfgrainger/agent-skills.git $repo
}
```

### WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"

if [ -d "$repo/.git" ]; then
  git -C "$repo" pull --ff-only
else
  git clone https://github.com/wilfgrainger/agent-skills.git "$repo"
fi
```

## 2. Install the four skills globally

Global installation makes the skills available in every repository you open with Codex.

### Windows PowerShell

Copy the folders into your personal skills directory:

```powershell
$repo = Join-Path $HOME "agent-skills"
$skillsHome = Join-Path $HOME ".agents\skills"
$skills = @("richard-hendricks", "gilfoyle", "dinesh", "jared")

New-Item -ItemType Directory -Force -Path $skillsHome | Out-Null

foreach ($skill in $skills) {
    $destination = Join-Path $skillsHome $skill
    if (Test-Path $destination) {
        Remove-Item $destination -Recurse -Force
    }
    Copy-Item (Join-Path $repo "skills\$skill") $destination -Recurse
}
```

This deliberately replaces only those four skill folders. It does not touch any other installed skills.

### WSL, Linux, or macOS

Symlink the repository folders so a future `git pull` updates them in place:

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.agents/skills"

for skill in richard-hendricks gilfoyle dinesh jared; do
  ln -sfn "$repo/skills/$skill" "$HOME/.agents/skills/$skill"
done
```

Codex follows symlinked skill folders.

## 3. Install the custom agent profiles

### Windows PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
$agentsHome = Join-Path $HOME ".codex\agents"

New-Item -ItemType Directory -Force -Path $agentsHome | Out-Null
Copy-Item (Join-Path $repo "codex\agents\*.toml") $agentsHome -Force
```

### WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.codex/agents"
cp "$repo"/codex/agents/*.toml "$HOME/.codex/agents/"
```

Each TOML file defines one custom agent with a narrow description and developer instructions. Model and permission settings are intentionally omitted so the specialists inherit the model and sandbox selected by the parent Codex session.

## 4. Add the team-lead instructions

Codex reads `~/.codex/AGENTS.md` before work in every repository.

First check whether you already have one.

### Windows PowerShell

```powershell
$globalAgents = Join-Path $HOME ".codex\AGENTS.md"
Test-Path $globalAgents
```

### WSL, Linux, or macOS

```bash
test -f "$HOME/.codex/AGENTS.md" && echo exists || echo missing
```

When the file is missing, copy the supplied template.

### Windows PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
New-Item -ItemType Directory -Force -Path (Join-Path $HOME ".codex") | Out-Null
Copy-Item (Join-Path $repo "codex\AGENTS.md") (Join-Path $HOME ".codex\AGENTS.md")
```

### WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.codex"
cp "$repo/codex/AGENTS.md" "$HOME/.codex/AGENTS.md"
```

When `~/.codex/AGENTS.md` already exists, do not overwrite it. Append or merge the contents of `codex/AGENTS.md` beneath your existing global working agreements. Keep the combined file below Codex's instruction-size limit and remove conflicting rules.

Repository-level `AGENTS.md` files still apply. More specific instructions closer to the current working directory override broader global guidance.

## 5. Configure bounded subagent concurrency

Codex defaults already permit direct subagents. The supplied configuration makes the intended team shape explicit: one parent lead plus up to four specialists, with no recursive fan-out.

Merge this into `~/.codex/config.toml`:

```toml
[agents]
max_threads = 5
max_depth = 1
interrupt_message = true
```

Do not blindly replace an existing `[agents]` section. Merge the keys and keep any deliberate local settings.

## 6. Restart and verify

Restart the ChatGPT desktop app, Codex CLI session, or IDE extension after installation.

In Codex CLI:

```text
/skills
```

Confirm these four skills are present:

```text
richard-hendricks
gilfoyle
dinesh
jared
```

Then ask:

```text
List the custom agents available to you and summarise the personal development team instructions you loaded. Do not change files.
```

The response should identify `jared`, `richard_hendricks`, `dinesh`, and `gilfoyle`, explain their COO, CTO, VP Engineering, and VP Architecture responsibilities, and state that the parent thread selects one primary editor per area.

In an interactive CLI session, use `/agent` to inspect or switch between running agent threads.

## 7. Use the team

### Full feature delivery

```text
Use my personal dev team for this task.

Goal: <customer outcome>
Constraints: <technical, legal, cost, deadline, or compatibility constraints>
Repository area: <known path or “inspect and determine it”>

Treat me as product owner and the parent thread as accountable engineering lead.

Use Jared when customer outcome, commitments, scope, ownership, launch, or business operations need definition.
Use Richard for material technical direction, architecture, algorithms, performance, or technology-ethics decisions.
Assign Dinesh as primary editor for application, API, UI, integration, migration, and developer-experience work.
Assign Gilfoyle as primary editor for platform, infrastructure, deployment, security, observability, or recovery work.
Use one primary editor per file or bounded area.

Have independent specialists review the actual diff and evidence. Send validated findings to the primary editor, rerun decisive checks, and report the delivered outcome, proof, decisions, and residual risk.

Do not push, merge, deploy, delete, rotate secrets, create standing automation, add paid services, or spend money without my explicit approval.
```

### Bug investigation and fix

```text
Bring in the dev team to fix this bug: <symptom and reproduction>.

Have Dinesh reproduce the real user or caller failure and implement the smallest root-cause application fix.
Have Gilfoyle lead instead when the defect is primarily infrastructure, deployment, network, identity, capacity, security, or recovery.
Use Richard only when the root cause involves architecture, data representation, concurrency, performance, or a technical promise.
Use Jared only when scope, ownership, customer impact, release coordination, or communication is material.

Run the smallest decisive reproduction first, then relevant broader checks. Review sibling paths and report what was not tested.
```

### Infrastructure or security change

```text
Use Gilfoyle to lead this infrastructure or security task: <task>.

Have Gilfoyle inspect the real configuration and runtime path, define assets and promises, map trust and failure boundaries, and implement the smallest bounded platform change.
Have Dinesh review integration contracts, local developer usability, compatibility, and the application impact.
Use Richard for material architecture, protocol, scaling, or build-versus-buy decisions.
Use Jared for cost approval, vendor commitments, rollout ownership, customer communication, or launch coordination.

Require rollback, restore, observability, capacity, cost, and runnable proof. Do not treat a successful deployment as proof of recovery.
```

### Architecture decision

```text
Use Richard and Gilfoyle as independent read-only reviewers of this proposal: <proposal>.

Richard should evaluate the product promise, invariants, representation, algorithms, conventional alternatives, measurable proof, migration, and technology-ethics boundary.
Gilfoyle should evaluate trust boundaries, dependencies, platform fit, failure domains, capacity, detection, rollback, restore, and recovery.
Have Dinesh evaluate implementation and migration practicality.
Have Jared capture the decision, commitments, owner, non-goals, commercial constraints, and revisit trigger.

Do not edit code.
```

### Release readiness

```text
Use Jared to lead release readiness for <release>.

Have Jared verify customer value, commitments, owners, communications, support, governance coordination, success gates, and stop conditions.
Have Dinesh verify build, tests, migrations, compatibility, accessibility, and the complete user path.
Have Gilfoyle verify security, observability, capacity, failure handling, rollback, restore, incident ownership, and production-operating evidence.
Use Richard for unresolved architecture, performance, data-use, or technology-ethics risks.

Return a go, no-go, or go-with-conditions decision backed by evidence.
```

### Project rescue

```text
Use Jared to lead a rescue of this initiative: <context>.

Stop starting new work. Reconstruct the customer outcome, current commitments, owners, actual repository and production state, constraints, and the next proof point.
Have Richard identify unresolved technical-direction decisions.
Have Dinesh identify incomplete product paths, implementation debt, and test reality.
Have Gilfoyle identify platform, security, reliability, deployment, and recovery risks.

Cancel, defer, or narrow work that is not required for the next valuable outcome. Publish a truthful recovery plan with named owners and a near-term proof point.
```

## 8. Select the primary editor

Do not default mechanically to Dinesh for every task.

| Change type | Primary editor | Independent review |
|---|---|---|
| Product UI, API, service, integration, migration | Dinesh | Gilfoyle for failure and security; Richard for architecture |
| Infrastructure, network, deployment, CI/CD, observability, security | Gilfoyle | Dinesh for integration and usability; Richard for architecture |
| Narrow algorithmic prototype | Richard | Dinesh for maintainability; Gilfoyle for operational risk |
| Planning, launch, operating, customer, stakeholder document | Jared | Relevant technical specialist for factual accuracy |

Two editors may work in parallel only on explicitly non-overlapping files with a clear integration owner and stable contract. Stop parallelism when it creates merge risk or duplicated reasoning.

## 9. Steer the agents while they work

Use plain instructions in the parent thread:

```text
Show me Gilfoyle's current findings.
Tell Richard to compare the conventional alternative and state the ethical stop condition.
Ask Jared to list external commitments and identify any that lack an owner.
Ask Dinesh to keep one integration owner and avoid editing deployment files.
Make Gilfoyle the primary editor because this is a platform task.
Stop Jared; the outcome and operating plan are already fixed.
Close completed subagent threads after synthesising them.
```

Do not run all four agents automatically for every task. Parallel agents use more tokens, and trivial work is usually faster and clearer with one accountable specialist.

## 10. Recommended working pattern

For each substantial change:

1. Start a new Codex chat in a worktree based on the intended branch.
2. Give the team one bounded customer outcome and explicit constraints.
3. Select only the specialists whose roles materially improve the work.
4. Let independent analysis run in parallel where useful.
5. Require the parent thread to choose one plan before editing.
6. Choose one primary editor per file or bounded area.
7. Integrate early and run the smallest decisive checks.
8. Ask independent specialists to review the actual diff and evidence.
9. Fix validated findings and rerun checks.
10. Inspect the final diff yourself.
11. Create a branch and pull request only after the evidence is satisfactory.

This is a development team, not four simultaneous typists and not a comedy role-play. The value comes from broad but bounded roles, task-shaped leadership, controlled handoffs, one integration owner, and a parent thread that remains accountable for the result.

## Humour rules

A small amount of original character flavour is allowed when it helps the user follow the team:

- one brief aside at most in an ordinary progress update;
- no quotations or close imitation of programme dialogue;
- no insults, humiliation, threats, or jokes about a person;
- no humour during incidents, safety issues, legal or personnel matters, or serious customer harm;
- no joke may replace an action, decision, test, caveat, or piece of evidence.

Omit humour whenever it makes the work less clear or trustworthy.

## Updating the team

### Windows PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
git -C $repo pull --ff-only
# Repeat steps 2 and 3 to refresh copied skills and agent profiles.
```

### WSL, Linux, or macOS

```bash
git -C "$HOME/agent-skills" pull --ff-only
# Symlinked skills update immediately. Re-copy codex/agents/*.toml if profiles changed.
```

Restart Codex when updated files do not appear immediately.

## Official Codex references

- [Build skills](https://learn.chatgpt.com/docs/build-skills)
- [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
- [Subagents and custom agents](https://learn.chatgpt.com/docs/agent-configuration/subagents)
- [Git worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees)
