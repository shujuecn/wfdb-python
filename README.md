# The WFDB Python Package

![signals](https://raw.githubusercontent.com/MIT-LCP/wfdb-python/master/demo-img.png)

[![tests workflow](https://github.com/MIT-LCP/wfdb-python/actions/workflows/run-tests.yml/badge.svg)](https://github.com/MIT-LCP/wfdb-python/actions?query=workflow%3Arun-tests+event%3Apush+branch%3Amaster)
[![PyPI Downloads](https://img.shields.io/pypi/dm/wfdb.svg?label=PyPI%20downloads)](https://pypi.org/project/wfdb/)
[![PhysioNet Project](https://img.shields.io/badge/DOI-10.13026%2Fegpf--2788-blue)](https://doi.org/10.13026/egpf-2788)
[![Supported Python Versions](https://img.shields.io/pypi/pyversions/wfdb.svg)](https://pypi.org/project/wfdb)

## v4 Announcement

[Major breaking changes](https://github.com/MIT-LCP/wfdb-python/issues/369) are planned for WFDB v4, in the core APIs, and the installation method. The planned release date is in August 2022.

- Stable v3 documentation: <https://wfdb.readthedocs.io/en/stable/>
- WIP v4 documentation: <https://wfdb.readthedocs.io/en/latest/>

## Introduction

A Python-native package for reading, writing, processing, and plotting physiologic signal and annotation data. The core I/O functionality is based on the Waveform Database (WFDB) [specifications](https://github.com/wfdb/wfdb-spec/).

This package is heavily inspired by the original [WFDB Software Package](https://www.physionet.org/content/wfdb/), and initially aimed to replicate many of its command-line APIs. However, the projects are independent, and there is no promise of consistency between the two, beyond each package adhering to the core specifications.

## Documentation and Usage

See the [documentation site](http://wfdb.readthedocs.io) for the public APIs.

See the [demo.ipynb](https://github.com/MIT-LCP/wfdb-python/blob/master/demo.ipynb) notebook file for example use cases.

## Installation

The distribution is hosted on PyPI at: <https://pypi.python.org/pypi/wfdb/>. The package can be directly installed from PyPI using either pip or poetry:

```sh
pip install wfdb
poetry add wfdb
```

The development version is hosted at: <https://github.com/MIT-LCP/wfdb-python>. This repository also contains demo scripts and example data. To install the development version, clone or download the repository, navigate to the base directory, and run:

```sh
# Without dev dependencies
pip install .
poetry install

# With dev dependencies
pip install ".[dev]"
poetry install -E dev

# Install the dependencies only
poetry install -E dev --no-root
```

See the [note](#package-management) below about dev dependencies.

## Developing

We welcome community contributions in the form of pull requests. When contributing code, please ensure:

- Documentation is provided. New functions and classes should have numpy/scipy style [docstrings](https://github.com/numpy/numpy/blob/master/doc/HOWTO_DOCUMENT.rst.txt).
- Unit tests are written for new features that are not covered by [existing tests](https://github.com/MIT-LCP/wfdb-python/tree/master/tests).
- The code style is consistent with the project's formating standards.

Run the formatter with:

```sh
black .
```

### Package Management

This project uses [poetry](https://python-poetry.org/docs/) for package management and distribution.

Development dependencies are specified as optional dependencies, and then added to the "dev" extra group in the [pyproject.toml](./pyproject.toml) file.

```sh
# Do NOT use: poetry add <somepackage> --dev
poetry add --optional <somepackage>
```

The `[tool.poetry.dev-dependencies]` attribute is NOT used because of a [limitation](https://github.com/python-poetry/poetry/issues/3514) that prevents these dependencies from being pip installable. Therefore, dev dependencies are not installed when purely running `poetry install`, and the `--no-dev` flag has no meaning in this project.

Make sure the versions in [version.py](./wfdb/version.py) and [pyproject.toml](./pyproject.toml) are kept in sync.

To upload a new distribution to PyPI:

```sh
poetry publish
```

### Creating Documentation

The project's documentation is generated by [Sphinx](https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html) using the content in the [docs](./docs) directory. The generated content is then hosted on readthedocs (RTD) at: <http://wfdb.readthedocs.io>

To manage the content on RTD, request yourself to be added to the [wfdb](https://readthedocs.org/projects/wfdb/) project. The project has already been configured to import content from the GitHub repository. Documentation for new releases should be automatically built and uploaded. See the [import guide](https://docs.readthedocs.io/en/stable/intro/import-guide.html) for more details.

There is some redundancy in specifying the Sphinx requirements between pyproject.toml and [docs/requirements.txt](./docs/requirements.txt), the latter of which is used by RTD. Make sure that the content is consistent across the two files.

To generate the HTML content locally, install the required dependencies and run from the `docs` directory:

```sh
make html
```

### Tests

Run tests using pytest:

```sh
pytest
# Distribute tests across multiple cores.
# https://github.com/pytest-dev/pytest-xdist
pytest -n auto
```

## Citing

When using this resource, please cite the software [publication](https://physionet.org/content/wfdb-python/) oh PhysioNet.
