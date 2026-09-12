# Concordance wiki

The configuration repository that publishes the Concordance project wiki at `https://concordance-wiki.github.io/demo-wiki`. It holds nothing but configuration: which sources to read, the profile override, the theme, the stopwords and the pipeline. The content lives in [demo-glossary](https://github.com/concordance-wiki/demo-glossary) and [demo-specs](https://github.com/concordance-wiki/demo-specs).

Copy this repository to start a wiki of your own: change the sources in `concordance.yaml`, the name and colours in `theme.yaml`, and the pipeline does the rest.

The pipeline is disabled until the `concordance` command is published; it runs on manual dispatch only.
