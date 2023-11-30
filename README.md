# coach-scraper

**Caution! Be careful running this script.**

We intentionally delay each batch of requests. Make sure any adjustments to this
script appropriately rate-limit.

## Overview

This is a simple web scraper for coaches listed on:

* [chess.com](https://www.chess.com/coaches)
* [lichess.org](https://www.lichess.org/coach)

The program searches for coach usernames as well as specific information about
each of them (their profile, recent activity, and stats). The result will be
found in a newly created `data` directory with the following structure:
```
data
└── <site>
│   ├── coaches
│   │   ├── <username>
│   │   │   ├── <username>.html
│   │   │   ├── export.json
│   │   │   └── ...
│   │   ├── ...
└── pages
    ├── <n>.txt
    ├── ...
```

## Usage

If you have nix available, run:
```bash
$> nix run . -- --user-agent <your-email> -s chesscom
```
If not, ensure you have [poetry](https://python-poetry.org/) on your machine and
instead run the following:
```bash
$> poetry run python3 -m app -u <your-email> -s chesscom
```

## Development

[nix](https://nixos.org/) is used for development. The included `flakes.nix`
file automatically loads in Python (version 3.11.6) with packaging and
dependency management handled by poetry (version 1.7.0). [direnv](https://direnv.net/)
can be used to a launch a dev shell upon entering this directory (refer to
`.envrc`). Otherwise run via:
```bash
$> nix develop
```

### Language Server

The [python-lsp-server](https://github.com/python-lsp/python-lsp-server)
(version v1.9.0) is included in this flake, along with the [python-lsp-black](https://github.com/python-lsp/python-lsp-black)
plugin for formatting purposes. `pylsp` is expected to be configured to use
[McCabe](https://github.com/PyCQA/mccabe), [pycodestyle](https://pycodestyle.pycqa.org/en/latest/),
and [pyflakes](https://github.com/PyCQA/pyflakes). Refer to your editor for
configuration details.

### Formatting

Formatting depends on the [black](https://black.readthedocs.io/en/stable/index.html)
(version 23.9.1) tool. A `pre-commit` hook is included in `.githooks` that can
be used to format all `*.py` files prior to commit. Install via:
```bash
$> git config --local core.hooksPath .githooks/
```
If running [direnv](https://direnv.net/), this hook is installed automatically
when entering the directory.
