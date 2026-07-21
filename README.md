# Agent Skills

Portable `SKILL.md` operating methods for software engineering, product delivery, company operations, and adversarial review.

The repository contains five specialists inspired by HBO's *Silicon Valley*, one master skill that coordinates them, and Cave Pony for simplicity and proof. They are professional methods, not character impersonations. Harmful or comic behaviour is converted into failure modes to resist.

This is an unofficial fan-made project. It is not affiliated with or endorsed by HBO, Warner Bros. Discovery, the programme's creators, cast, or rights holders.

## Skills

| Skill | Professional role | Best used for |
|---|---|---|
| [Silicon Valley Dev Team](skills/silicon-valley-dev-team/) | Master orchestrator | Selecting the smallest relevant team, assigning one lead and editor per area, reconciling advice, review, testing, and final delivery |
| [Richard Hendricks](skills/richard-hendricks/) | Technical founder and CTO | Technical direction, architecture, algorithms, performance, scaling, pivots, and technology ethics |
| [Gilfoyle](skills/gilfoyle/) | VP Architecture and platform lead | Infrastructure, networks, security, reliability, deployments, incidents, capacity, and recovery |
| [Dinesh](skills/dinesh/) | VP Engineering and application-delivery lead | Application delivery, APIs, UI, integrations, migrations, testing, maintainability, and developer experience |
| [Jared](skills/jared/) | COO and delivery lead | Customer outcomes, product and business operations, commitments, planning, launches, ownership, and rescue |
| [Jian-Yang](skills/jian-yang/) | Read-only adversarial product and ecosystem reviewer | Competitors, loopholes, incentive abuse, ownership gaps, hostile dependencies, unsupported claims, copyability, and metric gaming |
| [Cave Pony](skills/cave-pony/) | Simplicity and proof coach | Removing unnecessary scope, code, abstraction, and narration while preserving correctness |

See [character role coverage](docs/CHARACTER_ROLE_COVERAGE.md) for the source-to-professional mapping and role boundaries.

## Use the team

Invoke the master skill when work crosses roles:

```text
silicon-valley-dev-team deliver <customer outcome>
silicon-valley-dev-team review <repository, PR, plan, or product>
silicon-valley-dev-team architecture <decision>
silicon-valley-dev-team release <release>
silicon-valley-dev-team rescue <initiative>
```

The runtime may add its own invocation prefix.

The master skill:

1. selects only specialists that can materially improve the result;
2. chooses one accountable lead;
3. assigns one primary editor per file or bounded area;
4. reconciles advice before editing;
5. reviews the actual result and evidence;
6. corrects validated findings and reruns decisive checks;
7. returns one coherent outcome.

Dinesh normally edits application work. Gilfoyle normally edits platform work. Richard may build a narrow prototype or architecture record. Jared may edit operating documents. Jian-Yang is always read-only.

Gilfoyle and Jian-Yang are deliberately different: Gilfoyle attacks technical trust, failure, infrastructure, and recovery paths; Jian-Yang attacks product, competitor, incentive, ownership, dependency, claim, and metric weaknesses.

## Portability

The `SKILL.md` files are the product. No vendor-specific profiles or adapters are required.

- A runtime with skill and subagent support may delegate selected specialist skills to separate agents.
- A runtime with skill support but no subagents applies the selected skills sequentially and must not pretend parallel agents ran.
- Any runtime that can read Markdown can use the master skill as the team contract and load only the specialist skills needed for the task.

## Install

Install the master and specialists with an Agent Skills-compatible installer:

```bash
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/silicon-valley-dev-team
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/richard-hendricks
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/gilfoyle
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/dinesh
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/jared
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/jian-yang
```

Or copy or symlink the skill folders into the personal or project skill directory supported by your runtime.

Invoke one specialist directly when the problem clearly fits one role. Use Cave Pony as a final simplification lens, not as another standing team member.

## Design principles

- Improve decisions and execution, not merely tone.
- Keep the user as product owner and final decision-maker.
- Keep one parent agent accountable for integration and truthfulness.
- Use one primary editor per file or bounded area.
- Keep Jian-Yang read-only and defensive.
- Evidence, safety, privacy, accessibility, legal obligations, and truthful reporting outrank character flavour.
- Humour may make the skills memorable; it must never make the work hostile or vague.
- Every skill must remain useful after its character name is removed.

## Licence

MIT. See [LICENSE](LICENSE).