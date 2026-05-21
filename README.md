# Nightingale OS Support Site

A small static support page for the iOS app **Nightingale OS** (Apple ID 6769794835), published by **The Premier Health Group LLC**. It exists so that App Store reviewers and customer agencies have a public, login-free URL to reach our support information. The site is plain HTML and CSS with no build step, no JavaScript, and no external network requests.

## Files

- `index.html` &mdash; the public support page (served at `/`)
- `privacy.html` &mdash; Privacy Policy (served at `/privacy`)
- `terms.html` &mdash; Terms of Service (served at `/terms`)
- `styles.css` &mdash; shared stylesheet for all three pages
- `netlify.toml` &mdash; Netlify config (publish directory and security headers)
- `.gitignore` &mdash; standard ignores

## Legal pages &mdash; action required before App Store submission

`privacy.html` and `terms.html` are baseline drafts written for a HIPAA-bound B2B home-health workforce SaaS. They cover the structure App Store Review expects (scope vs. BAA, data collection, sharing, retention, security, governing law) but they are **not** a substitute for review by your own counsel.

Before you paste the live URL into App Store Connect's required **Privacy Policy URL** field, have legal:

- Confirm the state of incorporation in section 10 of `terms.html` (currently set to **Maryland** based on the 240 area code &mdash; change if Premier Health Group LLC is registered elsewhere).
- Confirm the categories of information in section 2 of `privacy.html` match what the app and platform actually collect.
- Confirm the security claims in section 5 of `privacy.html` (TLS 1.3, AES-256, OAuth 2.0 / OIDC, MFA) are accurate as deployed.
- Confirm the BAA language reflects your standard agreement.

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

## Use in App Store Connect

The site exposes three URLs that map to the three required App Store Connect fields:

| App Store Connect field | URL to paste |
| --- | --- |
| Support URL | `https://<your-site>.netlify.app/` |
| Privacy Policy URL | `https://<your-site>.netlify.app/privacy` |
| Marketing URL *(optional)* | `https://<your-site>.netlify.app/` or your main marketing site |

Set these in **App Store Connect** &rarr; **Nightingale-os** &rarr; the version page (Support URL, Marketing URL) and **App Information** (Privacy Policy URL), then **Save**.

## Initial git setup

```
cd /Users/premierhealthgroup/projects/support-url
git init
git add .
git commit -m "feat: initial Nightingale OS support page"
gh repo create nightingale-support --public --source=. --remote=origin --push
```
