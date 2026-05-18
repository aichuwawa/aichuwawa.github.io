# Aichuwawa

This is the GitHub Pages site for `aichuwawa.com`. It uses Jekyll with the
GitHub Pages dependency set and the default Minima theme.

## Run locally

Use Docker Compose from the repo root:

```sh
docker compose up
```

Then open <http://localhost:4000>.

The first run installs the Ruby gems into a named Docker volume. Later runs
should start faster because the gems stay cached in that volume.

## GitHub Pages

In the repo settings, set GitHub Pages to publish from the default branch and
the repo root.

For the custom domain, this repo includes `CNAME` with:

```text
aichuwawa.com
```

The remaining custom-domain setup happens in GitHub and your DNS provider:

- Verify `aichuwawa.com` in GitHub before pointing DNS at GitHub Pages.
- Point the apex domain at GitHub Pages with these A records:
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`
- Or use an `ALIAS` or `ANAME` record to `aichuwawa.github.io` if your DNS host
  supports apex aliases.
- Add a `www` CNAME to `aichuwawa.github.io` if you want
  `www.aichuwawa.com` to redirect to the apex domain.
- After DNS resolves and GitHub provisions the certificate, enable
  "Enforce HTTPS" in the repo's Pages settings.

For a GitHub Pages user site, the repo should be named `aichuwawa.github.io`.
