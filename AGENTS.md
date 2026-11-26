# Project agent memory

This file is the project's committed home for project-intrinsic agent knowledge: build, test, release, architecture, and sharp-edge notes that should travel with the code.

- Add durable project-specific notes here as they are discovered through real work.

## Stack

Hugo static site (theme: PaperMod, vendored as a git submodule at `themes/papermod` — run
`git submodule update --init --recursive` after cloning). Deploys to GitHub Pages via
`.github/workflows/hugo.yml` on every push to `main` (or manual `workflow_dispatch`); there is
no `pull_request` trigger, so PR branches never get a CI run — only a merge to `main` triggers
a real deploy.

- `resources/` is a pure Hugo image-processing cache (hashed filenames under `resources/_gen/`)
  with nothing hand-authored in it — it's fully gitignored, along with `/public/` (build output)
  and `.hugo_build.lock`.
- `static/CNAME` (containing exactly `maxmadeproducts.com`) is what makes GitHub Pages keep
  the custom domain across each rebuild — don't delete it.
- DNS for `maxmadeproducts.com` is outside this repo.

## Maintaining this file

Keep this file for knowledge useful to almost every future agent session in this project.
Do not repeat what the codebase already shows; point to the authoritative file or command instead.
Prefer rewriting or pruning existing entries over appending new ones.
When updating this file, preserve this bar for all agents and keep entries concise.
