(local:build)=

# Local Build

In addition to directly editing it on GitHub, you can also download the repository to your local machine, edit the files, and then upload. You may want to visually check that everything works fine before uploading. To do this, you can build the doc locally.

## Installation

First, create a [conda environment](conda:environment):

```
$ conda create --name wen_group_manual
$ conda activate wen_group_manual
```

Clone the repo from GitHub to your local machine:

```
$ git clone https://github.com/wengroup/group_manual.git
```

Then install dependencies and this repo:

```
$ pip install -e group_manual
```

## Building

We use [jupyter-book](https://jupyterbook.org/en/stable/intro.html) to convert the markdown source files into html webpages. To build it, in the directory where the `pyproject.toml` file resides, do

```
$ jupyter-book build docs --path-output docs_build
```

The generated group manual is placed in `docs_build`, and you can look at it by opening this file in a browser: `docs_build/_build/html/index.html`.
