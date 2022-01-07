# Welcome to Ajuna Network GitHub Pages

The project has two folders worth mentioning:

- `assets/` - contains css styles and images
- `docs/` - contains individual markdown pages to render

The main entrypoint (or homepage) is `index.md` and new pages must be referenced here.

### To test locally

Making sure [Ruby](https://www.ruby-lang.org/en/documentation/installation/) and [Bundler](https://bundler.io/) are installed in your machine, run the following:

```sh
git clone git@github.com:ajuna-network/ajuna-network.github.io.git
cd ajuna-network.github.io

bundle install
bundle exec jekyll serve
```

The default URL is http://127.0.0.1:4000/.

### Troubleshoot

If there are any issues regarding authentication, follow [this guide](https://jekyll.github.io/github-metadata/authentication/#authentication) to create a personal access token for your GitHub account and use it to set `JEKYLL_GITHUB_TOKEN` environment variable.

```sh
JEKYLL_GITHUB_TOKEN=<YOUR_PAT> bundle exec jekyll serve
```
