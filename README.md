# openastronomy.org

This is the source for the openastronomy.org website.

## Building

To build the site locally, you will need [jekyll](https://jekyllrb.com) to be installed.
Depending on your Ruby setup this may require superuser privileges to install to the default location.
Clone this repository locally, then inside it, type:

```shell
gem install -i vendor/bundle bundler
bundle config --local path 'vendor/bundle'
bundle install
```

to install the dependencies locally at `vendor/bundle`.

You can then build the website with:

```shell
bundle exec jekyll build
```

To view the site locally, you will then need to run:

```shell
bundle exec jekyll serve
```

this will track the changes and rebuild automatically.
However, it won't reflect changes on `_config.yaml`

## Building using a Jekyll container

```bash
# So it's available for other projects
mkdir -p ../vendor/bundle
export JEKYLL_VERSION=3.10.0
# Only needs to run it once to download the dependencies
docker run --rm -e BUNDLE_APP_CONFIG="/srv/vendor/bundle" -e BUNDLE_HOME="/srv/vendor/bundle" -e BUNDLE_PATH="/srv/vendor/bundle" --volume="$PWD:/srv/jekyll" --volume="$PWD/../vendor:/srv/vendor" -it jekyll/jekyll:$JEKYLL_VERSION  bundle install
# Build
docker run --rm -e BUNDLE_APP_CONFIG="/srv/vendor/bundle" -e BUNDLE_HOME="/srv/vendor/bundle" -e BUNDLE_PATH="/srv/vendor/bundle" --volume="$PWD:/srv/jekyll" --volume="$PWD/../vendor:/srv/vendor" -it jekyll/jekyll:$JEKYLL_VERSION  bundle exec jekyll build
# Serve from python
python -m http.server -d _site
```

## Submodule

Note that this uses a submodule to complete the build process of the site.
So you may need to do:

```shell
git submodule update --recursive --init
```

in a fresh clone, or even to just update the submodule.
