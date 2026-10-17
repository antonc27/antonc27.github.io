# Fork website

This is a self-contained static site for `https://ac27.github.io/iliberated/`.
It adapts the original home, free games, compatibility, and privacy pages. No
JavaScript, package installation, compilation, or Cargo commands are needed.

## Files and maintenance

- `index.html`: home page. `home.html` forwards the old local entry point here.
- `free_games.html`, `compat.html`, and `privacy.html`: the other pages.
- `assets/style.css`: shared layout and the app icon's navy/mint/white palette.
- `assets/icon.svg` and `assets/icon.png`: copies of `res/icon.svg` and
  `res/icon.png`, licensed under MPL-2.0. Copy them again if the app icon changes.
- `.nojekyll`: marks the site as plain static files.

Navigation and assets use relative URLs, so they work under the `/iliberated/`
project path as well as in a local preview. The canonical and Open Graph URLs
use the requested public address. There is no custom domain or `CNAME` file.
The visible name is `iLibirated`, as requested; the native app remains iLiberated.

Source and issue links use `https://github.com/antonc27/iliberated`, the public
project address documented in the repository's main README. Hosting this site
under `ac27` does not change those source links. If the source repository moves,
update the source, issues, and license links in all four pages. Links to free
games retain the actual upstream repositories.

The privacy policy retains the original app policy, with the new name and
support address, and adds a separate explanation of GitHub Pages hosting and
support correspondence. Keep it aligned with the app's actual data practices.

## Preview locally

From the repository root:

```sh
python3 -m http.server 8000 --directory site
```

Open `http://localhost:8000/`. Check all four pages at desktop and mobile widths.
For a project-path preview, put a copy of `site` in a temporary directory named
`iliberated` and serve its parent; visit `http://localhost:8000/iliberated/`.

## Deploy later to GitHub Pages

The workflow in `.github/workflows/site-pages.yml` is **manual only**. It has no
push or pull-request trigger. No deployment has been run as part of these changes.

1. Put these changes in the **`ac27/iliberated`** repository. GitHub Pages derives
   the default hostname from the repository owner, so this owner/repository pair
   is required for `ac27.github.io/iliberated`. Publishing from a different owner
   produces that owner's hostname instead. The repository must have GitHub Pages
   available on its plan; public repositories can use it on GitHub Free.
2. Ensure `.github/workflows/site-pages.yml` exists on that repository's default
   branch so GitHub displays its manual **Run workflow** control. The selected
   deployment branch must also contain the workflow and the completed `site` folder.
3. In the repository, open **Settings → Pages → Build and deployment**. Set
   **Source** to **GitHub Actions**. Do not select “Deploy from a branch”: that
   mode cannot directly serve `/site` (it only supports the root or `/docs`).
4. When ready to publish, open **Actions → Deploy site to GitHub Pages → Run
   workflow**. Select the branch containing the finished site and run it. If the
   `github-pages` environment has branch restrictions or required reviewers,
   allow that branch and approve the deployment when prompted.
5. Wait for the workflow to finish. Open **`https://ac27.github.io/iliberated/`**
   and check navigation, images, free game links, and the support email on mobile
   and desktop. The workflow's environment link also shows the deployed URL.

The workflow uploads only `site` and deploys it directly, without building the
emulator or fetching submodules. For later updates, save the site changes and
manually run the same workflow again. To preview or review without publishing,
leave the workflow unrun.
