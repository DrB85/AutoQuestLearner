# AutoQuestLearner — GitHub Pages site

This is a static one-page site for the **AutoQuestLearner** WoW addon. It's plain HTML/CSS (no build step) so it works with GitHub Pages out of the box.

## Publish it

1. Create a new GitHub repo (e.g. `AutoQuestLearner`).
2. Copy everything in this folder into the repo root:
   - `index.html`
   - `assets/img/*.png`
   - `downloads/AutoQuestLearner.zip`
   - `README.md`
3. Commit and push to the `main` branch.
4. In the repo, go to **Settings → Pages**, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`, then Save.
5. Your site will be live at `https://<your-username>.github.io/<repo-name>/` within a minute or two.

## Updating the addon download

The **Download v2.0** button on the page points to `downloads/AutoQuestLearner.zip`. To ship a new version:
1. Replace `downloads/AutoQuestLearner.zip` with the new zip (keep the same filename, or update the link in `index.html`).
2. Update the version number in the hero button text and the footer in `index.html`.

## Notes

- The "View on GitHub" link in the top nav currently points to a placeholder (`https://github.com/`) — update it to your actual repo URL once it's created.
- Icons in `assets/img/` were converted from the addon's original `.tga` files to `.png` for web display; the in-game addon itself still ships its original `.tga` files unchanged.
