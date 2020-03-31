# Container Action Template

To get started, click the `Use this template` button on this repository [which will create a new repository based on this template](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/).

For info on how to build your first Container action, see the [toolkit docs folder](https://github.com/actions/toolkit/blob/master/docs/container-action.md).


### Usage
```yaml
name: Build & Deploy

on:
  push:
    branches: [ master ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-node@v1
      with:
        node-version: 13.x
    - run: npm ci
    - run: npm run build
    - run: npm test
      env:
        CI: true
        
    - name: Deploy to GitHub Pages
      if: github.ref == 'refs/heads/master'
      uses: qoomon/deploy-to-github-pages-action@v1
      with:
        GITHUB_PAGES_SOURCE_DIR: dist # default value:  dist
        GITHUB_PAGES_BRANCH: gh-pages # default value:  gh-pages
        GITHUB_PAGES_REPLACE: false   # default value:  false
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```