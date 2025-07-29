# geosdhydro

geosdhydro package.

GIS tools for semi-distributed hydrologic modelling

Classes:

- **`ShapefileToSwiftConverter`** – Converts shapefile data to SWIFT JSON catchment structure.

Functions:

- **`get_parser`** – Return the CLI argument parser.
- **`main`** – Run the main program.

## ShapefileToSwiftConverter

```
ShapefileToSwiftConverter(
    gdf: GeoDataFrame, include_coordinates: bool = False
)

```

Converts shapefile data to SWIFT JSON catchment structure.

Parameters:

- **`gdf`** (`GeoDataFrame`) – GeoDataFrame loaded from shapefile containing link data
- **`include_coordinates`** (`bool`, default: `False` ) – Whether to include lat/lon in node definitions

Methods:

- **`convert`** – Convert shapefile data to SWIFT JSON format.
- **`save_to_file`** – Save converted data to JSON file.

Attributes:

- **`gdf`** (`GeoDataFrame`) – The geodataframe from which we build the json file.
- **`include_coordinates`** (`bool`) – Should the Latitude/Longitude coordinates be derived from the geometry and written in the json file.

Source code in `src/geosdhydro/_internal/swift.py`

```
def __init__(self, gdf: gpd.GeoDataFrame, include_coordinates: bool = False):  # noqa: FBT001, FBT002
    """Initialize converter with geopandas dataframe.

    Args:
        gdf: GeoDataFrame loaded from shapefile containing link data
        include_coordinates: Whether to include lat/lon in node definitions
    """
    self.gdf = gdf
    self.include_coordinates = include_coordinates
    self._check_geodf()

```

### gdf

```
gdf: GeoDataFrame

```

The geodataframe from which we build the json file.

### include_coordinates

```
include_coordinates: bool

```

Should the Latitude/Longitude coordinates be derived from the geometry and written in the json file.

### convert

```
convert() -> Dict[str, Any]

```

Convert shapefile data to SWIFT JSON format.

Returns:

- `Dict[str, Any]` – Dictionary containing Links, Nodes, and SubAreas sections

Source code in `src/geosdhydro/_internal/swift.py`

```
def convert(self) -> Dict[str, Any]:
    """Convert shapefile data to SWIFT JSON format.

    Returns:
        Dictionary containing Links, Nodes, and SubAreas sections
    """
    return {"Links": self._create_links(), "Nodes": self._create_nodes(), "SubAreas": self._create_subareas()}

```

### save_to_file

```
save_to_file(filepath: str, indent: int = 2) -> None

```

Save converted data to JSON file.

Parameters:

- **`filepath`** (`str`) – Path where to save the JSON file
- **`indent`** (`int`, default: `2` ) – Number of spaces for JSON indentation (default: 2)

Source code in `src/geosdhydro/_internal/swift.py`

```
def save_to_file(self, filepath: str, indent: int = 2) -> None:
    """Save converted data to JSON file.

    Args:
        filepath: Path where to save the JSON file
        indent: Number of spaces for JSON indentation (default: 2)
    """
    with open(filepath, "w") as f:
        json.dump(self.convert(), f, indent=indent)

```

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
