# Agent Skills

Portable operating methods for software engineering, product delivery, company operations, and adversarial review.

This repository now contains one installable product: **Silicon Valley Dev Team**. Five character-inspired specialist playbooks are bundled inside one master skill so one installation provides the whole team.

[Cave Pony](https://github.com/wilfgrainger/cave-pony) is a separate project with its own repository, releases, tests, and installation path. This repository only documents how the team can hand a completed result to it as an optional companion pass.

The character-inspired methods are professional workflows, not impersonations. Harmful or comic behaviour is converted into failure modes to resist.

This is an unofficial fan-made project. It is not affiliated with or endorsed by HBO, Warner Bros. Discovery, the programme’s creators, cast, or rights holders.

## Install the whole team

```bash
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/silicon-valley-dev-team
```

That single directory contains:

```text
skills/silicon-valley-dev-team/
├── SKILL.md
└── team/
    ├── dinesh.md
    ├── gilfoyle.md
    ├── jared.md
    ├── jian-yang.md
    └── richard-hendricks.md
```

The master skill selects and loads only the profiles relevant to the task. A request for the full team loads all five.

## Why the team profiles are not nested SKILL.md files

The profiles are bundled reference playbooks rather than deeper `SKILL.md` files. This keeps the package portable: common skill installers treat the shallower master `SKILL.md` as the discovered skill and may shadow deeper skills.

The practical result is better:

- one installation;
- one activation and orchestration contract;
- no duplicate skill discovery;
- only selected profiles enter context;
- one coherent final answer instead of five disconnected reports.

The specialists still behave as distinct roles inside the master workflow. They are not separately installed slash-command skills.

## Team

| Specialist | Professional role | Best used for |
|---|---|---|
| Jared | COO and delivery lead | Customer outcomes, product and business operations, commitments, ownership, planning, launches, and rescue |
| Richard Hendricks | Technical founder and CTO | Technical direction, architecture, algorithms, performance, scaling, pivots, and technology ethics |
| Dinesh | VP Engineering and application-delivery lead | Application code, APIs, UI, integrations, migrations, testing, maintainability, and developer experience |
| Gilfoyle | VP Architecture and platform lead | Infrastructure, networks, security, reliability, deployments, incidents, capacity, rollback, restore, and recovery |
| Jian-Yang | Read-only adversarial product and ecosystem reviewer | Competitors, loopholes, incentives, ownership gaps, hostile dependencies, unsupported claims, copyability, and metric gaming |

See [character role coverage](docs/CHARACTER_ROLE_COVERAGE.md) for the source-to-professional mapping and boundaries.

## Use the team

```text
silicon-valley-dev-team deliver <customer outcome>
silicon-valley-dev-team review <repository, PR, plan, or product>
silicon-valley-dev-team architecture <decision>
silicon-valley-dev-team release <release>
silicon-valley-dev-team rescue <initiative>
silicon-valley-dev-team full-team <substantial task>
silicon-valley-dev-team richard <technical decision>
silicon-valley-dev-team dinesh <application delivery>
silicon-valley-dev-team gilfoyle <platform or security work>
silicon-valley-dev-team jared <operations or rescue>
silicon-valley-dev-team jian-yang <adversarial review>
```

Natural requests such as “use the full dev team” or “get Gilfoyle to review the platform” also activate the master.

The runtime may delegate selected profiles to separate subagents. Without subagents, it applies them sequentially and must not pretend parallel agents ran.

## Cave Pony companion

Install Cave Pony from its own repository:

```bash
npx skills add https://github.com/wilfgrainger/cave-pony/tree/main/skills/cave-pony
```

Use it independently or after the team has produced one coherent, reviewed result:

```text
silicon-valley-dev-team deliver <customer outcome>
cave-pony audit <resulting diff, plan, or documentation>
```

Cave Pony is not a sixth team member and is not embedded or copied here. The master may suggest it when the remaining problem is unnecessary scope, code, dependencies, abstractions, process, documentation, proof cost, or narration. It must never claim Cave Pony ran unless the external skill was available and actually applied.

Accepted simplifications return to the team’s accountable editor for normal correction, review, and proof. Cave Pony must not compress away security evidence, migration safeguards, incident chronology, rollback, recovery, accessibility, or legal and operational obligations.

## Migration from the old layout

Earlier versions exposed the five specialists and Cave Pony as separate top-level skills in this repository.

- Reinstall `silicon-valley-dev-team` using the single command above.
- Remove old standalone team copies from your local agent skill directory to avoid duplicate activation.
- Install or update Cave Pony only from `wilfgrainger/cave-pony`.

## Design principles

- Improve decisions and execution, not merely tone.
- Keep the user as product owner and final decision-maker.
- Use the smallest relevant specialist set unless the user explicitly requests the full team.
- Keep one parent agent accountable for reconciliation and truthfulness.
- Use one primary editor per file or bounded area.
- Keep Jian-Yang read-only and defensive.
- Keep Cave Pony external and independently versioned.
- Evidence, safety, privacy, accessibility, legal obligations, and truthful reporting outrank character flavour or brevity.
- Humour may make the method memorable; it must never make the work hostile or vague.
- Every profile must remain useful after its character name is removed.

## Licence

MIT. See [LICENSE](LICENSE).
