# geosdhydro

geosdhydro package.

GIS tools for semi-distributed hydrologic modelling

Modules:

- **`swift`** – Convert shapefile data to SWIFT JSON catchment structure.

Functions:

- **`get_parser`** – Return the CLI argument parser.
- **`main`** – Run the main program.

## get_parser

```
get_parser() -> ArgumentParser

```

Return the CLI argument parser.

Returns:

- `ArgumentParser` – An argparse parser.

Source code in `src/geosdhydro/_internal/cli.py`

```
def get_parser() -> argparse.ArgumentParser:
    """Return the CLI argument parser.

    Returns:
        An argparse parser.
    """
    parser = argparse.ArgumentParser(prog="geosdhydro")
    parser.add_argument("-V", "--version", action="version", version=f"%(prog)s {debug._get_version()}")
    parser.add_argument("--debug-info", action=_DebugInfo, help="Print debug information.")
    return parser

```

## main

```
main(args: list[str] | None = None) -> int

```

Run the main program.

This function is executed when you type `geosdhydro` or `python -m geosdhydro`.

Parameters:

- **`args`** (`list[str] | None`, default: `None` ) – Arguments passed from the command line.

Returns:

- `int` – An exit code.

Source code in `src/geosdhydro/_internal/cli.py`

```
def main(args: list[str] | None = None) -> int:
    """Run the main program.

    This function is executed when you type `geosdhydro` or `python -m geosdhydro`.

    Parameters:
        args: Arguments passed from the command line.

    Returns:
        An exit code.
    """
    parser = get_parser()
    opts = parser.parse_args(args=args)
    print(opts)
    return 0

```
