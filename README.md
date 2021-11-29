# lc_site

## Deployment
- code deploys automatically to Digital Ocean on push/merge to GitHub main branch
- data must be manually deployed:
  - upload to a Digital Ocean space
  - set to public
  - update `_config.yml` `feather_files` setting to point to the relevant directory
