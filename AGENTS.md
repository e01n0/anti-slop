# Reader-first writing rules

Apply these rules to documents, decks, READMEs, reports, and release notes. Do not apply them to code or quoted text.

## Before drafting

- Identify the audience.
- State what the reader needs to understand or decide.
- List the evidence available.
- Keep facts, numbers, names, commands, and quoted errors unchanged.
- Do not invent detail to make a vague claim look concrete.

For a deck, give each slide one claim. Put the claim in the title.

For a document, separate descriptions from procedures. A description explains. A procedure tells the reader what to do.

## Write for one reading

- Put one fact or action in each sentence.
- Keep descriptive sentences under 25 words.
- Keep instructions under 20 words.
- Use active voice and name the actor.
- Put a condition before its instruction.
- Use one term for each concept.
- Prefer common words.
- When a necessary technical term first appears, define it.
- Do not start a sentence with `this`, `it`, `they`, `their`, `these`, or `those`. Repeat the noun.

Delete promotional adjectives, vague attribution, narrator framing, decorative triplets, rhetorical questions, and fake punchlines.

Replace corrective "not X but Y" phrasing with one positive claim.

Replace an announcement sentence with the fact that it introduces.

Delete any sentence that survives only for rhythm.

## Review

Inspect every heading. Each heading must name the content or state the claim.

Inspect every paragraph. Each paragraph must contain a fact, evidence, a decision, a cause, or an instruction.

Run a mechanical prose linter and a structural slop detector. Read each finding in context. Keep deliberate exceptions and explain them.

Run both the `ai-style` and `reader-first` SlopSift rulepacks.

Do not chase a score of zero. Tables, diagrams, quoted text, and terse runbooks can produce false positives.

The checks improve expression but do not prove that a claim is true.
