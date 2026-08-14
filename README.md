# Speedtest with GitHub Actions → GitHub Pages

Runs [sitespeed.io](https://www.sitespeed.io/) every 6 hours via GitHub Actions against a list of URLs, generates an HTML performance report, and publishes it to GitHub Pages.

## How it works

- A scheduled GitHub Actions workflow (`.github/workflows/sitespeed.yml`) runs every 6 hours (`0 */6 * * *`) and can also be triggered manually (`workflow_dispatch`).
- The workflow uses the official `sitespeedio/sitespeed.io` Docker image and tests each URL in `urls.txt` once (`-n 1`) to keep CI minutes low.
- Results are written to `sitespeed-result/` and pushed to the `gh-pages` branch, which is served by GitHub Pages.

## Add a new URL

Open [`urls.txt`](urls.txt) and add one URL per line:

```
https://www.example.com
https://www.wikipedia.org
https://your-site.example
```

Lines starting with `#` are treated as comments and ignored. Commit the change and the next scheduled run (or a manual run) will include it.

## View the report

The published report is available at:

```
https://<your-username>.github.io/<your-repo>/
```

Replace `<your-username>` and `<your-repo>` with your GitHub details, or find the link under **Settings → Pages** after the first run.

## Run manually

Go to the **Actions** tab, select the **sitespeed** workflow, and click **Run workflow**.

## Notes

- Each run overwrites the previous report (latest only) to keep the `gh-pages` branch small. Per-run history can be added later if needed.
- Iterations are kept low (`-n 1`) to stay within the monthly Actions minutes budget. Increase with care.
