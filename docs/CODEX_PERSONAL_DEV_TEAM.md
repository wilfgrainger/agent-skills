# Use the team with Codex

This is the Codex adapter for the platform-neutral [Silicon Valley development team](USING_THE_TEAM.md).

Codex uses:

- Agent Skills under `~/.agents/skills/`;
- custom-agent TOML files under `~/.codex/agents/`;
- `~/.codex/AGENTS.md` for parent-thread orchestration rules;
- bounded subagent concurrency in `~/.codex/config.toml`.

The canonical behaviour remains in the six team skills. The Codex files only adapt discovery, delegation, permissions, and concurrency.

## Team

- **Master:** `silicon-valley-dev-team`
- **Jared:** `jared`
- **Richard:** `richard_hendricks`
- **Dinesh:** `dinesh`
- **Gilfoyle:** `gilfoyle`
- **Jian-Yang:** `jian_yang`, always read-only

The user is product owner and final decision-maker. The parent Codex thread is accountable engineering lead and integration owner.

## 1. Clone or update the repository

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

## 2. Install the six skills

### PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
$skillsHome = Join-Path $HOME ".agents\skills"
$skills = @(
  "silicon-valley-dev-team",
  "jared",
  "richard-hendricks",
  "dinesh",
  "gilfoyle",
  "jian-yang"
)

New-Item -ItemType Directory -Force -Path $skillsHome | Out-Null

foreach ($skill in $skills) {
    $destination = Join-Path $skillsHome $skill
    if (Test-Path $destination) {
        Remove-Item $destination -Recurse -Force
    }
    Copy-Item (Join-Path $repo "skills\$skill") $destination -Recurse
}
```

### Bash, WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.agents/skills"

for skill in silicon-valley-dev-team jared richard-hendricks dinesh gilfoyle jian-yang; do
  ln -sfn "$repo/skills/$skill" "$HOME/.agents/skills/$skill"
done
```

Symlinks update immediately after `git pull`. Copied installations need the copy step repeated.

## 3. Install the five custom-agent profiles

### PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
$agentsHome = Join-Path $HOME ".codex\agents"
New-Item -ItemType Directory -Force -Path $agentsHome | Out-Null
Copy-Item (Join-Path $repo "codex\agents\*.toml") $agentsHome -Force
```

### Bash, WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.codex/agents"
cp "$repo"/codex/agents/*.toml "$HOME/.codex/agents/"
```

The profiles inherit the model and sandbox selected by the parent session. Jian-Yang's profile explicitly requires read-only work.

## 4. Add the parent-team instructions

Codex reads `~/.codex/AGENTS.md` before work in every repository.

When that file does not exist, copy the supplied adapter.

### PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
$codexHome = Join-Path $HOME ".codex"
New-Item -ItemType Directory -Force -Path $codexHome | Out-Null
Copy-Item (Join-Path $repo "codex\AGENTS.md") (Join-Path $codexHome "AGENTS.md")
```

### Bash, WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.codex"
cp "$repo/codex/AGENTS.md" "$HOME/.codex/AGENTS.md"
```

When `~/.codex/AGENTS.md` already exists, merge the adapter rather than overwriting deliberate personal rules. The key requirement is that “use the dev team” loads the `silicon-valley-dev-team` master skill and keeps the parent thread accountable.

Repository-level `AGENTS.md` files still apply and may provide more specific project instructions.

## 5. Configure bounded concurrency

Merge this into `~/.codex/config.toml`:

```toml
[agents]
max_threads = 6
max_depth = 1
interrupt_message = true
```

Six threads permit the parent plus five specialists. The master skill should still select only the specialists needed for each task. `max_depth = 1` prevents unmanaged recursive teams.

Do not blindly replace an existing `[agents]` section. Merge the keys.

## 6. Restart and verify

Restart Codex after installing new skills or custom agents.

Run `/skills` and confirm:

```text
silicon-valley-dev-team
jared
richard-hendricks
dinesh
gilfoyle
jian-yang
```

Then ask:

```text
List the Silicon Valley development-team skill and custom agents available to you. Explain who normally edits application files, who edits platform files, and who must remain read-only. Do not change files.
```

A correct response identifies:

- the master orchestrator;
- all five specialists;
- Dinesh as the normal application editor;
- Gilfoyle as the normal platform editor;
- Jian-Yang as always read-only;
- the parent thread as accountable integration owner.

## 7. Use the master skill

### Full delivery

```text
$silicon-valley-dev-team deliver

Goal: <customer outcome>
Constraints: <technical, legal, cost, timing, compatibility, privacy, or operational boundaries>
Repository area: <path or inspect and determine it>
Authority: <what may be edited, committed, pushed, merged, or deployed>
```

### Read-only review

```text
$silicon-valley-dev-team review <repository, PR, product, architecture, or plan>
```

### Architecture decision

```text
$silicon-valley-dev-team architecture <decision>
```

### Release readiness

```text
$silicon-valley-dev-team release <release>
```

### Project rescue

```text
$silicon-valley-dev-team rescue <initiative>
```

Natural language also works:

```text
Use the Silicon Valley dev team to deliver this feature.
Bring in the team for a complete repository review.
Use Jian-Yang as the final read-only adversarial reviewer.
```

## Expected Codex flow

For substantial work, the parent thread should:

1. load the master skill;
2. inspect the repository and authority;
3. select the smallest relevant specialist set;
4. run independent analysis in parallel only where useful;
5. reconcile one plan before editing;
6. assign one primary editor per file or bounded area;
7. run decisive checks during implementation;
8. review the actual diff and evidence;
9. correct validated findings and rerun checks;
10. return one coherent result.

Use worktrees for substantial isolated changes when available. Do not let multiple agents edit the same files concurrently.

## Direct specialist invocation

Invoke a specialist directly when the problem clearly fits one role:

```text
$richard-hendricks design <system>
$gilfoyle platform <infrastructure change>
$dinesh build <feature>
$jared launch <release>
$jian-yang red-team <product or plan>
```

Use the master skill when the work crosses roles or needs implementation plus independent review.

## Official Codex references

- [Build skills](https://learn.chatgpt.com/docs/build-skills)
- [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
- [Subagents and custom agents](https://learn.chatgpt.com/docs/agent-configuration/subagents)
- [Git worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees)
