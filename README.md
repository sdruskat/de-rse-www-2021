## Setup

This site uses the Minimal Mistakes Jekyll template together with the Multiple Languages Plugin.
Due to a [bug](https://github.com/kurtsson/jekyll-multiple-languages-plugin/issues/186) in the latter, and due to how the template works, auto-deploying via the GitHub Pages functionality doesn't work.

Instead, GitHub Actions are used to make it work:

1. The multiple languages plugin is configured so that each language has its own subfolder (`/de/`, `/en/`).
2. The bug makes it impossible to have the default language content both in the root and in the subfolder.
3. Therefore, the root index.html must forward to the default language subfolder.
4. In order to achieve this, a forwarding index.html in the root folder is written during the GitHub Action.
5. The site is then deployed to (and served from) `github-pages`.

## Create a new page

1. Create template in `_pages`
2. Create content file in `_i18n/<language>/<pagename>/<pagename>.md