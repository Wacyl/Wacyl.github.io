# wacyl.github.io

Personal site. Built with Jekyll on GitHub Pages; every push to `main`
rebuilds the site. No local toolchain is required.

## Layout

```
_config.yml             site metadata and Jekyll settings
_layouts/default.html   page frame: head, MathJax config, nav, footer
_layouts/post.html      blog post frame
_includes/about.md      homepage introduction (Markdown)
_includes/pub-list.html renders a publication list from a data file
_data/papers.yml        papers and preprints
_data/notes.yml         notes and expository writing
_posts/                 blog posts, one Markdown file each
index.html              homepage
blog/index.html         blog index, generated from _posts/
style.css               stylesheet
papers/ notes/          PDFs referenced from the data files
cv.pdf                  linked from the nav
```

## Adding a paper or note

Append an entry to `_data/papers.yml` or `_data/notes.yml` (newest first).
Only `title` is required.

```yaml
- title: Title of the paper.
  coauthors: A. Person and B. Person
  status: Preprint, 2026.
  pdf: papers/filename.pdf
  arxiv: '2611.01234'
  doi: 10.1000/xyz
  code: https://github.com/...
  abstract: >
    Abstract text. Math is written as $$H^*(X)$$.
```

Place the PDF in `papers/` or `notes/`. Markdown and `$$` math work in every
text field. Values containing `: ` must be quoted.

## Adding a blog post

Create `_posts/YYYY-MM-DD-title.md`. The date sets the post date; the rest of
the filename becomes the URL (`/blog/title/`).

```
---
title: Post title
summary: Optional one-line description shown in the index.
---

Body in Markdown.
```

The blog index is generated. `updated: YYYY-MM-DD` in the front matter adds an
"updated" date to the post header.

### Math

kramdown uses `$$ ... $$` for both inline and display math; single `$` is not
recognized.

- Inline: `$$H^*(X;\Z)$$`
- Display: `$$` alone on the lines before and after the formula.
- Environments (`equation`, `align`, …) go inside a display block:

  ```
  $$
  \begin{align}
    a &= b \\
      &= c.
  \end{align}
  $$
  ```

  `\label` / `\eqref` behave as in LaTeX.

Site-wide macros (`\Z`, `\Q`, `\R`, `\C`) are defined in
`_layouts/default.html`.

### Theorem environments

A paragraph followed by a kramdown attribute line:

```
**Theorem 1.** Statement.
{: .thm}

Argument.
{: .proof}
```

Classes: `thm`, `lemma`, `prop`, `cor`, `defn` (boxed); `remark`, `example`
(rule on the left); `proof` (adds "Proof." and a tombstone). Multi-paragraph
blocks use a `div`:

```
<div class="proof" markdown="1">
First paragraph.

Second paragraph.
</div>
```

## Troubleshooting

Build status is shown under the Actions tab. Common build failures: a YAML
value containing an unquoted `: `, or a post missing the closing `---` of its
front matter.

## Local preview (optional)

```
bundle install
bundle exec jekyll serve
```

Requires Ruby and the `Gemfile` in this repository.
