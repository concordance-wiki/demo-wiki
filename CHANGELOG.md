# Changelog

## First loop

The wiki built from the tool's own checkout, the sources read from local clones of the two content repositories, before and after the first pass over its findings.

| | Before | After |
|---|---|---|
| Files read | 102 | 216 |
| Entities | 715 (39 terms, 613 keyword pages, 63 specifications) | 999 (105 terms, 785 keyword pages, 109 specifications) |
| Findings | 950 (0 errors, 568 warnings, 382 info) | 1896 (0 errors, 718 warnings, 1178 info) |
| `W-TERM-UNDEFINED` | 556 | 718 |
| `W-REF-UNRESOLVED` | 12 | 0 |
| `W-DOMAIN-UNCLASSIFIED` | 22 | 0 |
| `I-TERM-HOMONYM` | 10 | 16 |
| `W-DUP-CANDIDATE` | 8 | 27 |
| `I-REL-AMBIGUOUS` | 342 | 1135 |

What the tool found and what changed:

- `W-REF-UNRESOLVED` ×12: every screen note named its roles (`reader`, `integrator`, `writer`) and no role note existed. Seven role notes were written under `roles/` of the specifications, the screens name them by path (`roles/reader`) and `writer` became `author`. Fixed.
- `W-DOMAIN-UNCLASSIFIED` ×22: the four domains of the configuration matched notes by a handful of name patterns. The `domains:` block now files every note of both repositories under `quality`, `ingestion`, `inference` (with a `recognition` subdomain) or `publication`. Fixed.
- `I-TERM-HOMONYM`: the alias `relation` was shared by the glossary terms "Link" and "Relation", the alias `LOCAL_CHECKS` by the glossary term "Local check" and the rule "Linter and build parity"; both aliases dropped. The remaining homonyms are deliberate, a term and the object or screen of the same name (`entity`, `finding`, `link`, `model`, `source`, `index` among them), each settled by a `## Not to be confused with` section; the count grew with the new object and screen notes.
- `W-TERM-UNDEFINED`: `type`, `pipeline`, `step`, `frontmatter`, `section`, `keyword`, `locale`, `attribute`, `severity`, `identifier` and the other expressions the tool found without a note received a glossary term, sixty-six in all with the public concepts that had none (every top-level key of `concordance.yaml`, every check family, the vocabulary of the plugin API and of the linter); the verbs and counters the notes repeat (`reads`, `writes`, `first`, `two`, `name`, `list`…) went to `stopwords.domain.txt`, forty-one of them. The count is higher after than before because the corpus doubled: 216 files against 102, and the discovery reads the new notes too. The next loop starts from `PDF`, `expression`, `panel`, `viewer`, `form` and the sentence every rule note repeats.
- `W-DUP-CANDIDATE` and `I-REL-AMBIGUOUS` are information: the first names a term and a specification with the same base name, the second a glossary occurrence between two notes whose types admit no single relation; neither asks for a change.

Also in this loop: the sources moved from `ref: v0.1.0` to `ref: main`, the Pages workflow runs on push, on schedule, on dispatch and on the `content-updated` event the content repositories send, and the specifications gained the notes the tool's parity check requires (twelve rules, the gallery screen, three processes, ten decisions, the canonical model API, five objects, one batch, three tables, three operations).
