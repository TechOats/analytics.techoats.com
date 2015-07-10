## analytics.techoats.com

A project to borrow analytics.usa.gov code base for TechOats

### Setup

Ths app uses [Jekyll](http://jekyllrb.com) to build the site, and [Sass](http://sass-lang.com/), [Bourbon](http://bourbon.io), and [Neat](http://neat.bourbon.io) for CSS.

Install them all:

```bash
bundle install
```

### Developing locally

Run Jekyll with development settings:

```bash
make dev
```

(This runs `bundle exec jekyll serve --watch --config _.yml,_development.yml`.)

Sass can watch the .scss source files for changes, and build the .css files automatically:

```bash
make watch
```

To compile the Sass stylesheets once, run `make clean all`, or `make -B` to compile even if the .css file already exists.

### Developing with local data

The development settings assume data is available at `http://localhost:3000`.

If also working off of local data, e.g. using `analytics-reporter`, you will need to make the data available over HTTP _and_ through CORS.

Various tools can do this. This project recommends using the Node module `serve`:

```bash
npm install -g serve
```

Generate data to a directory:

```
analytics --output [dir]
```

Then run `serve` from the output directory:

```bash
serve --cors
```

The data will be available at `http://localhost:3000` over CORS, with no path prefix. For example, device data will be at `http://localhost:3000/devices.json`.


### Deploying the app to production

In production, the site's base URL is set to `https://analytics.techoats` and the data's base URL is set to `https://analytics.techoats.com/data`.

```bash
make production && s3cmd put --recursive -P -f --rr --add-header="Cache-Control:max-age=300" _site/* s3://S3_BUCKET_HERE/
```

**Use the full command above.** The full command ensures that the build completes successfully, with production settings, _before_ triggering an upload to the production bucket.

### Fixing links in the Top 20

Links pulled directly from Google Analytics are occasionally broken (this is most common in the Top 20 section). For now, we're hard coding the fix in the `index.js` file [here](https://github.com/GSA/analytics.usa.gov/blob/master/js/index.js#L6) in the format: `"broken link" : "working link",`.

### Public domain

Code forked from https://github.com/GSA/analytics.usa.gov

This project is in the worldwide [public domain](LICENSE.md). As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.
