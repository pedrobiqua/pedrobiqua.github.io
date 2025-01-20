---
layout: post
category: Blog
author: pedro
tags: [cpp, python, cython, dev, "search engine", pypi]
title: "How to publish a package on PyPI with C++, Cython, and Python"
math: false
mermaid: false
date: Sat Jan 18 2025 21:00:00 GMT-0300 (Horário Padrão de Brasília)
description: In this post, you will see the experience of publishing a package on PyPI with C++ code and how to compile it during the package installation.
---

## Why Publish My Package on PyPI?

When I first thought about creating a library in C++, publishing it on PyPI never crossed my mind. However, while watching a video by [Waine - Dev do Desempenho](https://www.youtube.com/watch?v=fcUhOtZZPMI&t=1071s&pp=ygUeemlnIHBhcmEgcHl0aG9uIGRldiBkZXNlbXBlbmhv), I discovered it was possible to integrate C/C++ code with Python. So, I thought, why not take advantage of that?

That’s when I decided to port my _Search Engine_ library to Python. To achieve this, I used **Cython**, which allows me to call functions written in C++ and directly consume them in Python.

Since PyPI is one of the most popular package distribution platforms, it seemed like the natural choice to make my library available to others.

---

## How to Integrate C++ with My Package?

This was a somewhat challenging task. I had to dive into the Cython documentation, as there are many parameters and possibilities to consider. The first step was compiling the C++ library. Once compiled, I obtained the `libsearch_engine.so` file, which is essential for synchronizing the library with Cython.

After the compilation step, I had to create a `setup.py` file to define how the C++ library would be built and linked. To streamline the process, after a lot of research, I decided to use **Poetry**. Poetry offers several tools that make development, organization, and package publishing on PyPI much easier.

In addition to Poetry, I created a `build.py` file to replace `setup.py`. This file is responsible for compiling the C++ code and linking it with Cython to generate the `.so` files used in the Python library.

Below is an example of how I structured the build process:

```python
import os

# See if Cython is installed
try:
    from Cython.Build import cythonize
# Do nothing if Cython is not available
except ImportError:
    # Got to provide this function. Otherwise, poetry will fail
    def build(setup_kwargs):
        pass
# Cython is installed. Compile
else:
    from setuptools import Extension, setup
    from setuptools.dist import Distribution
    from distutils.command.build_ext import build_ext
    import subprocess
    import glob
    import shutil
    import pathlib


BUILD_FOLDER = "build"

def build_lib_cpp(path: str):
    if not os.path.exists(path):
        old_path = os.getcwd()
        os.makedirs(path)
        os.chdir(path)
        subprocess.run(["cmake", "..", "-DBUILD_TESTS=OFF"])
        subprocess.run(["make"])
        os.chdir(old_path)

def copy_lib(root_path, path_lib):
    extensions = [".so*", ".dll*", ".dylib*"]
    for ext in extensions:
        path_so = root_path.glob(f"{BUILD_FOLDER}/lib/*{ext}")
        path_lib.mkdir(exist_ok=True, parents=True)
        # Copy each .so file
        for lib in path_so:
            shutil.copy(lib, path_lib)
            print(f"\n\n\n{path_lib}\n\n\n")

# setup_kwargs
def build(setup_kwargs):
    # Build the C++ library to be used in Python
    build_lib_cpp(BUILD_FOLDER)
    root_path = pathlib.Path(__file__).parent
    path_lib = pathlib.Path(__file__).parent / "search_engine_cpp/lib"
    copy_lib(root_path, path_lib)
    library_dir = os.path.abspath("search_engine_cpp/lib")


    # Modules to be used in Python
    libs_names = [
        "_hello",
        "_page_rank",
        "_inverted_index"
    ]

    extensions = []

    for lib in libs_names:
        ext = Extension(
            f"search_engine_cpp.{lib}",
            language="c++",
            sources=[
                f"lib/src/{lib}.pyx"
            ],
            include_dirs=["lib/include"],
            library_dirs=[library_dir],
            runtime_library_dirs=[library_dir],
            libraries=["search_engine"],
            # extra_compile_args=["-std=c++11"]
        )
        extensions.append(ext)

    # Build the setup using extensions
    # setup_kwargs["cmdclass"] = {"build_ext": build_ext}
    setup_kwargs["script_args"] = ["build_ext"]
    # Include .so files in the installation
    setup_kwargs["package_data"] = {
        "search_engine_cpp": ["lib/*.so"]
    }
    setup_kwargs["include_package_data"] = True

    setup_kwargs["ext_modules"] = cythonize(extensions, compiler_directives={"language_level": "3str"}, force=True)
```

Once I successfully built everything, I had to make sure it would work on the end user's machine during installation. This required changes to the `pyproject.toml` file, which is one of Poetry’s conveniences. I specified the folders that must be included for the C++ code to be compiled on the user’s machine. Here's an example of my `pyproject.toml`:

```toml
[tool.poetry]
name = "search-engine-cpp"
version = "0.1.3"
description = "Search Engine is a project that implements a basic search engine using C++, Python, and Cython. It builds a reverse index and ranks pages with the PageRank algorithm based on keyword relevance and page importance."
authors = ["Pedro Bianchini de Quadros <pedrobiqua@gmail.com>"]
readme = "README.md"
include = [
    "lib/**",  # Include the lib directory with all files
    "search_engine_cpp/lib/*.so",
    "search_engine_cpp/.*so",
    "CMakeLists.txt",
    "README.md",  # Include the README
    "LICENSE.md"  # Include the license file
]
homepage = "https://pedrobiqua.github.io/Search_Engine/html/"

[tool.poetry.dependencies]
python = "^3.10"
cython = "^3.0.11"
requests = "^2.32.3"
beautifulsoup4 = "^4.12.3"


[tool.poetry.group.dev.dependencies]
commitizen = "^4.1.0"
setuptools = "^75.7.0"

[build-system]
requires = ["poetry-core", "setuptools", "wheel", "cython"]
build-backend = "poetry.core.masonry.api"

[tool.poetry.build]
script = "build.py"
generate-setup-file = true
```

---

## How Was the Process?

This entire process was time-consuming and required hours of studying. I had to carefully read the Cython documentation to figure out how to properly integrate everything. I also watched countless videos and joined Discord communities to find an acceptable solution. However, it’s still not perfect—one issue I suspect is the organization and location of the C++ files, which will take more time to fix.

---

## How I Create Releases for My Package

To create releases and publish the package, I needed to create an account on PyPI and generate a token for publishing. To simplify this process, I’m using **GitHub Actions**, which automatically publishes a new release whenever I create a new tag. The core publishing process involves the following commands:

```bash
poetry build
poetry publish --username __token__ --password $POETRY_PASSWORD
```

Using these commands, my GitHub Actions workflow looks like this:

```yaml
name: Release Python Package

on:
  workflow_dispatch:
  push:
    tags:
      - '*'
    branches:
      - main

permissions: write-all

jobs:
  build-and-publish:
    if: contains(github.ref, 'refs/tags/')
    runs-on: ubuntu-latest

    steps:
      # 1. Checkout code
      - name: Checkout Code
        uses: actions/checkout@v4

      # 2. Set up Python
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.11

      # 3. Create and activate virtual environment
      - name: Create Virtual Environment
        run: |
          python -m venv .venv
          source .venv/bin/activate

      # 4. Install Poetry
      - name: Install Poetry
        run: pip install poetry

      # 5. Install dependencies
      - name: Install Dependencies
        run: poetry install --without dev

      # 6. Build the package with Poetry
      - name: Build Package
        run: poetry build

      # 7. Publish to PyPI
      - name: Publish to PyPI
        env:
          POETRY_PASSWORD: ${{ secrets.PYPI_API_TOKEN }}
        run: poetry publish --username __token__ --password $POETRY_PASSWORD

      - name: GH Release
        uses: softprops/action-gh-release@v2.2.0
        with:
          draft: false
          prerelease: true
          token: ${{ secrets.GITHUB_TOKEN }}
          generate_release_notes: true
```

---

## Conclusion
This experience of creating and publishing a Python package with a C++ core was challenging but also very rewarding. I not only learned about tools like Cython and Poetry but also about how to structure and distribute a project so that others can use it. There are still improvements to be made, but the learning process along the way made every challenge worthwhile.


Keep learning,
**_Pedro_ ;)**
