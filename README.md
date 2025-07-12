# BiagioAntonelli.github.io


Test locally:

**Option 1: Using Docker (Recommended)**
```bash
docker run --rm -v "$PWD:/srv/jekyll" -p 4000:4000 jekyll/jekyll jekyll serve --host 0.0.0.0
```

**Option 2: Using Ruby/Bundler**
Follow installation requirements [here](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)
```bash
bundle exec jekyll serve
```