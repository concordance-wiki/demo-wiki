# Concordance wiki

The configuration repository that publishes the Concordance project wiki at `https://concordance-wiki.github.io/demo-wiki`. It holds nothing but configuration: which sources to read, the profile override, the theme, the stopwords and the pipeline. The content lives in [demo-glossary](https://github.com/concordance-wiki/demo-glossary) and [demo-specs](https://github.com/concordance-wiki/demo-specs), and the tool builds its own wiki from them.

Copy this repository to start a wiki of your own: change the sources in `concordance.yaml`, the name, logo and colours in `theme.yaml` (and drop `footer.credit`, which this wiki keeps because the tool is documenting itself), and the pipeline does the rest.

## The loop

1. An author changes a note in the glossary or in the specifications. The pull request is linted where it is written (`.github/workflows/lint.yml` of each content repository): the SARIF log lands in the margin of the diff and an error finding fails the check.
2. Once merged, the lint runs again on `main` and, when green, sends a `content-updated` dispatch to this repository.
3. The wiki workflow (`.github/workflows/pages.yml`) builds the site of the three repositories, the two sources cloned at their `main` ref at depth 1, and publishes `dist/` on GitHub Pages. It also runs on every push here, every morning at 05:00 UTC, and on manual dispatch, so that a dispatch lost for want of a token is caught up within a day.
4. The repository of the tool verifies on every change that the wiki still covers it (`scripts/parity.mjs`): every check has a rule note, every page slot a screen note, every active type a note, every top-level configuration key and every check family a glossary term.

Until the first release of the tool, every workflow builds the command line from a checkout of [the tool's repository](https://github.com/concordance-wiki/concordance) at `main`; once the `concordance` package is published, the build steps become the one-liners of the [pipelines guide](https://github.com/concordance-wiki/concordance/blob/main/docs/guides/pipelines.md).

Two steps are done by a person, once:

- GitHub Pages: in the settings of this repository, set Pages → Source to "GitHub Actions". Until then the workflow builds and the deploy job fails.
- The dispatch token: the automatic token of a run cannot reach another repository. Create a fine-grained personal access token with the "Contents: read and write" permission on this repository and store it as the `WIKI_DISPATCH_TOKEN` secret of each content repository. Without it the dispatch step is skipped and the nightly build takes over.

## Building locally

```bash
node <tool>/packages/cli/dist/bin.js build --config concordance.yaml --output dist
```

reads the sources from GitHub. To build from local checkouts, copy `concordance.yaml` next to them and replace each `git`/`ref` pair with `path: ../demo-glossary` and `path: ../demo-specs`; the copy stays out of this repository.

## First loop

The first build of this wiki from the tool's own checkout read 102 files and reported 950 findings, none an error: 556 recurring expressions without a note (`W-TERM-UNDEFINED`), 12 unresolved references (`W-REF-UNRESOLVED`: every screen named its roles, `reader`, `integrator`, `writer`, and no role note existed), 22 notes outside every domain (`W-DOMAIN-UNCLASSIFIED`), 10 homonyms (`I-TERM-HOMONYM`, two of them accidental: the alias `relation` shared by the terms "Link" and "Relation", the alias `LOCAL_CHECKS` shared by a glossary term and a rule) and 342 links left on the generic relation (`I-REL-AMBIGUOUS`). What changed, in the three repositories: seven role notes, and every screen now names its roles by path; the domain globs rewritten so that every note of the two repositories is filed, with a `recognition` subdomain; the two accidental aliases dropped; sixty-six glossary terms written for the expressions the tool found without a note (`type`, `pipeline`, `step`, `frontmatter`, `section`, `keyword`, `locale`, `attribute` among them) and for the public concepts that had no note, forty-one verbs and counters added to `stopwords.domain.txt` so that the discovery stops proposing them, and the missing specifications: twelve rules, one screen, three processes, ten decisions, one API, five objects, one batch, three tables and three operations. The [CHANGELOG](CHANGELOG.md) keeps the counts before and after.
