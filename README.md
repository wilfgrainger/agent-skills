# Agent Skills

A small collection of practical agent skills for software engineering and product delivery.

Each skill is designed as an operating method, not a novelty persona. The four *Silicon Valley*-inspired skills translate recognisable character strengths into useful workflows while explicitly rejecting their harmful or comic failure modes.

This is an unofficial fan-made project. It is not affiliated with or endorsed by HBO, Warner Bros. Discovery, the programme's creators, cast, or rights holders. Character names are used only to identify the source of inspiration. The skills do not reproduce scripts, dialogue, or attempt actor impersonation.

## Skills

| Skill | Best used for | Core question |
|---|---|---|
| [Cave Pony](skills/cave-pony/) | Minimal, direct engineering with enough proof | What is the smallest correct change? |
| [Richard Hendricks](skills/richard-hendricks/) | Architecture, algorithms, performance, compression, scaling | Is there a better representation or boundary? |
| [Gilfoyle](skills/gilfoyle/) | Infrastructure, security, reliability, incidents, adversarial review | How does this fail, and can we recover? |
| [Dinesh](skills/dinesh/) | Feature implementation, integrations, APIs, UI and developer experience | Does the complete path actually work? |
| [Jared](skills/jared/) | Product operations, planning, launches, ownership and stakeholder clarity | Who owns the next valuable outcome? |

## Install

Install a skill directly from its folder:

```bash
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/richard-hendricks
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/gilfoyle
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/dinesh
npx skills add https://github.com/wilfgrainger/agent-skills/tree/main/skills/jared
```

The commands above track `main`. Pin to a tag or commit when reproducibility matters.

## Choosing a skill

Use one lead skill for a task:

- Start with **Richard** when the hard part is the technical model or dominant bottleneck.
- Start with **Gilfoyle** when the hard part is trust, failure, operations, or recovery.
- Start with **Dinesh** when the design is understood and the hard part is getting the full implementation path working.
- Start with **Jared** when the hard part is ownership, priorities, sequencing, launch, or communication.
- Start with **Cave Pony** when the main risk is unnecessary scope, code, abstraction, or narration.

Skills may hand work to one another, but avoid running all of them as persistent personalities. A useful sequence for a substantial feature is:

```text
Jared defines the outcome and ownership
Richard resolves the hard architecture
Dinesh implements the vertical slice
Gilfoyle challenges failure and recovery
Cave Pony removes anything that did not earn its place
```

## Commands

```text
/richard-hendricks design <system>
/richard-hendricks optimize <bottleneck>
/gilfoyle audit <system>
/gilfoyle incident <service>
/dinesh build <feature>
/dinesh integrate <components>
/jared plan <initiative>
/jared launch <release>
```

Each `SKILL.md` contains its activation rules, modes, execution loop, decision rules, output contract, boundaries, and completion test.

## Design principles

- Skills must improve decisions and execution, not merely change tone.
- Character inspiration is limited to broad traits and working patterns.
- Every skill names the failure modes it must resist.
- Evidence, safety, privacy, accessibility, and truthful reporting outrank persona consistency.
- Skills should have distinct activation boundaries and useful completion criteria.
- Humour may make the method memorable; it must not make the work hostile.

## Licence

MIT. See [LICENSE](LICENSE).
