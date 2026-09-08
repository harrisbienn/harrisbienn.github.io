# Account-root deployment runbook

## Architecture

[`harrisbienn/unified-cv`](https://github.com/harrisbienn/unified-cv) is the only editable CV and website source. This repository owns the special account-root URL and acts only as its publisher.

The `Publish central CV` workflow checks out a requested `unified-cv` ref, builds and verifies it in the central repository's container, uploads `source/dist`, and deploys that artifact to GitHub Pages. Scheduled and `master`-push runs always use `unified-cv/main`. A manual run may select a branch, tag, or commit SHA.

The build job has read-only repository access. Pages write and OIDC permissions exist only in the deploy job, which does not execute the checked-out source. No personal access token, GitHub App, or cross-repository write credential is required.

## Normal deployment

1. Merge an approved pull request into `unified-cv/main`.
2. Allow the hourly publisher to run, or start `Publish central CV` from this repository's Actions tab with `source_ref` set to `main`.
3. Confirm that both jobs succeed.
4. Verify [the site root](https://harrisbienn.github.io/) and [the PDF](https://harrisbienn.github.io/Harris_Bienn_CV.pdf).

From the GitHub CLI, the immediate-publish command is:

```sh
gh workflow run pages.yml --repo harrisbienn/harrisbienn.github.io -f source_ref=main
```

Scheduled workflows run only from this repository's default branch. GitHub may disable schedules after 60 days without repository activity; manual dispatch remains available.

## Failure recovery

A failed checkout, build, verification, or artifact upload prevents the deploy job from running. GitHub Pages continues serving the last successful deployment.

1. Open the failed workflow run and identify the first failed build step.
2. Fix source failures in `unified-cv`; fix publishing failures here.
3. Merge the repair through the appropriate repository's pull-request flow.
4. Manually dispatch `source_ref=main` and verify the root site.

## Rollback

1. Find the last known-good commit SHA on `unified-cv/main`.
2. Manually dispatch `Publish central CV` with that SHA as `source_ref`.
3. Verify the root HTML and PDF, then record the deployed SHA in the incident or pull request.
4. After the central fix is merged, dispatch `source_ref=main` to resume current releases.

This rollback changes only the deployed artifact; it does not rewrite either repository's history. The last duplicated RenderCV source remains recoverable at root-repository commit `567e78b`, and the pre-RenderCV Jekyll site at `6ddecd1`.
