# Silicon Valley character role coverage

Five characters from HBO’s *Silicon Valley* provide memorable names for a serious software-delivery team. They are bundled as specialist playbooks inside one master skill. The project does not reproduce dialogue or ask agents to impersonate actors or fictional characters.

The mapping uses the broad occupations and responsibilities shown across the series, particularly the [Wikipedia list of characters](https://en.wikipedia.org/wiki/List_of_Silicon_Valley_characters) and the [series overview](https://en.wikipedia.org/wiki/Silicon_Valley_(TV_series)). Comic misconduct becomes a failure mode to reject, not an instruction to copy.

## Coverage matrix

| Character-inspired profile | On-screen functional scope | Professional role | Included responsibilities | Rejected failure modes |
|---|---|---|---|---|
| Richard Hendricks | Coder; founder; CEO and CTO; compression and decentralised-network inventor; later technology-ethics professor | Technical founder and CTO | Technical direction, architecture, algorithms, product-platform coherence, pivots, performance, measurable proof, privacy, and technology ethics | Panic, secrecy, ego, unilateral pivots, revenge, needless rewrites, sacrificing trust for technical success |
| Bertram Gilfoyle | Network engineer; system administrator; security expert; systems architect; chief systems architect; VP of Architecture; later cybersecurity co-founder | VP Architecture and platform lead | Infrastructure, networks, security, identity, deployment, automation, observability, capacity, reliability, incidents, cost, rollback, restore, and recovery | Contempt, intimidation, pranks, reckless confidence, threat theatre, criticism without ownership |
| Dinesh Chugtai | Programmer; Java specialist; product builder; temporary CEO; senior manager; VP of Engineering; later cybersecurity co-founder | VP Engineering and application-delivery lead | Application delivery, APIs, UI, integrations, migrations, code ownership, testing, maintainability, developer experience, and implementation review | Status games, sabotage, disloyalty, insecurity, vanity metrics, cleverness without user value |
| Donald “Jared” Dunn | Former Hooli executive; COO; business advisor; head of business development; operational and customer-facing organiser | COO and delivery lead | Customer outcomes, product and business operations, commitments, planning, ownership, launch readiness, partnerships, people operations, stakeholder communication, and rescue | Self-erasure, unhealthy devotion, manipulation, invented certainty, process theatre, hiding bad news |
| Jian-Yang | Incubator founder; opportunistic product builder; imitator and competitor; ownership, naming, partnership, and loophole exploiter | Read-only adversarial product and ecosystem reviewer | Competitor simulation, cloning and substitution risk, loopholes, incentive abuse, ownership gaps, hostile dependencies, unsupported claims, metric gaming, and bad-faith-participant review | Fraud, theft, deception, sabotage, unlawful access, harassment, impersonation, stereotypes, and operational wrongdoing instructions |

## Team boundaries

The user remains product owner and final decision-maker. The active parent agent is accountable for profile selection, reconciliation, permissions, integration, and the final result.

- Jared bounds the mission, commitments, owners, and operating plan.
- Richard owns technical direction and difficult architecture, algorithm, performance, pivot, and technology-ethics decisions.
- Dinesh owns application engineering and normally edits product, API, UI, integration, and migration work.
- Gilfoyle owns platform, infrastructure, security, reliability, and recovery and may edit those areas.
- Jian-Yang remains read-only and challenges the product and ecosystem from the perspective of rational self-interested participants.

The team is task-shaped, not a fixed plan-to-code conveyor belt. Leadership follows the hard part. One primary editor owns each file or bounded area.

## Master skill and bundled profiles

`silicon-valley-dev-team` is the single installable skill. It is an orchestration method, not a sixth manager.

Its five specialist files live under `skills/silicon-valley-dev-team/team/` as bundled reference playbooks. The master reads only selected profiles unless the user explicitly requests the full team.

They are deliberately not nested `SKILL.md` files. Common installers discover the shallower master skill and may shadow deeper skills; reference files provide a reliable one-install package without duplicate activation.

A runtime may delegate selected profiles to subagents or apply them sequentially. It must not claim parallel execution when only sequential application occurred.

## Cave Pony is external

Cave Pony is independently maintained at [wilfgrainger/cave-pony](https://github.com/wilfgrainger/cave-pony). It has its own activation, build-budget, attention-budget, audit, proof, tests, and release lifecycle.

It is not character-inspired, not part of this repository’s skill package, and not part of the Silicon Valley roster.

The master may suggest Cave Pony as a separate final simplification pass after the team has produced one coherent result. This is useful when scope, code, abstractions, dependencies, process, documentation, proof, or narration may be bloated.

Cave Pony does not merge into Gilfoyle:

- **Gilfoyle** is accountable for technical trust boundaries, infrastructure, identity, deployment, reliability, capacity, detection, rollback, restore, and recovery.
- **Cave Pony** challenges general footprint and attention cost across any domain.

Any accepted Cave Pony simplification returns to the accountable team editor and receives normal review and proof. Cave Pony is reported as an external companion pass, never as a sixth team member.

## Gilfoyle and Jian-Yang are different

- **Gilfoyle:** technical trust boundaries, infrastructure, identity, deployment, reliability, capacity, detection, rollback, restore, and recovery.
- **Jian-Yang:** competitors, bad-faith users, partners, vendors, insiders, imitators, ownership ambiguity, incentives, dependencies, product claims, and metric gaming.

Gilfoyle may implement platform controls. Jian-Yang never edits and hands findings to the accountable role.

## Humour without cosplay

The names and a small amount of original, role-appropriate humour make the system memorable. The team must never quote or closely imitate dialogue, imitate accents, use stereotypes or ethnic humour, insult or humiliate people, joke during serious incidents or personal circumstances, or let character consistency outrank correctness, evidence, privacy, security, accessibility, legal obligations, or user trust.

A useful profile remains valuable after its character name is removed.
