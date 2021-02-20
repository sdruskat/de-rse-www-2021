## Setup

This site uses the [Minimal Mistakes Jekyll template](https://github.com/mmistakes/minimal-mistakes) together with the [Multiple Languages Plugin](https://github.com/kurtsson/jekyll-multiple-languages-plugin).
Due to a [bug](https://github.com/kurtsson/jekyll-multiple-languages-plugin/issues/186) in the latter, and due to how the template works, auto-deploying via the GitHub Pages functionality doesn't work.

Instead, GitHub Actions are used to make it work:

1. The multiple languages plugin is configured so that each language has its own subfolder (`/de/`, `/en/`).
2. The bug makes it impossible to have the default language content both in the root and in the subfolder.
3. Therefore, the root index.html must forward to the default language subfolder.
4. In order to achieve this, a forwarding index.html in the root folder is written during the GitHub Action.
5. The site is then deployed to (and served from) `github-pages`.

## Create a new page

1. Create template in `_pages`
2. Create content file in `_i18n/<language>/<sectionname>/<pagename>.md
3. in the template Markdown file in `_pages`, add `{% tf <sectionname>/<pagename>.md %}`, which will embed the translated file contents.

## Create a new post

1. Create a new post in the `_posts` directory
2. Provide the key `language` in the YAML metadata (e.g., `language: en`)
3. Only English (`en`) and German (`de`) posts are possible at the moment
4. Posts will be displayed on language-specific blog pages, sorted by publication date

## Creating a splash page

Splash pages with feature rows can be used, and content at different places be translated.

- *Excerpt translations* (which replace values for the `excerpt` keys) with a length of > 1 line are translated via a translated file in the `_i18n/<language>/` directory, and a value for the YAML key `excerpt-translation` in the feature row or front matter YAML.
- *Short translations* (1 line, replacing `title` or `btn_label` keys with `title-translation`, `btn_label-translation`) are translated via translation keys in `_i18n/<language>.yml`.

### Example excerpt

```yaml
intro: 
    - excerpt-translation: home/intro-excerpt.md # Long excerpt translations have their own files
feature_row:
  - image_path: /assets/images/image.png
    alt: "Positions"
    title-translation: home.positions-title # Translation key for the positions title
    excerpt-translation: home/positions-excerpt.md
    url: "/home/positions/"
    btn_class: "btn--primary"
    btn_label-translation: home.learn-more-button
```