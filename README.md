# Agent Skills

A small collection of practical agent skills for software engineering, product delivery, company operations, and adversarial review around software teams.

Each skill is an operating method, not a novelty persona. The five *Silicon Valley*-inspired skills translate the characters' broad on-screen responsibilities into a high-functioning professional team while explicitly rejecting their harmful or comic failure modes.

This is an unofficial fan-made project. It is not affiliated with or endorsed by HBO, Warner Bros. Discovery, the programme's creators, cast, or rights holders. Character names are used only to identify the source of inspiration. The skills do not reproduce scripts, dialogue, or attempt actor impersonation.

## Skills

| Skill | Professional role | Best used for | Core question |
|---|---|---|---|
| [Cave Pony](skills/cave-pony/) | Simplicity and proof coach | Minimal, direct engineering with enough evidence | What is the smallest correct change? |
| [Richard Hendricks](skills/richard-hendricks/) | Technical founder and CTO | Technical vision, architecture, algorithms, performance, compression, scaling, pivots, and technology ethics | Is there a better representation or technical direction? |
| [Gilfoyle](skills/gilfoyle/) | VP Architecture and platform lead | Infrastructure, networks, security, reliability, deployments, incidents, capacity, and recovery | How does this fail, and can we operate and recover it? |
| [Dinesh](skills/dinesh/) | VP Engineering and application-delivery lead | Feature implementation, integrations, APIs, UI, migrations, engineering execution, testing, and developer experience | Does the complete path actually work and remain maintainable? |
| [Jared](skills/jared/) | COO and delivery lead | Customer outcomes, product and business operations, commitments, planning, launches, partnerships, ownership, and stakeholder clarity | Who owns the next valuable outcome, and what promise are we making? |
| [Jian-Yang](skills/jian-yang/) | Adversarial product and ecosystem reviewer | Competitor simulation, loopholes, incentive abuse, cloning and substitution risk, hostile dependencies, ownership gaps, and metric gaming | How would a self-interested actor exploit, copy, game, or route around this? |

See [Silicon Valley character role coverage](docs/CHARACTER_ROLE_COVERAGE.md) for the source-to-professional mapping, team boundaries, and humour rules.

## Codex personal dev team

The repository includes ready-to-copy Codex custom-agent profiles and lead-agent instructions that combine the five *Silicon Valley*-inspired skills into a controlled delivery team:

```text
User: product owner and final decision-maker
Jared: COO, customer and business operations, delivery structure
Richard: technical founder and CTO
Dinesh: VP Engineering and application delivery
Gilfoyle: VP Architecture, platform, security, reliability, and recovery
Jian-Yang: read-only adversarial product, competitor, loophole, and abuse review
Parent Codex thread: accountable engineering lead and integrator
```

The team is task-shaped rather than a rigid conveyor belt:

- Dinesh normally edits application, API, UI, integration, and migration work.
- Gilfoyle may lead and edit infrastructure, deployment, security, observability, or recovery work.
- Richard may create a narrow algorithmic prototype or architecture document.
- Jared may own planning, launch, operating, customer, or stakeholder documents.
- Jian-Yang remains read-only and challenges the product, business model, ecosystem, ownership, incentives, and claims from a self-interested external perspective.
- One primary editor owns each file or bounded area.
- Independent specialists review the actual evidence and diff.

See [Use the Silicon Valley skills as a Codex dev team](docs/CODEX_PERSONAL_DEV_TEAM.md) for Windows, WSL, Linux, and macOS setup, verification, worktree guidance, and copy-paste team prompts.

The supporting files are under [`codex/`](codex/):

- `AGENTS.md` — global team-lead, role-boundary, safety, evidence, and handoff rules;
- `agents/*.toml` — the five spawnable custom-agent profiles;
- `config.toml.example` — bounded concurrency with no recursive fan-out.

## Install individual skills

Install a skill directly from its folder with an Agent Skills-compatible installer:

```bash
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/richard-hendricks
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/gilfoyle
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/dinesh
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/jared
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/jian-yang
```

For Codex, personal skills can instead be copied or symlinked into `~/.agents/skills/`. The team setup guide provides exact commands. Installations tracking `main` receive future changes; pin to a tag or commit when reproducibility matters.

## Choosing a lead

Use one accountable lead for the hard part of the task:

- Start with **Richard** when the hard part is technical direction, architecture, algorithms, performance, a major pivot, or an ethical capability boundary.
- Start with **Gilfoyle** when the hard part is platform, trust, infrastructure, deployment, failure, operations, capacity, or recovery.
- Start with **Dinesh** when the direction is understood and the hard part is application engineering, integration, migration, or getting the complete product path working.
- Start with **Jared** when the hard part is customer outcome, commitments, business operations, ownership, priorities, sequencing, launch, or communication.
- Add **Jian-Yang** when a product, plan, contract, ecosystem, metric, or completed change needs a read-only hostile-actor or competitor challenge.
- Start with **Cave Pony** when the main risk is unnecessary scope, code, abstraction, or narration.

Skills may hand work to one another, but avoid running all of them as persistent personalities. A useful default sequence for a substantial application feature is:

```text
Jared bounds the outcome, commitments, ownership, and sequence
Richard resolves material technical direction
Dinesh implements and integrates the vertical slice
Gilfoyle challenges security, failure, operability, and recovery
Jian-Yang challenges copyability, loopholes, incentives, dependencies, and claims
Cave Pony removes anything that did not earn its place
```

For infrastructure or security work, Gilfoyle may lead implementation while Dinesh reviews integration and developer usability. Jian-Yang does not replace Gilfoyle's technical threat model; he reviews how self-interested participants can exploit the product and operating model.

## Codex invocation

In Codex CLI or the IDE extension, run `/skills` to browse installed skills or type `$` to mention one explicitly:

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

Each `SKILL.md` contains activation rules, modes, execution loops, decision rules, output contracts, boundaries, and completion tests.

## Design principles

- Skills must improve decisions and execution, not merely change tone.
- Character inspiration covers broad roles and working patterns, not impersonation.
- On-screen misconduct becomes an explicit failure mode to resist.
- The user remains product owner and final decision-maker.
- One parent agent remains accountable for team selection and final synthesis.
- One primary editor owns each file or bounded area.
- Adversarial review remains read-only and defensive.
- Evidence, safety, privacy, accessibility, legal obligations, and truthful reporting outrank persona consistency.
- Skills should have distinct activation boundaries and useful completion criteria.
- Humour may make the method memorable; it must never make the work hostile, vague, or unserious.
- A skill should remain useful after its character name is removed.

## Licence

MIT. See [LICENSE](LICENSE).
