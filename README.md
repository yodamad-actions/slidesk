# slidesk

A GitHub actions to deploy your [Slidesk]() presentation on GitHub pages.

The action will :

* Build your presentation with `slidesk`
* Publish it on GitHub pages

## Prerequisites

* GitHub Pages must be enabled on your project and setup on `GitHub Actions`
* Don't forget to add the permissions in your workflow file, as showed in [example](#very-important)

```yml
permissions:
  contents: read
  pages: write       # required by deploy-pages
  id-token: write    # required by deploy-pages
```

## Inputs

| Input | Description | Default value |
|-------|-------------|---------------|
| output-dir | Directory containing the static site output | public |
| image-version | SLidesk image version to use | latest |
| workdir | Directory containing `main.sdf` slidesk file | . |

## Sample

```yml
name: Deploy with Toto
on:
  push:
    branches: [ "main" ]
  workflow_dispatch:

## Very important

permissions:
  contents: read
  pages: write       # required by deploy-pages
  id-token: write    # required by deploy-pages

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Build & Deploy
        id: toto
        uses: yodamad-actions/slidesk@0.0.2
        with:
          output-dir: public
          image-version: latest
          workdir: slidesk

      - name: Show site URL
        run: echo "Deployed at ${{ steps.toto.outputs.page_url }}"
```