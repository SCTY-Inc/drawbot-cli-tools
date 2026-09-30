# drawbot

Skia-native, headless DrawBot CLI. Branded vector artifacts with typographic rules enforced.

## Layout

- `vendor/`: bundled upstream `drawbot-skia` (Apache-2.0). Keep intact, with its LICENSE.
- `drawbot_cli/`: CLI package. `runtime/skia.py` is the import boundary into `vendor/`; `commands/` holds the command groups; `spec/core.py` is the YAML spec renderer; `design.py`, `recipes/`, `create.py` implement the branded flow.
- `fixtures/brand_artifacts/`: social-quote recipe, content, review rubric. `DESIGN.md` is the brand contract.
- `tests/`: pytest.

## Commands

`uv sync --extra dev`, `uv run pytest -q`, `uv run drawbot --help`.

## Rules

- Skia-native and headless only. No backend switching, no native DrawBot compatibility layer.
- Keep the command surface small. Delete before adding.
- Extend `spec/core.py` incrementally.
- Prefer simple integration tests over mocks.
- Use `trash`, not `rm`.
