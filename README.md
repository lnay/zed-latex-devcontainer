# "dev"-container template for LaTeX in Zed editor

[Zed](https://zed.dev) does not have built-in support for devcontainers, however for LaTeX this is not a barrier as `texlab` is not tightly coupled with LaTeX compilers anyway.
This template demonstrates how to configure Zed to build the document via `docker-compose` using a
[texlive container image from dockerhub](https://hub.docker.com/r/texlive/texlive).

A benefit to this approach is not needing to install a LaTeX distribution directly, and a bit of extra confidence with the reproducibility of the build.

## Forward+inverse search

This template includes a config to have both forward and inverse search working with `zathura` (requires `sed` and `bash` on path).
Adjustments are necessary for other PDF viewers.
The corresponding section of `.zed/settings.json` (the "forwardSearch" item) could be deleted, and the autoconfig could be relied on instead (provided that works already), at the cost of inverse-search not working. Inverse-search needs extra care when compiling the document from inside the container, as the file path that will be attempted to be opened will actually be the path inside the container (not where `zed` is running).

## `texlab` vs tasks

This template is set up with build-on-save and forward-search after build.
Alternatively, one could use the `tasks` feature of Zed to build the document, by clicking the play button next to `\documentclass` in main.tex.
If doing so, set "lsp.texlab.settings.texlab.build.onSave" to `false` in `.zed/settings.json`.
Forward+inverse search are not set up here with tasks.

## Shell access

To run `bash` in the container (with the workspace), run the following in this directory:
```bash
docker compose -f .container/compose.yaml run shell
```
... or just `docker compose run shell` in the `.container` directory.

If needing to run a `latexmk` command, for example `latexmk -C`, then you can also run:
```bash
docker compose -f .container/compose.yaml run latexmk -C
```
