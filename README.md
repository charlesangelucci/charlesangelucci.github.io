# charlesangelucci.github.io

Personal academic website. One static file, no build step, no dependencies, no
domain to renew.

```
index.html                                 the entire site (markup + styles inline)
photo.jpg                                  portrait, 600x720
angelucci-cv.pdf                           the CV
appendix-journalistic-truth.pdf            online appendices, served from here
appendix-multi-project-collaborations.pdf    so the links cannot rot
appendix-beliefs-political-news.pdf
.nojekyll                                  tells GitHub Pages to serve files as-is
```

The *Media Competition and News Diets* appendix is deliberately **not** here — it
is 32 MB, which would sit in git history forever. That one link still points at
Google Drive, and is the only external file the site depends on. If its sharing
permission ever changes, that link breaks silently.

## Publishing

Commit and push to `main`. GitHub Pages redeploys in under a minute.

```sh
git add -A
git commit -m "Update publications"
git push
```

The live site is <https://charlesangelucci.github.io>. Pages is already
configured (source `main`, folder `/`, HTTPS enforced) — nothing to set up.

## Editing

Everything is in `index.html`:

- **Design tokens** — the `:root` block at the top. Colours, fonts, and layout
  widths are custom properties; change one value and it updates everywhere, in
  both light and dark mode.
- **Content** — plain HTML below `<body>`.

### Adding a paper

Copy an existing `<article class="entry">` block and edit it. Papers live in
three groups, in this order: Work in Progress, Working Papers, Publications.

```html
<article class="entry">
  <div class="year">2026</div>
  <div>
    <p class="entry-title"><a href="URL">Title of the Paper</a></p>
    <p class="entry-meta">
      with <a href="URL">Coauthor Name</a><br>
      <span class="venue">Journal Name</span>
      <span class="cite">16(2), May 2026, 62&ndash;102</span>
    </p>
    <details class="abstract">
      <summary>Abstract</summary>
      <p>Abstract text.</p>
    </details>
    <div class="entry-links">
      <a href="URL">Journal</a>
      <a href="URL">Working paper</a>
    </div>
    <p class="entry-coverage">Coverage: <a href="URL">Outlet</a></p>
  </div>
</article>
```

Every part below the title is optional — omit the whole element rather than
leaving it empty. For an unpublished paper, replace `<span class="venue">` with
`<span class="status is-live">R&amp;R, Journal Name</span>`.

Use `&rsquo;` and `&mdash;` rather than pasting curly quotes and dashes directly.

### Updating the CV

Overwrite `angelucci-cv.pdf`, then change the date beside the download link:

```html
<span class="note">(PDF, April&nbsp;2026)</span>
```

### Replacing the photo

Overwrite `photo.jpg` — no markup change needed. The slot is 5:6 and the current
file matches that ratio exactly, so nothing is cropped. A source of a different
shape will be centre-cropped by `object-fit: cover`; if the result is badly
framed, either crop it to 5:6 before saving or nudge it:

```css
.portrait { object-position: 50% 30%; }   /* shift the crop upward */
```

To resize the portrait, change one value in `:root`:

```css
--portrait-w: 170px;   /* height follows automatically at 5:6 */
```

The phone size is set separately in the `max-width: 40rem` block. Going much
beyond 170px means re-exporting the photo larger than 600px wide.

## Search engines

`index.html` carries a `noindex` tag near the top, marked `LAUNCH STEP`. While it
is there, the site is reachable but will not appear in search results. Delete
that one line to be indexed.
