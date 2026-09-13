# Changelog

## Structure

The two content repositories restructured so that the wiki shows every way a corpus can be described: thematic folders in the glossary, nested families in the specifications, domains by folder, typing by folder glob, file name pattern, suffix, default type and frontmatter, three applications, three stopword files, a lock file with real decisions, a profile that extends a type. The README of this repository lists the scenarios. The wiki built from the tool's own checkout, the sources read from local clones, before and after.

| | Before | After |
|---|---|---|
| Files read | 218 | 218 |
| Entities | 1021 (107 terms, 805 keyword pages, 109 specifications) | 1010 (106 terms, 794 keyword pages, 110 specifications) |
| Findings | 1935 (0 errors, 746 warnings, 1189 info) | 1939 (0 errors, 736 warnings, 1203 info) |
| `W-TERM-UNDEFINED` | 746 | 736 |
| `W-REF-UNRESOLVED` | 0 | 0 |
| `W-DOMAIN-UNCLASSIFIED` | 2 | 0 |
| `W-TYPE-UNKNOWN`, `W-APP-UNKNOWN`, `W-ATTRIBUTE-UNKNOWN` | 0 | 0 |
| `I-TERM-HOMONYM` | 16 | 16 |
| `W-DUP-CANDIDATE` | 27 | 19 |
| `I-REL-AMBIGUOUS` | 1144 | 1168 |
| `concordance lint` on each content repository | 0 findings | 0 findings |

What changed and what the counts say:

- The file count is unchanged although two notes were written (`notes/type-by-filing.md`, a decision typed by the source's default type, and `screens/pages/exploring-the-site.md`, a process filed among the screens on purpose): the README of each content repository, read as a term and as a document until now, is excluded by `privacy.exclude`. Hence one term and one specification fewer on that side. Twenty-three keyword pages disappear, eleven of them the interface words the new `stopwords.publication.txt` absorbs (`button`, `region`, `keyboard`, `heading`) and the others expressions the two READMEs carried over the threshold (`demo`, `story`, `layout`, `repository lint`); twelve appear, phrases of the two new notes (`entity at one hop`, `trail travels`, `highlighted property`).
- `W-DOMAIN-UNCLASSIFIED` ×2, the two terms written after the domain globs of the first loop (`facet`, `folder domain`), disappear with the globs themselves: every domain is now a folder, and a note filed in a new folder under one of them is classified without a change to the configuration. Fixed.
- `W-DUP-CANDIDATE` drops from 27 to 19: the pairs of glossary terms with close base names in one flat folder (`build` and `build-log`, `local-check` and `locale`, `markdown` and `markdown-link` among them) are no longer neighbours once the terms are filed by subject, and the two READMEs no longer meet. The pairs that remain are recorded as separated in `concordance.lock.yaml`; the build of this version accepts the lock without reading it, so the count stays.
- `W-TERM-UNDEFINED` loses twenty-seven expressions, the same interface words and README phrases, and gains seventeen from the two new notes; `I-REL-AMBIGUOUS` grows by 24 with the glossary occurrences of the two new notes. Neither asks for a change beyond what the next loop of terms will bring.
- Every check of the tool keeps its rule note, every page slot its screen note, every active type at least one note and every configuration key its term: the parity script of the tool's repository is green on the three restructured checkouts.

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
