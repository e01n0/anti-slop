# anti-slop

Use these rules and local checks to review documents and slide decks written with an LLM.

## Files

- `AGENTS.md`: Writing rules for an agent.
- `RESEARCH.md`: Current tools and primary research.
- `tools/ste_lint.py`: Python linter for mechanical prose patterns.
- `tools/slop.tsv`: Terms used by the linter.

Use [SlopSift](https://github.com/NikhilVerma/slopsift) for structural patterns.

## Rules

Keep a sentence when it:

- States a fact.
- Shows evidence.
- Records a decision.
- Explains a cause.
- Gives an instruction.

Delete sentences that do none of these jobs.

- Lead with the point.
- Put one fact or action in each sentence.
- Use active voice and name the actor.
- Use one term for each concept.
- Prefer common words.
- Do not start a sentence with `this`, `it`, `they`, `their`, `these`, or `those`. Repeat the noun.
- Make headings describe their content.
- Remove introductions and summaries that repeat the body.

Write `SlopSift reports possible writing problems`, not `Their findings describe the text`.

The sentence limits and procedural rules come from [ASD-STE100 Simplified Technical English](https://www.asd-ste100.org/).

## Use

Add the relevant rules from `AGENTS.md` to the project instructions.

Run the local linter:

```bash
python3 tools/ste_lint.py --type descriptive path/to/file.md
```

Use `--type procedural` for instructions. Use `--fail-on-findings` to return a non-zero exit code for any finding.

Run SlopSift:

```bash
npx slopsift path/to/file.md \
  --rulepack ai-style \
  --rulepack reader-first \
  --level info
```

Read each finding in context before editing the text.

## Slide decks

- Put one claim on each slide.
- State the claim in the title.
- Show its evidence in the body.
- Put spoken detail in the notes.
- Remove generic sections that contain no facts.

## Limits

The Python linter uses regular expressions. Markdown tables and diagrams can cause false positives.

SlopSift reports patterns in the text. SlopSift does not identify the author.

Neither tool checks factual accuracy.

## Licence

[MIT](LICENSE)
