# Blog (rushout09.github.io)

Read the Notion page "Working Context (read me first)" before working in this repo, and follow it.

Rushabh's personal blog, the "blog repo" in the Content workflow of `~/Repos/working-area/CLAUDE.md`. Long-form posts here are the source, and LinkedIn and X posts are extractions from them. The voice rules live in that Content workflow section, so read it before drafting.

## How it publishes

- A GitHub Pages site, built from branch `master`, path `/`, by GitHub itself (legacy Jekyll build, theme `jekyll-theme-slate`). Pushing to `master` publishes. Live at https://rushout09.github.io/.
- There is no Gemfile in the repo. A local preview can run from a scratch folder with the `github-pages` gem under Homebrew Ruby (`PAGES_REPO_NWO=rushout09/rushout09.github.io PAGES_DISABLE_NETWORK=1 bundle exec jekyll serve --source <repo>`). Check the live site after a push either way.
- Never push unless Rushabh asks.
- `_config.yml` sets `future: true`, so a post dated in the future is published immediately.

## Where things are

- `_posts/YYYY-MM-DD-slug.md`: published posts. The date comes from the filename, and the URL is `/YYYY/MM/DD/slug.html`.
- `_drafts/`: unpublished writing. GitHub Pages does not build it.
- `_layouts/default.html`: the one layout. Plain single column on a white background, styles inline, footer links to Email, X, YouTube, LinkedIn, GitHub and RSS. It replaces the Slate theme's layout (redesigned 30 Oct 2026); `theme` in `_config.yml` is now unused by the pages.
- `index.md`: the home page, an index. Photo and name, About (Rushabh's own words), then a plain list of links to the subpages (Writing, Photos, Books; add a line there for any new page, e.g. Vlogs).
- `writing.md`: the post list, titles and dates, newest first.
- `photos.md` + `_data/instagram.json` + `assets/instagram/`: a grid of his Instagram posts (instagram.com/rushin_out) with their captions. Updated by hand when he asks: the image comes from `https://www.instagram.com/p/<code>/media/?size=l`, the caption from the post. Captions that are only hashtags are left blank.
- `books.md`: books he is reading, title and author, each linked to Goodreads. No status notes.
- `_config.yml`: site title and description (shown in link previews and the home tab title), the `og-card.png` preview image as the default for every page, and the jekyll-feed (`/feed.xml`, latest 10 posts) and jekyll-sitemap plugins.
- `assets/icons/`: the favicon set (an R on black).
- `_parked-home-sections.md`: sections taken off the home page on 30 Oct 2026 (main quest, side quests, books, quotes, videos), kept unpublished.
- `assets/images/`: images.

- Rushabh writes his own text here. Do not draft site copy or posts unless he asks.

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
