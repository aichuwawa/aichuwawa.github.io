## Project

This is the GitHub Pages user site for `aichuwawa.com`, served at
`https://aichuwawa.com`. It uses Jekyll with the `github-pages` gem and local
theme files in this repo. It does not use Minima, `theme`, or `remote_theme`.

The initial Jekyll setup is documented in `github-pages-jekyll-setup-plan.md`.
Treat that file as historical setup context, not as a public site page.

Keep the repo small. Change only files needed for the site, GitHub Pages
compatibility, or local development with Docker. Do not run `git commit` or
`git push`; the user handles all commits and pushes.

## Jekyll and SEO

SEO support is enabled through `jekyll-seo-tag` in `_config.yml`. The plugin is
already bundled by the `github-pages` gem, so do not add a separate gem for it.
The local `_includes/head.html` must keep `{% seo %}` so pages get title tags,
canonical URLs, Open Graph tags, Twitter card tags, and JSON-LD.

Sitemap support is enabled through `jekyll-sitemap` in `_config.yml`. It
generates `/sitemap.xml` during the Jekyll build. The root `robots.txt` points
crawlers at `https://aichuwawa.com/sitemap.xml`.

Keep `url: "https://aichuwawa.com"` and `baseurl: ""` in `_config.yml` unless
the published domain changes. These values affect canonical URLs, Open Graph
URLs, JSON-LD, feed links, and the sitemap.

GitHub Pages enables plugins such as `jekyll-optional-front-matter` and
`jekyll-readme-index` by default. That means Markdown files without front matter
can become published pages, and regular repo files can be copied into `_site`.
Keep repo-only files such as `AGENTS.md`, `CLAUDE.md`, `README.md`, local editor
files, Docker files, and setup notes in the `_config.yml` `exclude` list unless
they are meant to be public site content.

For individual pages and posts, prefer front matter metadata over custom HTML:
`title`, `description`, and `image` feed the SEO plugin. Use `sitemap: false`
only when a public page should be omitted from the generated sitemap.

## Styling

This site uses local Sass files for its custom theme. The entrypoint is
`assets/main.scss`; shared partials live in `_sass/`.

The local `assets/main.scss` should keep this order:

```scss
@import "https://use.fontawesome.com/releases/v7.2.0/css/all.css";
@import "https://cdn.jsdelivr.net/npm/bulma@1.0.4/css/bulma.min.css";
@import "fonts";
@import "variables";
@import "base";
@import "layout";
@import "custom";
```

Put `@font-face` rules in `_sass/_fonts.scss`, shared design settings in
`_sass/_variables.scss`, element defaults in `_sass/_base.scss`, structural
page styles in `_sass/_layout.scss`, and one-off site rules in
`_sass/_custom.scss`. Do not edit generated files in `_site`.

Custom font files live in `assets/fonts/`. Since `assets/main.scss` builds to
`/assets/main.css`, font URLs in Sass should be relative to that CSS file, such
as `url("fonts/GOODDC.woff")`.

Font Awesome Free 7.2.0 is included through a pinned public
`use.fontawesome.com` CSS import in `assets/main.scss`. Use Font Awesome
classes in content only when an icon adds useful meaning or familiar visual
scanning.

Bulma 1.0.4 is included through a pinned public jsDelivr CSS import in
`assets/main.scss`. Keep framework imports before local Sass partials so site
styles can override framework defaults.

Montserrat is loaded from Google Fonts in `_includes/head.html` using
`preconnect` links plus the Google Fonts stylesheet link. Keep those tags in the
head include, not in Sass, so the browser can start the font connection early.
The base Sass font stack is `$font-family-base` in `_sass/_variables.scss`.

## JavaScript

Custom JavaScript uses plain browser ES modules with no bundler. The global
entrypoint is `assets/js/main.js`, and shared modules live under
`assets/js/modules/`.

`_layouts/default.html` includes `_includes/scripts.html` before `</body>`, so
`assets/js/main.js` runs on every page. Keep the script tag as
`type="module"` and use `relative_url` for local asset paths.

For page-specific modules, add a `scripts` list in page front matter:

```yaml
scripts:
  - /assets/js/example-page.js
```

Use this only when a page needs its own behavior. Prefer small, focused modules
over adding a JavaScript build step.

## Theme Structure

This repo owns its theme skeleton:

- `_layouts/default.html` wraps every page.
- `_layouts/home.html` renders the home page and post list.
- `_layouts/page.html` renders regular pages.
- `_layouts/post.html` renders posts.
- `_includes/head.html` owns metadata, SEO, feed metadata, and the stylesheet.
- `_includes/header.html` owns the site title and navigation.
- `_includes/footer.html` owns the footer.
- `_includes/scripts.html` owns global and page-specific ES module scripts.
- `_data/navigation.yml` controls top-level navigation.
- `assets/fonts/` stores local font files referenced by `_sass/_fonts.scss`.

Prefer changing these local theme files directly instead of adding an external
theme. Keep the skeleton small and avoid adding front-end build tools unless
the site has a clear need for them.

## Prose

When editing prose, first scan the surrounding text. If the document already
has a substantial amount of prose, infer its overall style and match it. If
there is not enough existing prose to guide the edit, use a casual, everyday
conversational style aimed at a layman reader. Prefer everyday words, short
sentences, contractions when they sound natural, and direct explanations that
feel like one person talking to another. Avoid academic, corporate, or overly
polished phrasing unless the topic needs that tone. Assume the reader is smart
but may not know the context, and explain unfamiliar terms the first time they
matter. Generated prose must be ASCII-only UTF-8: straight quotes, no curly
quotes, no em dashes, no en dashes, no ellipsis characters, and no emojis. Use
hyphens only for real hyphenation, not as dash substitutes.

Prefer concrete verbs and nouns over vague praise or vague effort. Avoid filler
phrases that sound polished but do not add meaning. If a phrase can be deleted
without changing the meaning, delete it.

Prose blacklist:

- Avoid generic praise words such as "clean", "nice", "neat", "elegant",
  "powerful", or "robust" when they do not name what is true.
- Avoid vague effort phrases such as "does the heavy lifting", "carries the
  weight", "gets out of the way", "just works", "earns its keep", or "punches
  above its weight".
- Avoid essay-register phrases such as "the real payoff", "the headline
  benefit", "comes into its own", "shines when", or "connective tissue".
- Avoid hollow intensifiers and hedges such as "really", "very", "basically",
  "actually", "simply", "perhaps", "maybe", "sort of", or "kind of" unless
  they add real contrast or meaning.
- Avoid using "thing" or "things" as placeholder nouns. Name the actual idea,
  choice, rule, detail, or result.

## Editing

Prefer minimal, targeted changes that preserve GitHub Pages compatibility. Use
existing Jekyll, Liquid, and SCSS conventions before adding custom structure.

Avoid decorative dependencies, generated artifacts, local editor state,
unrelated rewrites, and removal of user-created changes.
