# Harris Bienn CV

This repository is the source for [harrisbienn.github.io](https://harrisbienn.github.io). One validated YAML file drives the public website, printable PDF, and Markdown export.

## Source of truth

Edit `cv/Harris_Bienn_CV.yaml`. Do not edit generated files in `dist/`.

RenderCV 2.8 provides the schema, validation, and document renderers. The custom template at `cv/html/Full.html` wraps RenderCV's HTML output in the portfolio layout. Client-side enhancements turn professional experience and education and training into collapsed vertical timelines, present specialties as a Shields.io-enhanced capability grid, and load live GitHub project cards. All professional content remains available without JavaScript or third-party badge assets.

## Build

The project uses a container so the host does not need Python, Typst, RenderCV, or their dependencies.

```sh
make build
make verify
```

Set `CONTAINER_ENGINE=podman` when Podman is preferred over Docker.

Open `dist/index.html` after a successful build. The output directory also contains `Harris_Bienn_CV.pdf`, `Harris_Bienn_CV.md`, and the intermediate Typst file.

## Content review

The first normalized draft intentionally omits street address, phone number, and references from the public source. Editorial discrepancies and suggested next updates are tracked in `docs/content-review.md`.

## Deployment

The GitHub Actions workflow validates pull requests and deploys pushes to `master` through GitHub Pages. GitHub Pages must use GitHub Actions as its deployment source. The generated `dist/` directory is uploaded as an artifact and is never committed.

The previous Jekyll site remains recoverable from the repository history. See `docs/migration.md` for the cutover checklist and rollback point.
