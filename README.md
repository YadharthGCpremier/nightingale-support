# Nightingale OS Support Site

A small static support page for the iOS app **Nightingale OS** (Apple ID 6769794835), published by **The Premier Health Group LLC**. It exists so that App Store reviewers and customer agencies have a public, login-free URL to reach our support information. The site is plain HTML and CSS with no build step, no JavaScript, and no external network requests.

## Files

- `index.html` &mdash; the support page itself
- `netlify.toml` &mdash; Netlify config (publish directory and security headers)
- `.gitignore` &mdash; standard ignores

## Local preview

Open `index.html` directly in any browser, or serve the folder with any static file server:

```
python3 -m http.server 8080
```

Then visit `http://localhost:8080`.

## Deploy to Netlify

1. **Push this repo to GitHub.** See the commands at the bottom of this file.
2. In the **Netlify dashboard**, click **"Add new site"** &rarr; **"Import an existing project"** &rarr; **"Deploy with GitHub"**, and authorize Netlify if prompted.
3. Select the `nightingale-support` repository.
4. On the build settings screen:
   - **Build command:** leave blank
   - **Publish directory:** `.`
5. Click **Deploy site**. Netlify will assign a URL like `https://<random-name>.netlify.app`.
6. *(Optional)* Add a custom domain such as `support.premierhealthgroup.health`:
   - In Netlify go to **Site configuration** &rarr; **Domain management** &rarr; **Add a domain**.
   - Enter `support.premierhealthgroup.health` and follow the verification flow.
   - At your DNS provider, create a `CNAME` record for `support` pointing to your Netlify site (e.g. `<your-site>.netlify.app`).
   - Netlify will automatically issue a Let's Encrypt TLS certificate once DNS resolves.

## Use as the App Store Support URL

Paste the live URL into **App Store Connect** &rarr; **Nightingale-os** &rarr; the version page &rarr; **Support URL** &rarr; **Save**.

## Initial git setup

```
cd /Users/premierhealthgroup/projects/support-url
git init
git add .
git commit -m "feat: initial Nightingale OS support page"
gh repo create nightingale-support --public --source=. --remote=origin --push
```
