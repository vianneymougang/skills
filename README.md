# skills

Agent skills I write and maintain. A skill is a folder of Markdown files that a coding agent (Claude Code, Codex, Cursor and others) loads when a task matches its description.

## Install

```bash
npx skills add vianneymougang/skills
```

## Available skills

| Skill | What it does |
| --- | --- |
| [`ux-psychology`](skills/ux-psychology) | Psychology-based UI/UX principles for designing and auditing interfaces |

## ux-psychology

The skill gives an agent a catalog of 40 interface principles grounded in psychology, such as Hick's law, anchoring, chunking or loss aversion. Each principle has a stable ID (`UX-P01` to `UX-P40`), so a design note, a ticket or a code comment can cite the reasoning behind a choice and reuse it later.

The agent works in one of two modes:

- **Design**: there is no screen yet. The agent states the screen's job, picks the principles whose cue matches, and returns one recommendation per principle.
- **Audit**: a screen exists (code, mockup, screenshot or URL). The agent checks it against the catalog and returns findings with a severity: `blocking`, `significant` or `minor`.

Every item it returns carries an ethical guard verdict: `respected`, `adjusted` or `refused`. Many of these principles sit one step from a dark pattern (fake urgency, confirmshaming, decoy pricing). A `refused` verdict names the dark pattern as the finding.

The principles are split into five files:

| File | Covers |
| --- | --- |
| `PRINCIPLES-cognition.md` | Cognitive load and decision-making: forms, settings, pricing |
| `PRINCIPLES-perception.md` | Visual hierarchy, attention, grouping, navigation |
| `PRINCIPLES-motivation.md` | Onboarding, multi-step flows, progress, retention |
| `PRINCIPLES-persuasion.md` | Acquisition, landing and conversion screens |
| `PRINCIPLES-trust.md` | Transactional and high-stakes screens, feedback, error states |

`SKILL.md` holds the procedure and an index of all 40 cues. `FORMAT.md` defines the entry template.

## Checking the catalog

A script checks every entry against `FORMAT.md` and regenerates the index in `SKILL.md`. It uses the Python standard library only.

```bash
python3 tools/check-ux-psychology.py          # check all entries
python3 tools/check-ux-psychology.py --fix    # regenerate the indexes
python3 tools/tests/run.py                    # test the checker on its fixtures
```

The `research/` folder holds the audits and source checks behind each rewrite of the catalog.

## License

MIT
