<div align="center">

# `web-installation-instruction-action`

**Action for building webpage from install config file.**

</div>


## Usage
```yaml
  path:
    description: Path to config file. Defaults to ./install.cfg
    default: ./install.cfg
  output:
    description: Path to directory, where the html file is written to. Defaults to ./public directory.
    default: ./public
  version:
    description: Version of web-installation-instruction to use. If not specified, uses the latest version.
```


## Deploy to GH Pages on Change

1. Follow the [guide](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#creating-a-repository-for-your-site) for enabling gh pages for your account.
2. Set `Settings > Pages > GitHub Pages > Build and deployment > Source` to `Deploy from a branch`.
3. Create a yaml file in `.github/workflows` folder (for example `webpage.yaml`) and put the following content into it:

```yaml
name: Webpage

on:
  push:
    branches:
      - main
    paths:
      - "install.cfg"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  webpage:
    runs-on: ubuntu-latest
    name: Compile Webpage
    steps:
      - uses: actions/checkout@v4
      - name: Compile Webpage
        uses: instructions-d-installation/web-installation-instruction-action@v0.1.0
      - name: Deploy Webpage
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          folder: ./public
```

4. Push it. And wait for `JamesIves/github-pages-deploy-action` to do it's thing. (See actions.)
5. Go to actions and execute the workflow at least once.
6. Check under `Settings > Pages > GitHub Pages > Build and deployment` if `Branch` is set to `gh-pages`.