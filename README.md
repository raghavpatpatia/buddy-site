# Buddy site

A small static website for the Buddy Android app (`com.raghav.buddy_app`): a home page, the privacy policy and the
account-deletion page that Google Play asks for. It is plain HTML and CSS with no build step, so GitHub Pages
serves the files exactly as they are.

| File | What it is |
|---|---|
| `index.html` | A short intro to the app, with links |
| `privacy.html` | Privacy policy |
| `delete-account.html` | How to delete the account and its data (in the app and by email), what is deleted, and how long it takes |
| `app-ads.txt` | The AdMob publisher line (see the note below, because it must be at the root of a domain) |
| `style.css`, `icon.png` | The look (Buddy's Acid / Holo Pop colours, light and dark) and the app icon |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## Publish with GitHub Pages

1. Create a **public** repository on GitHub, for example `buddy` (a free account can only publish Pages from a
   public repository).
2. Push this folder to it:
   ```sh
   cd ~/Documents/buddy-site
   git init -b main
   git add .
   git commit -m "Buddy site"
   git remote add origin https://github.com/<username>/<repo>.git
   git push -u origin main
   ```
   Or with the GitHub CLI: `gh repo create <repo> --public --source . --push`.
3. On GitHub, open the repository, then **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a
   branch**, then branch **main** and folder **/ (root)**, and click **Save**.
4. After a minute or two, the site is live at `https://<username>.github.io/<repo>/`. Open each page on your phone
   to check it.

To update the site, edit the files, then commit and push again. The pages update within a minute or two.

## URLs for Play Console

With the site at `https://<username>.github.io/<repo>/`:

| Play Console field | URL |
|---|---|
| **Privacy policy** (App content → Privacy policy, and the store listing) | `https://<username>.github.io/<repo>/privacy.html` |
| **Delete account URL** (App content → Data safety → Data deletion) | `https://<username>.github.io/<repo>/delete-account.html` |
| Website (Store settings → Store listing contact details), optional | `https://<username>.github.io/<repo>/` |

For example, if the user is `raghavpatpatia` and the repository is `buddy`, the privacy policy URL is
`https://raghavpatpatia.github.io/buddy/privacy.html`.

## app-ads.txt must be at a domain root

AdMob only looks for `app-ads.txt` at the **root** of the developer website's domain, for example
`https://raghavpatpatia.github.io/app-ads.txt`. A copy inside a project site such as
`https://raghavpatpatia.github.io/buddy/app-ads.txt` is **not** found. Choose one of these:

- **Simplest:** name the repository `<username>.github.io`. The site is then served at the domain root
  (`https://<username>.github.io/`, with `privacy.html` and `delete-account.html` next to it), and `app-ads.txt`
  works as it is. Use those root URLs in Play Console instead of the `/<repo>/` ones above.
- **Or** keep this as a project site, and put `app-ads.txt` in a separate `<username>.github.io` repository
  (it can contain only that file). Set the Play listing's **Website** to `https://<username>.github.io/`.

Either way, the Website field in the Play listing must be the domain where `app-ads.txt` lives. Then, in AdMob, go to
**Apps → View all apps → app-ads.txt** to check it. AdMob may take a day or more to crawl the file.

## Before you publish

- Every page shows the contact email `raghav.patpatia@gmail.com`. A public site makes it visible to everyone.
- The deletion page promises to handle email requests within 30 days, and the privacy policy promises to answer
  data requests within 30 days. Keep those promises, or change the text.
- The in-app **Delete account** button calls the `deleteAccount` Cloud Function. Deploy it before release, and test
  it with a spare Google account.
- Update the "Last updated" date in `privacy.html` whenever what the app does with data changes.
