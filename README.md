# drawbot-cli-tools

Branded vector artifacts from DrawBot, with typographic rules enforced rather than suggested. A headless, Skia-native DrawBot CLI built on bundled upstream `drawbot-skia` source.

## Install

Requires [uv](https://docs.astral.sh/uv/) and Python 3.11+.

```bash
git clone https://github.com/SCTY-Inc/drawbot-cli-tools && cd drawbot-cli-tools
uv sync --extra dev
uv run drawbot doctor     # expect status=ok
uv run pytest -q
```

## Branded artifacts

`DESIGN.md` is the brand contract. The recipe locks geometry and copy; the content file supplies the text.

```bash
uv run drawbot design validate DESIGN.md
uv run drawbot recipe validate fixtures/brand_artifacts/social-quote.recipe.yaml
uv run drawbot create social-quote \
  --design DESIGN.md \
  --recipe fixtures/brand_artifacts/social-quote.recipe.yaml \
  --data fixtures/brand_artifacts/social-quote.content.yaml \
  -n 4 -o out/social-quote --seed 7
```

Writes deterministic variant specs (`social-quote-NN.yaml`), a PDF for each lint-clean variant, and `manifest.json` (inputs, layout, lint results, render status). `design explain` and `recipe explain` show the resolved contract.

## Other commands

```bash
drawbot run script.py -o output.png   # run a drawbot-skia script
drawbot new name                      # script scaffold
drawbot api list | show SYMBOL | gaps # inspect the drawbot-skia API
drawbot spec validate|explain|render poster.yaml -o poster.pdf
```

A spec is a YAML page (`letter`, `a4`, `tabloid`, `square`) with absolutely positioned `rect`, `oval`, `line`, `text`, and `image` elements:

```yaml
page:
  format: letter
  background: "#ffffff"

elements:
  - type: rect
    x: 72
    y: 72
    width: 200
    height: 120
    fill: "#111111"

  - type: text
    text: "Hello DrawBot"
    x: 72
    y: 240
    font: Helvetica
    font_size: 36
```

```

## License

SCTY code: MIT, copyright 2026 SCTY, Inc (see `LICENSE`). `vendor/` bundles [drawbot-skia](https://github.com/justvanrossum/drawbot-skia) by Just van Rossum under the Apache License 2.0 (see `vendor/LICENSE.txt`). This project is not a copy of [DrawBot](https://github.com/typemytype/drawbot) (BSD, Just van Rossum, Erik van Blokland, Frederik Berlaen), which is a separate upstream project.
