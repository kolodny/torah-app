# torah-app — publisher for [torah-llm](https://github.com/kolodny/torah-llm)

This repo only **publishes**. The app and the multi-source ingest pipeline live in **torah-llm**
(the source of truth). On a schedule (or manual run), the GitHub Action here:

1. clones `torah-llm`,
2. regenerates the corpus from the pinned sources (`npm run data`),
3. builds the published subset that fits under GitHub Pages' 1 GB limit
   (`npm run publish:db` — Sefaria he+en, excluded categories dropped; configured in
   `torah-llm/ingest/build-publish-master.ts`),
4. builds the app at the project base path (`PAGES_BASE=/torah-app/`) and deploys it via the
   GitHub Pages **Actions artifact**.

No SQLite corpus is ever committed to either repo — not in `main`, not in a `gh-pages` branch.

## One-time setup

- **Settings → Pages → Build and deployment → Source = "GitHub Actions"**
  (replaces the old "deploy from a branch"; the old `gh-pages` branch can be deleted).
- Then run the workflow: **Actions → Deploy to GitHub Pages → Run workflow**.

## Tuning what's published

Edit `ingest/build-publish-master.ts` in **torah-llm** (`SOURCES`, `LANGS`,
`EXCLUDE_TOP_CATEGORIES`) and re-run the workflow.
