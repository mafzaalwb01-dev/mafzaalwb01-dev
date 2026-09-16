name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Generate snake SVGs
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: mafzaalwb01-dev
          outputs: |
            dist/snake.svg?palette=github-light
            dist/snake-dark.svg?palette=github-dark&color_snake=#D4AF37&color_dots=#161b22,#8B6914,#B8860B,#D4AF37,#FFD700

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
