# Changelog

## Every feature

A third source, [demo-briefs](https://github.com/concordance-wiki/demo-briefs), brings the kinds of file the wiki had never read: three working sessions, each a folder of minutes and WebVTT transcript, one of them with the deck shown and its PDF preview, and one framing deck with its preview and its notes. The configuration declares the four plugins the corpus needs, converts the decks with LibreOffice, enables pseudonymisation on a committed dictionary of the four fictional participants and publishes the transcripts; the specifications gain the OpenAPI contract of the model query API, kept next to its note, and a sketch embedded by the entity page; the glossary gains the meeting, the deck and the preview. The wiki built from the tool's own checkout, the sources read from local clones, before and after.

| | Before | After |
|---|---|---|
| Sources | 2 | 3 |
| Files read | 229 | 249 |
| Entities | 1186 (109 terms, 959 keyword pages, 118 specifications) | 1480 (112 terms, 1246 keyword pages, 118 specifications, 4 briefs) |
| Findings | 2262 (0 errors, 887 warnings, 1375 info) | 2490 (0 errors, 1094 warnings, 1396 info) |
| `W-TERM-UNDEFINED` | 887 | 1094 |
| `W-DUP-CANDIDATE` | 21 | 21 |
| `I-TERM-HOMONYM` | 19 | 21 |
| `I-REL-AMBIGUOUS` | 1335 | 1354 |
| `W-DOC-NOMD`, `W-CONV-FAILED`, `W-CONTRACT-UNREACHABLE` | 0 | 0 |
| Twin resources merged | 0 | 4 groups (11 files) |
| Contracts imported | 0 | 1 (3 operations, all matched to a note) |
| `concordance lint` on each content repository | 0 findings | 0 findings |

What the tool found and what changed:

- **Pseudonymisation is declared, not applied.** The page of every session says "Pseudonymised participants" and the configuration validates, but the cues, the fragment and the copied transcript still carry the names of the dictionary: the pipeline of this version never calls the pseudonymisation the core package ships. The names are invented, the dictionary is committed for that reason, and the scenario stays configured so that the first build that applies it shows the difference. Reported to the tool.
- **A contract that was not one.** The plugin API note declared its manifest schema, a JSON schema at a URL that did not exist, under `contract:`; the importer, enabled for the first time, reported `W-CONTRACT-UNREACHABLE`. The note names the schema in its text and declares no contract. Fixed.
- **The briefs merge as intended.** Every file of a session shares its base name, the minutes carry the title of the deck as their heading and declare their transcript under `source:`, the preview repeats the text of the deck: four groups, 11 files, no `W-DOC-NOMD`, and the profile declares `source` on the meeting type so that the declaration raises no `W-ATTRIBUTE-UNKNOWN`. A local source has no commit, so the "same commit" signal only appears in the published build; the groups are the same without it. The two `I-TERM-HOMONYM` added are the titles the deck, its preview and its notes share before the reconciliation folds them into one page.
- **Plugins from a checkout.** The core of the command line cannot resolve the workspace plugins of the tool's checkout by their package names; the workflow links them into its `node_modules` until the preset is published. The dependency on LibreOffice is installed in the same workflow.
- `W-TERM-UNDEFINED` grows by 207 and the keyword pages by 287: the spoken text of three transcripts and the slides of two decks bring expressions no note defines (`slide`, `deck`, `session`, `minutes`, `preview` among them, three of which now have a term). The next loop of the glossary starts from them, and from the words the transcripts repeat that `stopwords.domain.txt` should absorb.
- Not shown: a dormant space on the home page. A source is a whole repository, and the newest change of every space is recent; a fourth source restricted to an archive folder would need a sub-folder root the configuration does not offer.

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
