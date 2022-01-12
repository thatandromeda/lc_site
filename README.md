# lc_site

## Development

This is a jekyll app. You can run it locally with `jekyll serve`.

It needs a source of `feather_files` (in the `_config.yml`) representing its
data source. Currently it's pointed straight at the files for the development
site.

## Deployment
- code deploys automatically to the Digital Ocean staging site on push/merge to GitHub `main` branch
- the Digital Ocean production site is connected to Github `main` but must be manually deployed
- data must be manually deployed:
  - upload to the Digital Ocean space matching `_config.yml`, in the `tiles` directory
  - set to public
  - add a file to the `tiles` directory which indicates which data set is currently there
