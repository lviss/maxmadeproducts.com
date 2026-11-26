# Project agent memory

This file is the project's committed home for project-intrinsic agent knowledge: build, test, release, architecture, and sharp-edge notes that should travel with the code.

- Add durable project-specific notes here as they are discovered through real work.

## Stack

Hugo static site (theme: PaperMod, vendored as a git submodule at `themes/papermod` — run
`git submodule update --init --recursive` after cloning). Deploys to GitHub Pages via
`.github/workflows/hugo.yml` on every push to `main` (or manual `workflow_dispatch`); that
workflow has no `pull_request` trigger, so PR branches never get a build/deploy run — only a
merge to `main` triggers a real deploy.

- `resources/` is a pure Hugo image-processing cache (hashed filenames under `resources/_gen/`)
  with nothing hand-authored in it — it's fully gitignored, along with `/public/` (build output)
  and `.hugo_build.lock`.
- `static/CNAME` (containing exactly `maxmadeproducts.com`) is what makes GitHub Pages keep
  the custom domain across each rebuild — don't delete it.
- DNS for `maxmadeproducts.com` is outside this repo.
- The repo's GitHub PAT cannot enable Pages itself: `POST .../pages` 403s with "Insufficient
  permissions for this action" (a plain `GET` on an already-enabled repo's Pages settings does
  work, so this is specifically an enable/write limitation). Enabling Pages (Actions build type +
  custom domain) currently has to be done by a human in the GitHub UI, or the token needs broader
  permissions.
- `.github/workflows/strip-image-metadata.yml` runs on every `pull_request` (including the
  README's GitHub-web-UI upload flow, which skips any local git client entirely). It diffs new/
  changed `*.jpg`/`.jpeg`/`.png`/`.webp`/`.tif`/`.tiff` files against the PR base, runs
  `mogrify -auto-orient -strip` on each (physically rotates pixels per the EXIF orientation tag
  before dropping it, so stripping never visually re-rotates a portrait phone photo), and commits
  the cleaned files straight back onto the PR branch with the workflow's own `GITHUB_TOKEN` — the
  raw file committed to the repo is the actual leak vector (downloadable from the repo or its git
  history regardless of how Hugo resizes/re-encodes it for display), so Hugo's own image
  processing is not a substitute for this. Only works for same-repo PR branches, which is the only
  path the README documents; it deliberately skips (rather than fails) PRs from a fork of this
  repo, since a fork's PR gets a read-only `GITHUB_TOKEN` that can't push back — a maintainer
  would need to strip a forked PR's images by hand before merging.

## Maintaining this file

Keep this file for knowledge useful to almost every future agent session in this project.
Do not repeat what the codebase already shows; point to the authoritative file or command instead.
Prefer rewriting or pruning existing entries over appending new ones.
When updating this file, preserve this bar for all agents and keep entries concise.
