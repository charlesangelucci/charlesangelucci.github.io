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

Everything is in `index.html`: a short `<style>` block at the top, then plain
HTML. The design is deliberately plain (one serif font, blue links, no
animation, no dark mode) so it reads like an ordinary academic homepage.

### Adding a paper

Copy an existing `<li>` inside a `<ul class="papers">` list and edit it. Papers
live in three groups, in this order: Work in Progress, Working Papers,
Publications.

```html
<li>
  <a class="paper-title" href="URL">Title of the Paper</a>, with <a href="URL">Coauthor Name</a>.<br>
  <em>Journal Name</em>, 16(2), May 2026, 62&ndash;102.<br>
  <span class="links">
    <a href="URL">Journal</a> &middot;
    <a href="URL">Working paper</a>
  </span><br>
  <span class="press">Press: <a href="URL">Outlet</a></span>
  <details>
    <summary>Abstract</summary>
    <p>Abstract text.</p>
  </details>
</li>
```

Every line below the title is optional; delete it (and the `<br>` before it)
rather than leaving it empty. For an unpublished paper, replace the journal
line with a status, e.g. `Revise and resubmit, <em>Journal Name</em>.<br>`.

Use `&rsquo;` and `&mdash;` rather than pasting curly quotes and dashes directly.

When you change anything, update the date in the footer:

```html
<footer>Last updated September 2026.</footer>
```

### Updating the CV

Overwrite `angelucci-cv.pdf`, then change the date beside the download link:

```html
<a href="angelucci-cv.pdf">CV</a> (April 2026)
```

### Replacing the photo

Overwrite `photo.jpg` — no markup change needed. The photo is shown at its own shape (currently 5:6), so crop it before saving.

To resize the portrait, change `width` in the `.portrait` rule (150px on
desktop; the phone size is set in the `max-width: 30rem` block).

## Search engines

The site is indexable — there is no `robots` meta tag. To take it back out of
search results, add this inside `<head>`:

```html
<meta name="robots" content="noindex">
```
