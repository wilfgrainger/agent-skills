# Use the team with Claude Code

Claude Code supports the same Agent Skills format used by this repository, project or personal `CLAUDE.md` instructions, and Markdown custom subagents. The adapter under `claude-code/` keeps the portable team model intact while using Claude Code's native discovery paths.

Official references:

- [Skills](https://code.claude.com/docs/en/skills)
- [Custom subagents](https://code.claude.com/docs/en/sub-agents)
- [CLAUDE.md memory](https://code.claude.com/docs/en/memory)

## What gets installed

```text
~/.claude/skills/
  silicon-valley-dev-team/
  jared/
  richard-hendricks/
  dinesh/
  gilfoyle/
  jian-yang/

~/.claude/agents/
  jared.md
  richard-hendricks.md
  dinesh.md
  gilfoyle.md
  jian-yang.md

~/.claude/CLAUDE.md
  imports or includes the parent-team adapter
```

The skill files are canonical. The agent files preload their matching skills. `claude-code/CLAUDE.md` tells the main conversation to load the master skill and remain accountable for orchestration.

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

## 2. Install the skills

Claude Code discovers personal skills under `~/.claude/skills/<skill-name>/SKILL.md`.

### PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
$skillsHome = Join-Path $HOME ".claude\skills"
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

Symlink the skills so `git pull` updates them immediately:

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.claude/skills"

for skill in silicon-valley-dev-team jared richard-hendricks dinesh gilfoyle jian-yang; do
  ln -sfn "$repo/skills/$skill" "$HOME/.claude/skills/$skill"
done
```

## 3. Install the custom subagents

Claude Code discovers personal custom agents under `~/.claude/agents/`.

### PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
$agentsHome = Join-Path $HOME ".claude\agents"
New-Item -ItemType Directory -Force -Path $agentsHome | Out-Null
Copy-Item (Join-Path $repo "claude-code\agents\*.md") $agentsHome -Force
```

### Bash, WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.claude/agents"
cp "$repo"/claude-code/agents/*.md "$HOME/.claude/agents/"
```

The specialist files use Claude Code's `skills` frontmatter field to preload the canonical skill. Jian-Yang is restricted to read and search tools.

## 4. Add the parent-team instructions

Claude Code loads `~/.claude/CLAUDE.md` for all projects.

Do not overwrite existing personal instructions. Import the adapter instead.

### PowerShell

```powershell
$repo = Join-Path $HOME "agent-skills"
$claudeHome = Join-Path $HOME ".claude"
$claudeFile = Join-Path $claudeHome "CLAUDE.md"
$adapter = (Join-Path $repo "claude-code\CLAUDE.md") -replace '\\','/'

New-Item -ItemType Directory -Force -Path $claudeHome | Out-Null
if (-not (Test-Path $claudeFile)) {
    New-Item -ItemType File -Path $claudeFile | Out-Null
}

$import = "@${adapter}"
if (-not (Select-String -Path $claudeFile -SimpleMatch $import -Quiet)) {
    Add-Content -Path $claudeFile -Value "`n$import`n"
}
```

### Bash, WSL, Linux, or macOS

```bash
repo="$HOME/agent-skills"
mkdir -p "$HOME/.claude"
touch "$HOME/.claude/CLAUDE.md"
import="@$repo/claude-code/CLAUDE.md"
grep -Fqx "$import" "$HOME/.claude/CLAUDE.md" || printf '\n%s\n' "$import" >> "$HOME/.claude/CLAUDE.md"
```

Claude Code supports `@path` imports in `CLAUDE.md`, so the adapter stays updateable from the cloned repository.

## 5. Restart and verify

Restart Claude Code if the skills or agents directories did not exist before the current session.

Ask:

```text
List the Silicon Valley development-team skill and custom subagents available to you. Explain the role boundaries and who must remain read-only. Do not change files.
```

The response should identify:

- `/silicon-valley-dev-team`;
- `jared`;
- `richard-hendricks`;
- `dinesh`;
- `gilfoyle`;
- `jian-yang` as read-only;
- the main conversation as accountable engineering lead.

## 6. Use the team

### Full delivery

```text
/silicon-valley-dev-team deliver

Goal: <customer outcome>
Constraints: <technical, legal, cost, timing, compatibility, privacy, or operational boundaries>
Repository area: <path or inspect and determine it>
Authority: <what may be edited, committed, pushed, merged, or deployed>
```

Claude Code should load the master skill, select only the useful subagents, reconcile one plan, assign one editor per area, review the actual diff, and return one result.

### Review only

```text
/silicon-valley-dev-team review <repository, PR, architecture, product, or plan>
```

### Explicit adversarial review

```text
Use the jian-yang agent as a read-only adversarial reviewer of this product and operating model. Focus on competitor substitution, loopholes, incentives, ownership, dependencies, claims, and metric gaming. Do not edit.
```

### Infrastructure change

```text
/silicon-valley-dev-team deliver

Have Gilfoyle lead and edit the bounded platform area. Have Dinesh review integration and developer usability. Use Richard for material architecture. Use Jared for rollout, cost, and commitments. Use Jian-Yang only when ecosystem incentives or dependencies are material.
```

## Claude Code-specific notes

- Custom subagents run in separate contexts and return summaries to the main conversation.
- Agent files under `~/.claude/agents/` are personal; project-specific files can instead be placed in `.claude/agents/`.
- Skills can also be committed under `.claude/skills/` for project or cloud-session use.
- Claude Code may delegate automatically based on an agent's description, but the master skill still controls team shape and editing ownership.
- Do not enable nested agent fan-out merely because the runtime supports it. The specialist agents should return to the parent, not form unmanaged teams.
