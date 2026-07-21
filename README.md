# Agent Skills

Practical agent skills for software engineering, product delivery, company operations, and adversarial review.

The repository contains five specialist skills inspired by HBO's *Silicon Valley*, one master team skill that orchestrates them, and Cave Pony for simplicity and proof. These are professional operating methods, not novelty personas. Harmful or comic character behaviour is converted into explicit failure modes to resist.

This is an unofficial fan-made project. It is not affiliated with or endorsed by HBO, Warner Bros. Discovery, the programme's creators, cast, or rights holders. Character names identify the source of inspiration only. The skills do not reproduce scripts, dialogue, or actor impersonations.

## Skills

| Skill | Professional role | Best used for | Core question |
|---|---|---|---|
| [Silicon Valley Dev Team](skills/silicon-valley-dev-team/) | Master team orchestrator | Selecting and coordinating the smallest relevant specialist team, assigning one editor per area, reconciling advice, testing, review, and final delivery | Which specialists, editor, proof, and review does this outcome actually need? |
| [Richard Hendricks](skills/richard-hendricks/) | Technical founder and CTO | Technical vision, architecture, algorithms, performance, compression, scaling, pivots, and technology ethics | Is there a better representation or technical direction? |
| [Gilfoyle](skills/gilfoyle/) | VP Architecture and platform lead | Infrastructure, networks, security, reliability, deployments, incidents, capacity, and recovery | How does this fail, and can we operate and recover it? |
| [Dinesh](skills/dinesh/) | VP Engineering and application-delivery lead | Feature implementation, integrations, APIs, UI, migrations, engineering execution, testing, and developer experience | Does the complete path actually work and remain maintainable? |
| [Jared](skills/jared/) | COO and delivery lead | Customer outcomes, product and business operations, commitments, planning, launches, partnerships, ownership, and stakeholder clarity | Who owns the next valuable outcome, and what promise are we making? |
| [Jian-Yang](skills/jian-yang/) | Read-only adversarial product and ecosystem reviewer | Competitor simulation, loopholes, incentive abuse, cloning and substitution risk, hostile dependencies, ownership gaps, and metric gaming | How would a self-interested actor exploit, copy, game, or route around this? |
| [Cave Pony](skills/cave-pony/) | Simplicity and proof coach | Minimal, direct engineering with enough evidence | What is the smallest correct change? |

See [Silicon Valley character role coverage](docs/CHARACTER_ROLE_COVERAGE.md) for the source-to-professional mapping, boundaries, and humour rules.

## The team model

```text
User: product owner and final decision-maker
Parent Codex thread: accountable engineering lead and integration owner
Master skill: selects and orchestrates the smallest relevant team
Jared: COO, customer and business operations, delivery structure
Richard: technical founder and CTO
Dinesh: VP Engineering and application delivery
Gilfoyle: VP Architecture, platform, security, reliability, and recovery
Jian-Yang: read-only adversarial product, competitor, loophole, and abuse review
```

The master skill is the front door. Invoke it when you want the team rather than manually assembling agents:

```text
$silicon-valley-dev-team deliver <customer outcome>
$silicon-valley-dev-team review <repository, PR, plan, or product>
$silicon-valley-dev-team architecture <decision>
$silicon-valley-dev-team release <release>
$silicon-valley-dev-team rescue <initiative>
```

It does not spawn everyone automatically. It selects the smallest useful set, chooses one accountable lead, assigns one primary editor per file or bounded area, reconciles advice before editing, reviews the actual result, and returns one evidence-based outcome.

The team is task-shaped:

- Dinesh normally edits application, API, UI, integration, and migration work.
- Gilfoyle may lead and edit infrastructure, deployment, security, observability, or recovery work.
- Richard may create a narrow algorithmic prototype or architecture record.
- Jared may own planning, launch, operating, customer, or stakeholder documents.
- Jian-Yang is always read-only and challenges the product, ecosystem, ownership, incentives, dependencies, claims, and metrics.
- The parent thread remains accountable for integration and truthfulness.

Jian-Yang complements rather than duplicates Gilfoyle. Gilfoyle reviews technical attack, failure, platform, and recovery paths. Jian-Yang reviews how rational self-interested participants can copy, game, exploit, misrepresent, or route around the product or operating model.

## Codex setup

The repository includes:

- `codex/AGENTS.md` — global team-lead, role-boundary, safety, evidence, and handoff rules;
- `codex/agents/*.toml` — five spawnable specialist profiles;
- `codex/config.toml.example` — bounded concurrency for the parent plus five specialists;
- specialist and master `SKILL.md` files under `skills/`.

See [Use the Silicon Valley skills as a Codex dev team](docs/CODEX_PERSONAL_DEV_TEAM.md) for Windows, WSL, Linux, and macOS setup, verification, worktree guidance, and copy-paste prompts.

## Install individual skills

```bash
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/silicon-valley-dev-team
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/richard-hendricks
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/gilfoyle
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/dinesh
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/jared
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/jian-yang
```

For Codex, personal skills can instead be copied or symlinked into `~/.agents/skills/`. Installations tracking `main` receive future changes; pin to a tag or commit when reproducibility matters.

## Choosing a specialist directly

Use the master skill for substantial team work. Invoke a specialist directly when the problem is clearly within one role:

```text
$richard-hendricks founder <product or technical decision>
$richard-hendricks design <system>
$richard-hendricks optimize <bottleneck>
$gilfoyle platform <infrastructure change>
$gilfoyle audit <system>
$gilfoyle incident <service>
$dinesh build <feature>
$dinesh integrate <components>
$dinesh lead <engineering change>
$jared operate <initiative>
$jared plan <initiative>
$jared launch <release>
$jian-yang red-team <product or plan>
$jian-yang competitor <proposition>
$jian-yang loopholes <policy or contract>
```

Use Cave Pony as a final simplification lens when unnecessary scope, code, abstraction, or narration is the main risk. It is a method, not a standing sixth specialist.

## Design principles

- Skills must improve decisions and execution, not merely change tone.
- Character inspiration covers broad roles and working patterns, not impersonation.
- On-screen misconduct becomes an explicit failure mode to resist.
- The user remains product owner and final decision-maker.
- The master skill orchestrates; it does not become another layer of management.
- One parent agent remains accountable for team selection and final synthesis.
- One primary editor owns each file or bounded area.
- Jian-Yang remains read-only and defensive.
- Evidence, safety, privacy, accessibility, legal obligations, and truthful reporting outrank persona consistency.
- Humour may make the method memorable; it must never make the work hostile, vague, or unserious.
- A skill should remain useful after its character name is removed.

## Licence

MIT. See [LICENSE](LICENSE).
