# easyeda2kicad v0.2.0

_________________
[![PyPI version](https://badge.fury.io/py/easyeda2kicad.svg)](https://badge.fury.io/py/easyeda2kicad)
[![License](https://img.shields.io/github/license/upesy/easyeda2kicad.py.svg)](https://pypi.org/project/isort/)
[![Downloads](https://pepy.tech/badge/easyeda2kicad)](https://pepy.tech/project/easyeda2kicad)
![Python versions](https://img.shields.io/pypi/pyversions/easyeda2kicad.svg)
[![Git hook: pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)
_________________


A Python script that convert any electronic components from [EasyEDA](https://easyeda.com/) or [LCSC](https://www.lcsc.com/) to a Kicad library including **3D model in color**.

<p align="center">
  <img src="https://raw.githubusercontent.com/uPesy/easyeda2kicad.py/master/ressources/demo_symbol.png" width="500">
</p>
<div align="center">
  <img src="https://raw.githubusercontent.com/uPesy/easyeda2kicad.py/master/ressources/demo_footprint.png" width="500">
</div>


## Installation

```bash
pip install easyeda2kicad
```

## Usage

```bash
# For symbol + footprint + 3d model (with --full argument)
easyeda2kicad --full --lcsc_id=C2040
# For symbol + footprint + 3d model
easyeda2kicad --symbol --footprint --3d --lcsc_id=C2040
# For symbol + footprint
easyeda2kicad --symbol --footprint --lcsc_id=C2040
# For symbol only
easyeda2kicad --symbol --lcsc_id=C2040
# For footprint only
easyeda2kicad --footprint --lcsc_id=C2040
# For 3d model only
easyeda2kicad --3d --lcsc_id=C2040
```

By default, all librairies are saved in `C:/Users/your_name/Documents/Kicad/easyeda2kicad/`, with :
- `easyeda2kicad.lib` for symbol library
- `easyeda2kicad.pretty/` for footprint libraries
- `easyeda2kicad.3dshapes/` for 3d models

If you want to save components symbol/footprint in your own libs, you can specify the output lib path by using `--output` option.

```bash
easyeda2kicad --full --lcsc_id=C2040 --output ~/libs/my_lib
```

This command will save:
- the symbol in `~/libs/my_lib.lib` file for symbol library. The file will be created if it doesn't exist.
- the footprint in `~/libs/my_lib.pretty/` folder for footprint libraries. The folder will be created if it doesn't exist.
- the 3d models in `~/libs/my_lib.3dshapes/` folder for 3d models. The folder will be created if it doesn't exist.

You can use the option `--overwrite` to update a component symbol/footprint that is already in a Kicad library (generated by easyeda2kicad)

```bash
easyeda2kicad --symbol --footprint --lcsc_id=C2040 --output ~/libs/my_lib --overwrite
```

## Add libraries in Kicad

**These are the instructions to add the default easyeda2kicad libraries in Kicad.**
Before configuring KiCad, run at least once time the script to create lib files. For example :

```bash
easyeda2kicad --symbol --footprint --lcsc_id=C2040
```

- In KiCad, Go to Preferences > Configure Paths, and add the environment variables `EASYEDA2KICAD` :
  - Windows : `C:/Users/your_username/Documents/Kicad/easyeda2kicad/`,
  - Linux : `/home/your_username/Documents/Kicad/easyeda2kicad/`
- Go to Preferences > Manage Symbol Libraries, and Add the global library `easyeda2kicad` : `${EASYEDA2KICAD}/easyeda2kicad.lib`
- Go to Preferences > Manage Footprint Libraries, and Add the global library `easyeda2kicad` : `${EASYEDA2KICAD}/easyeda2kicad.pretty`
- Enjoy :wink:


## Inspirations

- [KiPart](https://github.com/devbisme/KiPart) - A utility that generates single
and multi-unit symbols from a CSV file containing all the pin information for
one or more parts.
