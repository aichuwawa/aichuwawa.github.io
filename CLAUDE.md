## Project

This is the GitHub Pages user site for `aichuwawa.com`, served at
`https://aichuwawa.com`. It uses Jekyll with the `github-pages` gem and the
remote Minima theme pinned in `_config.yml`.

The initial Jekyll setup is documented in `github-pages-jekyll-setup-plan.md`.
Treat that file as historical setup context, not as a public site page.

Keep the repo small. Change only files needed for the site, GitHub Pages
compatibility, or local development with Docker. Do not run `git commit` or
`git push`; the user handles all commits and pushes.

## Jekyll and SEO

SEO support is enabled through `jekyll-seo-tag` in `_config.yml`. The plugin is
already bundled by the `github-pages` gem, so do not add a separate gem for it.
The `minima` theme includes the SEO tag in its default head markup. If you ever
override `_includes/head.html`, keep `{% seo %}` in the custom head.

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

This site uses `remote_theme: jekyll/minima@v2.5.2` so it can use the latest
released Minima theme while still building on GitHub Pages. The normal place
for style changes is `assets/main.scss` plus Sass partials in `_sass/`.

The local `assets/main.scss` should keep this order:

```scss
@import "variables";
@import "minima";
@import "custom";
```

Put minima variable overrides in `_sass/_variables.scss`. Put regular CSS or
SCSS rules in `_sass/_custom.scss`. Do not edit generated files in `_site`, and
do not edit files inside a downloaded theme cache or installed theme gem.

Font Awesome Free 7.2.0 is included through a pinned public jsDelivr CSS import
in `assets/main.scss`. Keep that import before the Minima import so the browser
can load the icon font stylesheet before site rules. Use Font Awesome classes
in content only when an icon adds useful meaning or familiar visual scanning.

Avoid overriding Minima theme files. Prefer extending and inheriting from the
theme through `_config.yml`, page front matter, local Sass partials, and site
content. Only copy a Minima file into `_layouts/` or `_includes/` when the
change cannot be made by extension. If an override is necessary, copy only that
one file, keep the edit small, and leave a short note explaining why the
override exists.

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
existing Jekyll, Liquid, SCSS, and minima conventions before adding custom
structure.

Do not override Minima `_layouts/` or `_includes/` unless necessary. If an
override is needed, copy only the specific file from Minima and edit the
smallest surface needed. Prefer extension and inheritance over replacing theme
files.

Avoid decorative dependencies, generated artifacts, local editor state,
unrelated rewrites, and removal of user-created changes.
