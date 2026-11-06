# DiceFlick website (GitHub Pages)

This folder is the public website App Store Connect needs for DiceFlick:

| File | Purpose | App Store Connect field |
|---|---|---|
| `index.html` | Landing and support page (features, FAQ, contact) | **Support URL** |
| `privacy.html` | Privacy policy | **Privacy Policy URL** |
| `icon.png` | App icon (256 px), used as favicon and hero image | n/a |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is, without Jekyll | n/a |

It is plain HTML with no build step and no external resources (fonts, scripts, analytics). Both pages support light and dark mode and work at phone width.

## 1. Before publishing

1. Replace **every** `[TODO: your-email@example.com]` with a real contact address. It appears in `index.html` (Support section) and `privacy.html` (Contact section). Check that none are left:
   ```sh
   grep -n "TODO" index.html privacy.html
   ```
2. Open both files in a browser and read them once.

## 2. Create a public repo and push

Use a **separate, public** repository such as `diceflick-site`. GitHub Pages on a free account only serves public repos, and keeping the site separate means the app's source code never has to be public.

No `gh` CLI was found on this Mac when this README was written, so the steps below use the GitHub website and plain `git`. Replace `ayushp2400` with your GitHub username.

1. Go to <https://github.com/new>.
   - Repository name: `diceflick-site`
   - Visibility: **Public**
   - Do **not** add a README, .gitignore or license (the repo must start empty).
   - Click **Create repository**.
2. Push the contents of this folder (the files must be at the repo root, not inside a `site/` subfolder):
   ```sh
   cd /Users/ayushpathak/Documents/Projects/DiceRoll/site
   git init -b main
   git add index.html privacy.html icon.png .nojekyll README.md
   git commit -m "DiceFlick website"
   git remote add origin https://github.com/ayushp2400/diceflick-site.git
   git push -u origin main
   ```

**Option: GitHub CLI.** If you install the CLI (`brew install gh`) and run `gh auth login`, you can replace step 1 and the last two commands of step 2 with one command, run from this folder after `git commit`:
```sh
gh repo create diceflick-site --public --source . --push
```

## 3. Turn on GitHub Pages

1. In the repo on GitHub, open **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Set **Branch** to `main` and the folder to `/ (root)`, then click **Save**.
4. Wait a minute or two. The Actions tab shows a "pages build and deployment" run, and the Pages settings page shows the live URL when it finishes.

## 4. Your URLs

| Use | URL |
|---|---|
| Support URL | `https://ayushp2400.github.io/diceflick-site/` |
| Privacy Policy URL | `https://ayushp2400.github.io/diceflick-site/privacy.html` |

GitHub Pages lowercases the username in the hostname, so use it in lowercase.

Open both URLs in a private browser window to make sure they load without signing in. Then:

1. In App Store Connect, enter the privacy URL under **App Privacy → Privacy Policy URL** and the support URL on the version page (**Support URL**, next to the description and keywords).
2. In the app, replace the placeholder URL in `DiceFlick/DiceFlick/AppLinks.swift` (`AppLinks.privacyPolicy`, currently `https://example.github.io/diceflick/privacy.html`) with the hosted `privacy.html` URL **before archiving**.

## Updating the site later

Edit the files, then `git commit -am "Update site" && git push`. Pages redeploys automatically. If you change the privacy policy, update the effective date at the top of `privacy.html`.
