name: Generate Snake Animation

on:
  schedule:
    - cron: "0 0 * * *" # Roda diariamente à meia-noite (UTC)
  workflow_dispatch:

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: Platane/snk@v3
        with:
          github_user_name: WilMarques05
          outputs: |
            dist/snake.svg
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output # O nome da branch que armazena o SVG
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
