# Stop making readers edit your AI output

AI makes text cheap. Reading still costs time.

That imbalance creates a grim little bargain. The author saves twenty minutes. Every reader spends extra time finding the point.

Slop sounds finished before an editor touches it. It expands weak ideas and hides missing evidence behind confident cadence. It gives minor points the same weight as decisions.

Readers learn to distrust the whole document. Once the first few slides waste their time, they skim the rest. The useful material disappears with the filler.

I do not try to prove whether AI wrote a document. I edit the visible problems. Good output starts with controlled language, passes through automated checks, and ends with human judgement.

This repository pairs a small mechanical linter with [SlopSift](https://github.com/NikhilVerma/slopsift), which detects structural writing patterns.

## The test

Every sentence must do at least one job:

- State a fact.
- Show evidence.
- Record a decision.
- Explain a cause.
- Tell the reader what to do.

Voice and rhythm are welcome when they carry content. Delete any sentence that survives only for rhythm.

This rule catches more slop than a blacklist. A word such as "critical" can name a real dependency. It becomes slop when it replaces the missing fact.

## The anti-slop stack

### 1. Decide what the reader needs

Before I prompt a model, I write down:

- Who will read the material.
- What they need to understand or decide.
- Which facts support the point.
- What the material must leave out.

For a deck, I write the claim of each slide as a plain sentence. For a document, I separate explanation from instructions. This prevents the model from filling an empty structure with generic prose.

A title such as "Key considerations" says nothing. "Three source systems miss the migration deadline" tells the reader what the slide contains.

### 2. Constrain the first draft

Negative instructions drift during a long generation. "Be concise" and "avoid buzzwords" leave the model to decide what good writing looks like.

I use positive rules based on [ASD-STE100 Simplified Technical English](https://www.asd-ste100.org/):

- Keep descriptive sentences under 25 words.
- Keep instructions under 20 words.
- Put one fact or action in each sentence.
- Use active voice and name the actor.
- Put a condition before its instruction.
- Use one term for each concept.
- Prefer the common word: "use" instead of "utilise".

These are production controls for technical text. They reduce the model's freedom to pad a weak point or rotate through impressive synonyms.

The first draft improves because the model receives a pattern to follow. It does not have to infer the pattern from a list of banned phrases.

### 3. Use two different detectors

One checker cannot see every class of problem. I use two:

1. A deterministic linter finds mechanical faults. Mine checks sentence length, weak modals, contractions, `-ing` tails, dashes, filler words, and synonym rotation.
2. [SlopSift](https://github.com/NikhilVerma/slopsift) finds structural patterns. It catches vague attribution, promotional language, decorative triplets, passive actor hiding, and repeated corrective contrasts.

Agreement between independent checks deserves attention. A single warning asks for inspection, not an automatic rewrite.

The tools report writing signals. They do not prove authorship. They also misread Markdown tables, diagrams, quoted text, and terse runbooks. Chasing a score of zero can make a good technical document worse.

### 4. Apply human judgement

The final pass looks for problems that linters miss:

- **Headings:** Each heading names the content. It does not editorialise. Replace "The evidence that sets the shape" with "Cross-domain coupling in the estate".
- **Lead-ins:** Delete sentences that announce the next point. State the point instead.
- **Evidence:** Replace claims about importance with the number, source, owner, or mechanism.
- **Repetition:** Remove repeated reassurance and summary paragraphs. Readers noticed the point the first time.
- **Voice:** Restore the writer's normal vocabulary and judgement. Clean prose does not need to sound sterile.

This is also where I reject false positives. A technical term can stay when it is exact. A repeated word is often clearer than forced synonym changes.

## Decks need a stricter edit

Slides encourage a specific form of slop. Models fill every empty region because the layout looks unfinished. Empty space helps the reader find the point.

I use these rules for decks:

- One slide carries one claim.
- The title states the claim, rather than naming a topic.
- The body shows the minimum evidence needed to support the claim.
- The source sits beside the evidence.
- Spoken detail belongs in the notes or appendix.
- Generic boxes called "Benefits", "Challenges", or "Considerations" need facts or removal.

A reader must be able to repeat the slide's claim after a short glance. The deck must also remain legible after the meeting, when the presenter is gone.

## A 15-minute review

**Minutes 0–3: Read only the headings.** They must tell the complete story. Replace topic labels and editorial commentary with claims.

**Minutes 3–6: Mark the useful material.** Highlight each fact, source, decision, cause, or instruction. Delete paragraphs that contain none.

**Minutes 6–9: Run both checks.** Fix high-confidence mechanical faults first. Inspect structural warnings in context.

**Minutes 9–12: Remove the narrator.** Cut announcements, fake punchlines, repeated conclusions, and claims of importance.

**Minutes 12–15: Read it aloud.** Restore natural rhythm. Shorten any sentence that needs a second reading.

## Use it with an agent

Copy [AGENTS.md](AGENTS.md) into a project, or add its rules to your existing agent instructions.

## Run the checks

The deterministic linter has no dependencies:

```bash
python3 tools/ste_lint.py --type descriptive README.md
```

Use `--type procedural` for instructions. Add `--fail-on-findings` when any finding must return a non-zero exit code.

Run [SlopSift](https://github.com/NikhilVerma/slopsift) for structural patterns:

```bash
npx slopsift README.md --level info
```

Read every reported sentence before changing it. Neither tool understands your intent.

## Eight-slide version

1. **AI makes text cheap. Reading still costs time.**
   Show the author's saved time beside the total time lost across the audience.

2. **Slop transfers editorial work to the reader.**
   Use one real before-and-after paragraph. Mark the facts in each version.

3. **Every sentence needs a job.**
   Show the five valid jobs: fact, evidence, decision, cause, instruction.

4. **Positive writing rules give the model a pattern.**
   Compare "avoid buzzwords" with the controlled-language rules.

5. **Two detectors find different faults.**
   Show mechanical checks beside structural checks. Include one false positive.

6. **The human edit removes the narrator.**
   Replace an editorial heading and a teeing-up sentence with the direct claim.

7. **Decks need one claim per slide.**
   Show a crowded "Key considerations" slide beside a claim-led version.

8. **A 15-minute review changes the economics.**
   End with the timed review and the agent instruction.

## Tools and references

- [ASD-STE100](https://www.asd-ste100.org/) supplies the controlled-language discipline.
- [SlopSift](https://github.com/NikhilVerma/slopsift) detects structural writing patterns locally. Its [website](https://slopsift.dev/) documents the rules.
- [Wikipedia's signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) is a useful human review checklist.
- `tools/ste_lint.py` checks sentence length, modals, filler words, dashes, and terminology drift.

The tools improve expression. They do not make a claim true. Source review remains a separate job.

## Licence

[MIT](LICENSE)
