# Seller Performance Dashboard

Interactive portfolio demo by Jiaxin Hu. All names, IDs, transaction values
and assessment thresholds are synthetic.

## Preview

Open index.html in a browser. This single file contains the HTML, CSS and
JavaScript; it does not need Python, npm, a database or company access.

## Publish with GitHub Pages

1. Extract this ZIP and upload its contents to a public GitHub repository.
2. Commit the files to the main branch.
3. Go to Settings > Pages.
4. Under Build and deployment, choose Deploy from a branch.
5. Select main and /(root), then Save.
6. When deployment finishes, use the website URL shown in Pages settings.

For an existing repository, these files can instead go into docs/; then select
/docs in Pages settings. Preserve any existing website configuration.

Uploading the ZIP itself will not deploy its contents. Upload the extracted
index.html, README.md and .nojekyll files.

## Project background

This static site recreates the main interactions of an original Python/Dash
seller dashboard: group/entity/seller/account navigation, monthly and YTD
filters, 14 metrics, account drill-down and CSV exports. The Project story
page explains the original Pandas/SQL data pipeline. The demo uses browser
JavaScript and deterministic fixtures; it does not run the original backend
or the company assessment rules.

Original scripts and internal data are not included in this package.

Official instructions:
https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
