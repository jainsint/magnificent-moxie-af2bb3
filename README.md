# Jains Internationnal — Website

Static website for Jains Internationnal (wovenwear manufacturing, Salem). No build step, no server code — just HTML, one tiny JS helper, and images. Any static host serves it.

```
.
├── index.html          ← homepage
├── support.js          ← runtime for the homepage (don't edit)
├── image-slot.js       ← image helper (don't edit)
├── .nojekyll           ← tells GitHub Pages to serve every folder as-is (keep it)
├── assets/             ← shared images (article covers, etc.)
└── insights/           ← the blog
    ├── index.html                       ← the article list page
    ├── understanding-fabric-weight-gsm.html   ← a published article
    └── _TEMPLATE-article.html           ← copy this to write a new article
```

---

## Going live (GitHub Pages)

1. Create a repo on GitHub and put **the contents of this folder** at the repo root (so `index.html` is at the top level).
2. Repo → **Settings → Pages**.
3. Under *Build and deployment*, set **Source: Deploy from a branch**, pick your branch (`main`) and folder **`/ (root)`**, then **Save**.
4. Wait ~1 minute. Your site is live at `https://<your-username>.github.io/<repo-name>/`.

Every time you `git push`, GitHub Pages re-publishes automatically — that's your publishing button.

> Using a custom domain (e.g. `www.jainsint.com`)? In Settings → Pages add the domain, then create a file named `CNAME` at the repo root containing just the domain. Point your DNS to GitHub per their docs.

---

## Publishing a new article — step by step

Three small edits, then push. No coding beyond filling in text.

### 1. Create the article file
- Copy `insights/_TEMPLATE-article.html` and rename it to a short, lowercase, hyphenated name describing the topic — this becomes the URL.
  Example: `insights/choosing-the-right-weave.html`
- Open it and fill in the 7 spots marked `EDIT 1` … `EDIT 7` (title, description, category, headline, author/read-time, hero image, body). Each is labelled with an HTML comment.

### 2. Add the hero / cover image
- Drop your image into the `assets/` folder (e.g. `assets/choosing-the-right-weave.jpg`).
- In the new article, set the hero `src` to `../assets/choosing-the-right-weave.jpg` (EDIT 6).
- Keep images reasonably sized (under ~400 KB, ~1600px wide is plenty) so pages load fast.

### 3. Add it to the article list
Open `insights/index.html`. Find the block that starts with `<!-- POST 1 -->`. Copy the whole `<article>…</article>` block, paste it directly above the `<!-- PLACEHOLDER: more posts land here -->` line, and update these four things in the copy:

- the cover image `src` → `../assets/your-image.jpg`
- the headline link `href` (appears twice — the `<h2>` link and the "Read →" link) → `your-file-name.html`
- the headline text
- the short summary line and the read-time

(When you have several posts, you can delete the dashed "More guides coming soon" placeholder box.)

### 4. (Optional) Feature it on the homepage
The homepage shows one featured article near the bottom. To swap which one is featured, open `index.html`, search for `understanding-fabric-weight-gsm.html`, and update that card's link, image and text the same way.

### 5. Publish
```bash
git add .
git commit -m "New article: choosing the right weave"
git push
```
Live in about a minute.

---

## Quick local preview
Double-clicking `index.html` works for a quick look, but links between pages behave best over a tiny local server:
```bash
python3 -m http.server
# then open http://localhost:8000
```

## Notes
- Fonts load from Google Fonts, so the live site needs internet (every normal host has it).
- All catalogue product photos are embedded directly in `index.html`, so there are no missing-image surprises after deploy.
- Don't edit `support.js` or `image-slot.js`.
