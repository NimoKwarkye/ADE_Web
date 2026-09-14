# ADE website

Independent static distribution website. No application source, SDK, or build dependency is required.
Publish **dist/** to GitHub Pages. Relative links work for both account and project Pages sites.

## Local preview

```powershell
python -m http.server 8082 --bind 127.0.0.1 --directory dist
```

Open http://127.0.0.1:8082. Use an HTTP server, not file://, to test the web app.
The app uses a scoped service worker to add isolation headers on hosts such as GitHub Pages.
Its first visit may reload once; service workers and WebAssembly threads must be supported.
The landing page itself needs no JavaScript or external services.

## GitHub Pages

1. Create a separate repository, then push the contents of this folder (including .github).
2. Set its default branch to main, or edit the workflow branch trigger.
3. In Settings → Pages, choose GitHub Actions as the source.
4. Push to main or run the Publish website workflow manually.

The included workflow uploads only dist/. No repository name or account URL is embedded.
No GitHub repository has been created and nothing has been published yet.
Workflow reference: https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages

## Updating a release

Copy a built MSI into dist/downloads/ and update the two download links, version and size
in dist/index.html and the application guide in dist/docs/README.md. Recompute SHA256SUMS.txt.
For larger releases you can replace those links with GitHub Release asset URLs instead.
The included MSI is the existing 0.1.0 build from the application, not a newly built installer.

To update the compiled web app, copy ade.js, ade.wasm, ade.data and any generated worker files
into dist/web-app/ as one matching build. Keep this site's index.html and coi-serviceworker.js.
If the upstream shell changes, merge those changes while retaining the service-worker script.
Do not copy the application source into this repository.
To host the web app in a separate GitHub repository, publish dist/web-app there and replace
all three web-app/ links in dist/index.html with its final HTTPS URL.

## Documentation and licenses

The on-page README is a user guide, with a Markdown copy in dist/docs/README.md.
Edit both when changing the guide. The original scientific model README is included as
an additional reference in dist/docs/MODEL-README.md, preserved as supplied.
The isolation helper is coi-serviceworker v0.1.7 (MIT), bundled with its license:
https://github.com/gzuidhof/coi-serviceworker
It is scoped to web-app/ and does not control the landing page or installer downloads.
