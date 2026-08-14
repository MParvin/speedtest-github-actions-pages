Goal: Run sitespeed.io every 6 hours in GitHub Actions against a set of URLs, generate an HTML report, and publish it via GitHub Pages.

Step 1 — Repo structure
.github/workflows/sitespeed.yml
urls.txt (list of URLs to test — user-editable)
README.md
Step 2 — Workflow (sitespeed.yml)
Triggers: schedule with cron every 6 hours (0 */6 * * *) + workflow_dispatch for manual runs
Job on ubuntu-latest
Run sitespeed.io via their official Docker image (sitespeedio/sitespeed.io), outputting to a sitespeed-result/ folder
If multiple URLs, read them from urls.txt and pass them all in a single run
Step 3 — Publish to GitHub Pages
Push the contents of sitespeed-result/ to a separate branch (gh-pages) using an action like peaceiris/actions-gh-pages
Decide: overwrite each run (keep only latest) vs. keep a dated folder per run for history (recommendation: start with "latest run only", add history later if needed)
Step 4 — GitHub Pages settings
Enable Pages on the gh-pages branch (via repo settings, or automatically handled by actions-gh-pages)
Step 5 — Test & document
Trigger once manually via workflow_dispatch and verify output
In README.md, explain how to add a new URL and link to the published site
Notes for the AI Agent
Use the official sitespeed.io Docker image, not a manual npm install (faster, more stable in CI)
Mind Actions minutes: each sitespeed.io run can take several minutes depending on URL count and iterations — keep iterations low (e.g. -n 1 or -n 3) to stay within the monthly budget
Set permissions: contents: write in the workflow for pushing to gh-pages
