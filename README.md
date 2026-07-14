# Quibbles Replica

This is my recreation of the Quibbles homepage and About page — just plain HTML and CSS, no frameworks, deployed to GitHub Pages with an automated CI/CD pipeline so it redeploys itself every time I push a change.

**Live site:** https://ab2fresh.github.io/quibbles-replica/

---

## Overview

I wanted to rebuild the Quibbles layout — the header with the logo and avatar, the feed of posts, and the sidebar with the About link — using nothing but static HTML/CSS. Beyond just copying the design, the real point of this project for me was learning the full pipeline: build it locally, push it to GitHub, get it live manually first, then wire up GitHub Actions so it deploys itself on every push.

---

## Project Structure

quibbles-replica/
├── index.html                  # Homepage — header, avatar, post feed, sidebar
├── about.html                  # About Quibbles page
├── styles.css                  # Styling for both pages
├── image/
│   ├── logo.jpeg
│   ├── avatar.jpeg
│   ├── post-founder.jpeg
│   ├── post-visas.jpeg
│   ├── post-stretching.jpeg
│   └── post-teens.jpeg
└── .github/
    └── workflows/
        └── deploy.yml           # Builds and deploys automatically on push to main

A couple of things I made sure to get right:
- Kept all image filenames lowercase and hyphenated — GitHub Pages runs on Linux, which is case-sensitive, so `Logo.jpeg` and `logo.jpeg` aren't the same file there even if they look fine on my own machine.
- Put `about.html` right at the root, not in a subfolder, so the sidebar link is a simple relative path.
- No build step, so the workflow just uploads the files as they are.

---

## How I Built It

1. **Set up the files locally** — wrote out `index.html`, `about.html`, and `styles.css` by hand, and dropped my images into an `image/` folder with names that matched what the HTML expected.
2. **Tested it before touching Git** — checked everything loaded properly in the browser first. Caught a couple of broken image paths this way before they became a bigger headache.
3. **Pushed it to GitHub** — initialized the repo, committed, and pushed to `Ab2fresh/quibbles-replica`.
4. **Got it live manually first** — turned on GitHub Pages under Settings, deploying straight from the `main` branch, just to confirm everything actually worked once it was live.
5. **Added the CI/CD workflow** — wrote `deploy.yml` and switched the Pages source over to GitHub Actions, so pushes trigger a proper build-and-deploy run instead of a static branch snapshot.
6. **Tested that the automation actually worked** — made a small edit, pushed it, and watched the Actions tab kick off a new run on its own. Once it went green, the live site had updated without me touching any settings.

---

## What I Learned

- You really don't need a backend for something like this — HTML, CSS, and a handful of images is enough to get a convincing-looking site running.
- Case sensitivity bit me once — something that looked fine locally broke on GitHub Pages because of a filename casing mismatch. Worth checking early.
- Testing locally before pushing saves a lot of back-and-forth. Broken image paths are way easier to catch on `localhost` than after a deploy.
- "Deploy from a branch" and "GitHub Actions" are not the same thing — one just redeploys a snapshot, the other actually runs a workflow every time you push, which is what I needed for this to count as real CI/CD.
- GitHub doesn't accept your account password for pushes anymore — you need a Personal Access Token instead. Wish I'd known that before my first push failed.
- The Actions tab tells you way more than the live site does. A red X points straight at what broke, usually a permissions setting or a wrong file path.

---

## Running It Locally

```bash
git clone https://github.com/Ab2fresh/quibbles-replica.git
cd quibbles-replica

```



## How Deployment Works

Every push to `main` triggers the GitHub Actions workflow in `.github/workflows/deploy.yml`, which builds and publishes the site automatically. I don't need to manually redeploy anything after the initial setup.
