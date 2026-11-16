# Research notes

Checked on 16 November 2026.

## Findings

- Use quality checks. Do not classify authorship.
- Syntax carries more useful signal than a word blacklist.
- Repetition density matters more than a single occurrence.
- News articles draw more style complaints. Short answers draw more factual and structural complaints.
- Human review remains necessary.
- Preserve differences between writers.

Shaib and colleagues define three review areas: information utility, information quality, and style quality. Syntax-only classifiers performed best, with area-under-curve scores of 0.64 and 0.68. Three model judges had near-zero agreement with human labels. ([Paper](https://arxiv.org/abs/2509.19163))

Sourati and colleagues studied more than 880,000 texts. Model rewriting reduced writing-complexity variance by 21% to 50% across the tested datasets and models. ([Paper](https://arxiv.org/abs/2502.11266))

Kobak and colleagues analysed more than 15 million biomedical abstracts. The authors estimated that language models processed at least 13.5% of 2024 abstracts. ([Paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC12219543/))

## Tools before generation

[SimpleEnglish](https://github.com/AminBlg/SimpleEnglish) version 2.1.2 applies ASD-STE100-derived rules before the model writes.

[Antislop](https://github.com/sam-paech/auto-antislop) suppresses repeated phrases during model inference. Antislop requires control of model inference.

## Tools after generation

[SlopSift](https://github.com/NikhilVerma/writinglint) version 0.12.0 uses dependency-graph and document-context rules. Run both `ai-style` and `reader-first`.

Slop Guard release `v0.5.0` scores repetition density and rhythm. Slop Guard calibrates scores against pre-2020 human writing. ([Repository](https://github.com/eric-tramel/slop-guard))

[Vale](https://github.com/vale-cli/vale) version 3.27.0 understands Markdown structure. Vale can restrict rules to headings, paragraphs, or other scopes.

[Humanizer](https://github.com/blader/humanizer) provides rewrite instructions and accepts voice samples.

[slop-gate](https://github.com/hwajongpark/slop-gate) provides vocabulary packs for several languages. Word lists do not detect syntax or relevance.

[Awesome Slop](https://github.com/hwajongpark/awesome-slop) lists more tools and papers.

## Use in this repository

1. `AGENTS.md` constrains the first draft.
2. `ste_lint.py` checks local mechanical rules, including vague pronoun openers.
3. SlopSift checks syntax and reading load.
4. A person reviews relevance, factuality, and voice.

Vale fits teams that need markup-aware house rules. Slop Guard fits teams that need a calibrated score across many documents. The anti-slop repository does not copy either tool.

## Limits

Liang and colleagues found systematic false positives against non-native English writers and easy detector bypasses. Do not use this repository to accuse a writer of using AI. ([Paper](https://arxiv.org/abs/2304.02819))

Paech and colleagues report strong phrase suppression during model inference. Phrase suppression does not measure relevance, factuality, or voice. ([Paper](https://arxiv.org/abs/2510.15061))

Sourati and colleagues link common model outputs with reduced variation in language and reasoning. A rewrite that removes obvious phrases can still flatten the writer's voice. ([Review](https://arxiv.org/abs/2508.01491))
