# Truth Be Told — Deploy Guide

A static site: one landing page + four article pages. No build step, no server. Hosting it on GitHub + Vercel takes about 5 minutes.

## What's in this folder

```
truth-be-told/
├── index.html              ← Landing page
├── articles/               ← The four articles
│   ├── is-your-honey-even-honey.html
│   ├── nmr-tested-isnt-one-thing.html
│   ├── mahabaleshwars-bee-village.html
│   └── the-mouli-and-the-tiger.html
├── assets/
│   └── logo.png            ← Top-left logo
└── README.md               ← This file
```

You can open `index.html` in your browser right now to preview locally.

---

## Step 0 — One-time cleanup (30 seconds)

Before pushing, drag these to the Trash from Finder. They're leftover files from work-in-progress that don't belong in the live site:

- `truth-be-told/.article-backups/` (entire folder)
- `truth-be-told/assets/covers/` (entire folder)
- `truth-be-told/Truth be told logo/` (entire folder — the logo already lives at `assets/logo.png`)
- `truth-be-told/articles/.test_write` (if you see it — it's hidden, so enable hidden files: `Cmd + Shift + .` in Finder)
- `truth-be-told/articles/newfile.txt`
- `truth-be-told/.DS_Store` (also hidden — macOS metadata, harmless but tidy to remove)

After cleanup the folder should contain only: `index.html`, `articles/`, `assets/`, `README.md`.

---

## Step 1 — Sign up if you don't already have accounts

1. **GitHub** — go to [github.com/signup](https://github.com/signup) and create an account. Free.
2. **Vercel** — go to [vercel.com/signup](https://vercel.com/signup) and click **Continue with GitHub**. This connects your Vercel account to your GitHub one. Free.

You'll do both with the same email if possible.

---

## Step 2 — Put the files on GitHub

Two paths. **Pick A if you've never used the command line**, pick B if you have.

### Path A — Drag and drop (no command line)

1. Go to [github.com/new](https://github.com/new).
2. Under **Repository name**, type `truth-be-told`.
3. Choose **Public** (Vercel's free tier works easiest with public repos).
4. **Do not** tick "Add a README" or any other checkbox — you already have a README.
5. Click the green **Create repository** button.
6. On the next page you'll see "Get started by creating a new file or **uploading an existing file**". Click **uploading an existing file**.
7. Open Finder. Open the `truth-be-told` folder. Select **everything inside** it (Cmd + A) — `index.html`, the `articles` folder, the `assets` folder, and `README.md`. Drag all of them into the GitHub upload area in your browser.
8. Wait a few seconds for the upload to finish. The 4 article files are about 1 MB each.
9. Scroll down. In the **Commit changes** box, leave the default message ("Add files via upload") or type something like `Initial commit`.
10. Click the green **Commit changes** button.

Done — refresh the repo page and you should see `index.html`, `articles/`, `assets/`, `README.md`.

### Path B — Command line (if you have git installed)

Open Terminal, navigate to the `truth-be-told` folder, then run these one at a time:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/truth-be-told.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username. Before running the last line, create the empty repo on github.com/new (don't tick anything — same as steps 1–5 of Path A).

---

## Step 3 — Deploy on Vercel

1. Go to [vercel.com/new](https://vercel.com/new).
2. You'll see a list called **Import Git Repository** with your GitHub repos. Find `truth-be-told` and click the **Import** button next to it.
   - If you don't see it, click **Adjust GitHub App Permissions** at the top, grant Vercel access to the repo, and come back.
3. On the configure screen:
   - **Project Name** — leave as `truth-be-told` (or change it; this becomes part of your URL)
   - **Framework Preset** — leave as **Other**. Vercel auto-detects plain HTML; nothing to configure.
   - **Root Directory** — leave as `./`
   - **Build and Output Settings** — leave empty. No build command needed.
   - **Environment Variables** — none.
4. Click the big **Deploy** button.
5. Wait ~30 seconds. You'll see a confetti animation and a preview screenshot.
6. Click **Continue to Dashboard** or click on the preview to open your live site. The URL looks like `https://truth-be-told-yourname.vercel.app`.

That's it — your site is live on the public internet.

---

## Step 4 (optional) — Custom domain

If you want it on your own domain (e.g. `truthbetold.in`) instead of the `.vercel.app` URL:

1. In Vercel, open your project, then click **Settings** at the top, then **Domains** in the left sidebar.
2. Type your domain in the **Add** field and click **Add**.
3. Vercel shows you two or three DNS records (A or CNAME) to add at your domain registrar (GoDaddy, Namecheap, Cloudflare, wherever you bought the domain).
4. Log into your registrar, find DNS settings for that domain, and add the records exactly as Vercel shows.
5. Back in Vercel, click **Refresh**. Within 5–60 minutes (usually fast) it goes green and your domain points to the site.

---

## Updating the site later

Two paths again, matching how you uploaded.

**If you used Path A (drag-and-drop):**

1. Edit the file on your computer.
2. Go to your GitHub repo, click the file you changed, click the pencil icon (top right of the file viewer), paste your updated content (or for binary files like images, delete the file and re-upload the new one).
3. Scroll down, click **Commit changes**.
4. Vercel sees the commit and redeploys within ~30 seconds.

Or: re-do the upload — go to the repo, click **Add file** → **Upload files**, drag the changed files in, and commit. GitHub will overwrite the old versions.

**If you used Path B (git CLI):**

```bash
git add .
git commit -m "Describe what you changed"
git push
```

Vercel redeploys automatically on push.

---

## Troubleshooting

**"My site shows but the articles 404."**
GitHub didn't upload the `articles/` folder, or the names don't match. Open the repo on github.com and confirm you see an `articles/` folder containing all four `.html` files with the exact same filenames as in `index.html`.

**"The logo is missing."**
Same idea — confirm `assets/logo.png` exists in the GitHub repo. If it's there but the page still shows a broken image icon, check that `index.html` references it as `assets/logo.png` (case-sensitive — `Assets/Logo.PNG` will not work on Vercel even if it worked on your Mac).

**"Vercel says my repo isn't visible."**
On vercel.com/new, click **Adjust GitHub App Permissions** (top right of the import list). On the GitHub page that opens, scroll down to **Repository access**, select **All repositories** or pick `truth-be-told` specifically, save, then go back to Vercel.

**"I want to change the Subscribe / Sign in links."**
Open `index.html`, search for `href="#"` — there are two of them on the Subscribe button and Sign in link. Replace `#` with your Substack URL (e.g., `https://tbthealth.substack.com/subscribe`). Save, commit, push. Vercel redeploys.
