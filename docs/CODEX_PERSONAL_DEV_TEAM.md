# Use the Silicon Valley skills as a Codex dev team

This setup gives Codex four spawnable specialist agents:

- **Jared** — delivery lead and product operations
- **Richard** — architecture and algorithms
- **Dinesh** — implementation and integration
- **Gilfoyle** — security, reliability, and adversarial review

The television programme supplies memorable names. The checked-in skills and agent profiles supply the professional behaviour. They do not impersonate the characters or reproduce dialogue.

## How the pieces fit

Codex uses three separate layers:

1. **Skills** describe the specialist methods. Codex discovers personal skills in `~/.agents/skills/`.
2. **Custom agents** make those specialists independently spawnable. Personal agent profiles live in `~/.codex/agents/`.
3. **AGENTS.md** tells the main Codex thread how to act as team lead and when to delegate.

Do not replace the skills with four long prompts. Skills use progressive loading: Codex initially sees their names and descriptions, then loads the full `SKILL.md` only when selected.

## Recommended client

The ChatGPT desktop app provides the clearest experience because it shows subagent threads and supports Git worktrees. Codex CLI and the IDE extension use the same skills, custom agents, and `AGENTS.md` setup.

For substantial work, use a worktree per task or branch. This lets the team work without disturbing your active checkout. Keep one primary editing agent per worktree.

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

First check whether you already have one:

### Windows PowerShell

```powershell
$globalAgents = Join-Path $HOME ".codex\AGENTS.md"
Test-Path $globalAgents
```

### WSL, Linux, or macOS

```bash
test -f "$HOME/.codex/AGENTS.md" && echo exists || echo missing
```

When the file is missing, copy the supplied template:

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

Codex defaults already permit direct subagents. The supplied configuration makes the intended team shape explicit: one lead plus four specialists, with no recursive fan-out.

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
List the custom agents available to you and summarize the personal development team instructions you loaded. Do not change files.
```

The response should identify `jared`, `richard_hendricks`, `dinesh`, and `gilfoyle`, and explain the plan → architecture → implementation → review flow.

In an interactive CLI session, use `/agent` to inspect or switch between running agent threads.

## 7. Use the team

### Full feature delivery

```text
Use my personal dev team for this task.

Goal: <customer outcome>
Constraints: <technical, legal, cost, deadline, or compatibility constraints>
Repository area: <known path or “inspect and determine it”>

Have Jared define the outcome, non-goals, ownership, sequence, risks, and next proof point. Have Richard inspect the relevant code and propose the smallest sound architecture. Reconcile both in the main thread, then have Dinesh implement the agreed vertical slice and run the decisive tests. Finally have Gilfoyle review the actual diff for correctness, security, reliability, operability, and recovery. Send validated findings back to Dinesh, rerun tests, and report the delivered outcome and residual risk.

Do not push, merge, deploy, delete, rotate secrets, or add paid services without my explicit approval.
```

### Bug investigation and fix

```text
Bring in the dev team to fix this bug: <symptom and reproduction>.

Use Richard only if the root cause involves architecture, data representation, concurrency, or performance. Have Dinesh reproduce and implement the smallest root-cause fix. Have Gilfoyle check sibling paths, failure modes, regressions, and recovery. Use Jared only when scope, ownership, release coordination, or customer communication is material. Run the smallest decisive test first, then the relevant broader checks.
```

### Architecture decision

```text
Use Richard and Gilfoyle as independent read-only reviewers of this proposal: <proposal>.

Richard should evaluate invariants, bottlenecks, representation, alternatives, measurable proof, and migration. Gilfoyle should evaluate trust boundaries, dependencies, failure domains, detection, rollback, and recovery. Have Jared synthesize the decision, trade-offs, owner, non-goals, and revisit trigger. Do not edit code.
```

### Release readiness

```text
Use Jared to lead release readiness for <release>. Have Dinesh verify build, tests, migrations, compatibility, and the complete user path. Have Gilfoyle verify security, observability, failure handling, rollback, restore, and incident ownership. Use Richard only for unresolved performance or architecture risks. Return a go, no-go, or go-with-conditions decision backed by evidence.
```

## 8. Steer the agents while they work

Use plain instructions in the main thread:

```text
Show me Gilfoyle's current findings.
Tell Richard to compare the conventional alternative as well.
Stop Jared; the product scope is already fixed.
Ask Dinesh to avoid editing the deployment files.
Close completed subagent threads after synthesizing them.
```

Do not run all four agents automatically for every task. Parallel agents use more tokens, and trivial work is usually faster and clearer with one agent.

## 9. Recommended working pattern

For each substantial change:

1. Start a new Codex chat in a worktree based on the intended branch.
2. Give the team one bounded customer outcome and explicit constraints.
3. Let Jared and Richard analyse in parallel where useful.
4. Require the main thread to choose one plan before editing.
5. Let Dinesh be the sole primary editor.
6. Let Gilfoyle review the resulting diff and test evidence.
7. Fix validated findings, rerun checks, and inspect the final diff yourself.
8. Create a branch and pull request only after the evidence is satisfactory.

This is a dev team, not four simultaneous typists. The value comes from specialist separation, controlled handoffs, one implementation owner, and one lead thread that remains accountable for the result.

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
