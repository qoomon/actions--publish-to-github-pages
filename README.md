# Deploy To GitHub Pages Action


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
