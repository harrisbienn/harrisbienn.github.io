# Root-site cutover

## Target architecture

`cv/Harris_Bienn_CV.yaml` is the only CV content source. RenderCV validates it and produces the PDF, Markdown, and HTML outputs. The custom `cv/html/Full.html` template adds the web layout, while `site/assets` supplies progressive enhancement for section navigation, theme preference, and public GitHub projects.

The generated `dist` directory is the GitHub Pages artifact. It is disposable and must not be edited by hand.

## Replacing the legacy site

GitHub reserves the account-root Pages URL for the repository named `harrisbienn.github.io`. This repository now contains the RenderCV-based replacement directly, so the website, PDF, and Markdown export share one content source without a cross-repository deployment credential.

Cutover checklist:

1. Review the replacement pull request without merging it yet.
2. In the repository's Pages settings, select GitHub Actions as the deployment source.
3. Confirm the `github-pages` environment permits deployments from `master`.
4. Merge the replacement pull request into `master`.
5. Run the workflow manually if the merge does not start it automatically.
6. Verify the root URL, PDF download, timelines, specialty badges, and GitHub project cards.

The final legacy commit before the replacement branch is `6ddecd1`. The old Jekyll implementation remains recoverable from that commit and its ancestors.

## Legacy functionality retained

- A browsable HTML CV at the existing account-root URL.
- A printable PDF generated from the same content.
- Vertically scrolling professional-experience and education-and-training timelines with collapsed, expandable details.
- A responsive specialties showcase with optional Shields.io badges and a text fallback.
- Live public GitHub project cards with a resilient profile-link fallback.
- Responsive navigation and a user-selectable light or dark color theme.

The old Jekyll configuration and includes are replaced by RenderCV output and a custom HTML wrapper, eliminating the duplicated CV content previously stored in `_config.yml`.
