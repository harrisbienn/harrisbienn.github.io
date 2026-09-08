# Harris Bienn CV

This repository owns the account-root deployment at [harrisbienn.github.io](https://harrisbienn.github.io). It intentionally contains only the GitHub Pages publishing workflow and its runbook.

## Source of truth

CV content, templates, site assets, and build tooling live in [`harrisbienn/unified-cv`](https://github.com/harrisbienn/unified-cv). Edit `cv/Harris_Bienn_CV.yaml` there; do not copy source or generated files into this repository.

The publisher checks out `unified-cv/main`, runs its containerized build and verification, uploads the resulting `dist/` artifact, and deploys it through GitHub Pages. Build failures stop before deployment, so the last successful site remains live.

## Publishing

The workflow runs in three situations:

- hourly at 17 minutes past the hour, picking up approved changes from `unified-cv/main`;
- after changes to this repository's `master` branch; and
- on manual dispatch, optionally targeting a central branch, tag, or commit.

To publish immediately after merging a central change:

```sh
gh workflow run pages.yml --repo harrisbienn/harrisbienn.github.io -f source_ref=main
```

The workflow uses only this repository's built-in `GITHUB_TOKEN`. The build job can read public source but cannot deploy; the isolated deploy job receives only `pages: write` and `id-token: write`.

## Recovery

Dispatch the workflow with a known-good `unified-cv` commit SHA to roll back the live site. Dispatch it with `source_ref=main` to return to the latest approved version.

See [`docs/deployment.md`](docs/deployment.md) for deployment checks, failure recovery, and rollback details.
