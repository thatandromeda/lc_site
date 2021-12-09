# lc_site

## Deployment
- code deploys automatically to Digital Ocean on push/merge to GitHub main branch
- data must be manually deployed:
  - upload to the Digital Ocean space matching `_config.yml`, in the `tiles` directory
  - set to public
  - add a file to the `tiles` directory which indicates which data set is currently there
