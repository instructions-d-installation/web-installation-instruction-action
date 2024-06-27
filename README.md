<div align="center">

# `web-installation-instruction-action`

**Action for building webpage from install config file.**

</div>


## Deploy to GH Pages on Change

1. Follow the [guide](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#creating-a-repository-for-your-site) for enabling gh pages for your account.
2. Set und Settings > Pages > GitHub Pages > Build and deployment  Source to `GitHub Actions`.
3. Create a yaml file in `.github/workflows` folder (for example `webpage.yaml`) and put the following content into it:

```yaml
name: Webpage

on:
  push:
    branches:
      - main
    paths:
      - "install.cfg"

jobs:
  webpage:
    runs-on: ubuntu-latest
    name: Compile Webpage
    steps:
      - name: Compile Webpage
        uses: instructions-d-installation/web-installation-instruction-action@0.1.0
      - name: Deploy Webpage
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```
