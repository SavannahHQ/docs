# Local build

The docs are built using [Jekyll](https://jekyllrb.com/) and are hosted by [Github Pages](https://pages.github.com/). 

To build them locally, you need to follow the [Github Pages documentation](https://docs.github.com/en/enterprise/2.14/user/articles/setting-up-your-github-pages-site-locally-with-jekyll) and create the appropriate `Gemfile`. 

Afterwards, just run `bundle exec jekyll serve` if you want to serve them locally and preview any changes you may make, or build them using `bundle exec jekyll build`.

Github pages automatically build the website, thus PR should concern only the source files (e.g `index.md`) and not the output of `jekyll build` (e.g `index.html`).

