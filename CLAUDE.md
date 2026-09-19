# Blog (rushout09.github.io)

Read the Notion page "Working Context (read me first)" before working in this repo, and follow it.

Rushabh's personal blog, the "blog repo" in the Content workflow of `~/Repos/working-area/CLAUDE.md`. Long-form posts here are the source, and LinkedIn and X posts are extractions from them. The voice rules live in that Content workflow section, so read it before drafting.

## How it publishes

- A GitHub Pages site, built from branch `master`, path `/`, by GitHub itself (legacy Jekyll build, theme `jekyll-theme-slate`). Pushing to `master` publishes. Live at https://rushout09.github.io/.
- There is no Gemfile and no local Jekyll on the Mac, so there is no local preview. Check a change on the live site after the push.
- Never push unless Rushabh asks.
- `_config.yml` sets `future: true`, so a post dated in the future is published immediately.

## Where things are

- `_posts/YYYY-MM-DD-slug.md`: published posts. The date comes from the filename, and the URL is `/YYYY/MM/DD/slug.html`.
- `_drafts/`: unpublished writing. GitHub Pages does not build it.
- `_layouts/default.html`: the one layout, with the header, footer and social links.
- `index.md`: the home page, with the quotes and the post list (newest first, with excerpts).
- `assets/images/`: images.

## Writing a post

- Front matter is just `title`:

  ```
  ---
  title: "Post title"
  ---
  ```

  A post without front matter still builds, with its title taken from the filename.
- Publish by adding the file to `_posts`. Unpublish by moving it to `_drafts` with `git mv` and keeping the date prefix, so the original date survives if it goes back.
- No em-dashes in anything new. Several older posts contain them; leave those as they are unless Rushabh asks.
