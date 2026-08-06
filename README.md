# charlesangelucci.com

Personal academic website. One static file, no build step, no dependencies.

```
index.html    the entire site (markup + styles inline)
CNAME         the custom domain, read by GitHub Pages
.nojekyll     tells GitHub Pages to serve files as-is
```

## Editing

Open `index.html` in any editor. Everything lives in one file:

- **Design tokens** — the `:root` block at the top. Colors, fonts, and layout
  widths are all custom properties; change a value once and it updates
  everywhere, in both light and dark mode.
- **Content** — plain HTML below `<body>`. To add a paper, copy an existing
  `<article class="entry">` block and edit it.

Two spots are marked `PLACEHOLDER` / `PHOTO` in comments and need your input:
the one-line research statement, and the portrait.

### Replacing the photo

`photo.jpg` (600×600, 41 KB) sits next to `index.html`. To swap it, overwrite that
file — no markup change needed. Keep it square and compressed; a full-resolution
export straight from a camera will be several megabytes and slow the page down.

The slot is 132×158, so `object-fit: cover` trims the sides of a square source.
If a future photo is off-centre, add `object-position` to the `.portrait` rule:

```css
.portrait { object-position: 50% 30%; }   /* nudge the crop upward */
```

Aim for at least 300px on the short edge so it stays sharp on high-density
displays.

### Adding a paper

```html
<article class="entry">
  <div class="year">2026</div>
  <div>
    <p class="entry-title"><a href="URL">Title of the Paper</a></p>
    <p class="entry-meta">
      with Coauthor Name &middot; <span class="venue">Journal Name</span>
    </p>
    <div class="entry-links">
      <a href="URL">Paper</a>
      <a href="URL">Online appendix</a>
    </div>
  </div>
</article>
```

For an unpublished paper, swap `<span class="venue">` for
`<span class="status is-live">R&amp;R, Journal Name</span>`.

## Publishing

Commit and push to `main`. GitHub Pages redeploys in under a minute.

```sh
git add -A
git commit -m "Update publications"
git push
```

## First-time setup

1. Create a public repo on GitHub named `charlesangelucci.github.io`.
2. Connect and push:

   ```sh
   git remote add origin https://github.com/USERNAME/charlesangelucci.github.io.git
   git branch -M main
   git push -u origin main
   ```

3. In the repo's **Settings → Pages**, set Source to "Deploy from a branch",
   branch `main`, folder `/ (root)`.
4. Buy the domain, then point it at GitHub with these DNS records:

   | Type  | Host  | Value                                                      |
   |-------|-------|------------------------------------------------------------|
   | A     | `@`   | `185.199.108.153`                                          |
   | A     | `@`   | `185.199.109.153`                                          |
   | A     | `@`   | `185.199.110.153`                                          |
   | A     | `@`   | `185.199.111.153`                                          |
   | CNAME | `www` | `USERNAME.github.io`                                       |

5. Put the bare domain in `CNAME` (one line, no protocol), push, then enable
   **Enforce HTTPS** in Settings → Pages once the certificate is issued.
6. Update the `<link rel="canonical">` and `og:url` values in `index.html` to
   the final domain.
7. On the old Google Site, replace the content with a short line pointing here,
   so existing links and search results still lead somewhere useful.
