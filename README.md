# latex-action

[![Test](https://github.com/zydou/latex-action/actions/workflows/test.yml/badge.svg)](https://github.com/zydou/latex-action/actions/workflows/test.yml)

This is a GitHub Action to compile LaTeX documents, and it's based on [xu-cheng/latex-action](https://github.com/xu-cheng/latex-action).

## What's the difference from the original action?

|                         | **Original** | **This Action** |
| ----------------------- | ------------ | --------------- |
| base image              | Alpine       | Debian & Ubuntu |
| install system packages | apk add      | apt-get install |
| change texlive version  | ✅            | ✅               |
| change base image       | /            | ✅               |

The main difference is that this action uses `Debian` or `Ubuntu` as the base image, whereas the original uses `Alpine`. Certain tools require `glibc` to function properly. Within debian or ubuntu, you won't encounter any glibc-related issues and can use `apt-get` to install a wider range of packages compared to using `apk` in Alpine. For instance, the Alpine-based image lacks the [xindy package](https://github.com/xu-cheng/latex-action/issues/32).

In addition, this action also allows you to specify the TeX Live version and the base image version through input parameters. ~~In contrast, the original action requires the use of different tags to specify the TeX Live version.~~ The advantage of this is that you can easily use `matrix` syntax to build your document with multiple TeX Live versions. For example:

```yaml
jobs:
  build_latex:
    strategy:
      fail-fast: false
      matrix:
        texlive_version: [2023, 2022, 2021, 2020, 2019, 2018] # `latest` is also valid
        base_image: [buster, bullseye, bookworm, trixie, xenial, bionic, focal, jammy]
    name: texlive-${{ matrix.texlive_version }}-${{ matrix.base_image }}
```

## Inputs

Each input is provided as a key inside the `with` section of the action.

- `root_file` (**required**, defaults to: "")

  The root LaTeX file to be compiled. You can also pass multiple files as a multi-line string to compile multiple documents. Each file path will be interpreted as bash glob pattern. For example:

  ```yaml
    - uses: zydou/latex-action@v3
      with:
        root_file: |
          file1.tex
          file2.tex
  ```

- `working_directory` (optional, defaults to: ".")

  The working directory for this action.

- `work_in_root_file_dir` (optional, defaults to: "false")

  Change directory into each root file's directory before compiling each documents. This will be helpful if you want to build multiple documents and have the compiler work in each of the corresponding directories.

- `continue_on_error` (optional, defaults to: "false")

  Continuing to build document even with LaTeX build errors. This will be helpful if you want to build multiple documents regardless of any build error.

- `compiler` (optional, defaults to: "latexmk")

  The LaTeX engine to be invoked. By default, [`latexmk`](https://ctan.org/pkg/latexmk) is used, which automates the process of generating LaTeX documents by issuing the appropriate sequence of commands to be run.

- `args` (optional, defaults to: "-pdf -file-line-error -halt-on-error -interaction=nonstopmode")

  The extra arguments to be passed to the LaTeX engine. By default, it is `-pdf -file-line-error -halt-on-error -interaction=nonstopmode`. This tells `latexmk` to use `pdflatex`. Refer to [`latexmk` document](http://texdoc.net/texmf-dist/doc/support/latexmk/latexmk.pdf) for more information.

- `extra_system_packages` (optional, defaults to: "")

  The extra packages to be installed by [`apk`](https://pkgs.alpinelinux.org/packages) separated by space. For example, `extra_system_packages: "inkscape"` will install the package `inkscape` to allow using SVG images in your LaTeX document.

- `extra_fonts` (optional, defaults to: "")

  Install extra `.ttf`/`.otf` fonts to be used by `fontspec`. You can also pass multiple files as a multi-line string. Each file path will be interpreted as bash glob pattern. For example:

  ```yaml
    - uses: zydou/latex-action@v3
      with:
        root_file: main.tex
        extra_fonts: |
          ./path/to/custom.ttf
          ./fonts/*.otf
  ```

- `pre_compile` (optional, defaults to: "")

  Arbitrary bash codes to be executed before compiling LaTeX documents. For example, `pre_compile: "tlmgr update --self && tlmgr update --all"` to update all TeXLive packages.

- `post_compile` (optional, defaults to: "")

  Arbitrary bash codes to be executed after compiling LaTeX documents. For example, `post_compile: "latexmk -c"` to clean up temporary files.

- `texlive_version` (optional, defaults to: "latest")

  The TeX Live version to be used. Currently, you can choose from `2018`, `2019`, `2020`, `2021`, `2022`, `2023`, or `latest`. (These choices may be outdated, please [check this page for the latest choices](https://github.com/zydou/texlive))

- `base_image` (optional, defaults to: "trixie")

  The base image version to be used. Currently, you can choose from `buster`, `bullseye`, `bookworm`, `trixie`, `xenial`, `bionic`, `focal`, or `jammy`. (These choices may be outdated, please [check this page for the latest choices](https://github.com/zydou/texlive))

**The following inputs are only valid if the input `compiler` is not changed.**

- `latexmk_shell_escape` (optional, defaults to: "false")

  Instruct `latexmk` to enable `--shell-escape`.

- `latexmk_use_lualatex` (optional, defaults to: "false")

  Instruct `latexmk` to use LuaLaTeX.

- `latexmk_use_xelatex` (optional, defaults to: "false")

  Instruct `latexmk` to use XeLaTeX.

## Example

```yaml
name: Build LaTeX

on:
  workflow_dispatch:
  push:
  pull_request:

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  build_latex:
    strategy:
      fail-fast: false
      matrix:
        # choose from 2018 to 2023, or latest
        texlive_version: [2023, 2022, 2021]
        # base_image: [buster, bullseye, bookworm, trixie, xenial, bionic, focal, jammy]
    name: Build with texlive-${{ matrix.texlive_version }}
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v3

      - name: Compile LaTeX document
        uses: zydou/latex-action@v3
        with:
          texlive_version: ${{ matrix.texlive_version }}
          # base_image: ${{ matrix.base_image }}
          work_in_root_file_dir: true
          continue_on_error: true
          root_file: |
            **/*.tex

      - name: Upload all assets to CI artifacts
        uses: actions/upload-artifact@v3
        with:
          name: latex
          path: |
            ./*
            !.git
            !.github

      - name: Collect pdf files
        run: |
          mkdir public
          find . -type f -name "*.pdf" -exec cp {} public \;

      - name: Push pdf files to texlive-${{matrix.texlive_version}} branch
        if: github.event_name != 'pull_request' && github.ref_name == github.event.repository.default_branch
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: texlive-${{ matrix.texlive_version }}
          folder: ./public
          single-commit: true
          commit-message: ${{ github.event.head_commit.message }}
```

## FAQs

### How to use XeLaTeX or LuaLaTeX instead of pdfLaTeX?

By default, this action uses pdfLaTeX. If you want to use XeLaTeX or LuaLaTeX, you can set the `latexmk_use_xelatex` or `latexmk_use_lualatex` input respectively. For example:

```yaml
  - uses: zydou/latex-action@v3
    with:
      root_file: main.tex
      latexmk_use_xelatex: true
```

```yaml
  - uses: zydou/latex-action@v3
    with:
      root_file: main.tex
      latexmk_use_lualatex: true
```

Alternatively, you could create a `.latexmkrc` file. Refer to the [`latexmk` document](http://texdoc.net/texmf-dist/doc/support/latexmk/latexmk.pdf) for more information.

### How to enable `--shell-escape`?

To enable `--shell-escape`, set the `latexmk_shell_escape` input.

```yaml
  - uses: zydou/latex-action@v3
    with:
      root_file: main.tex
      latexmk_shell_escape: true
```

### Where is the PDF file? How to upload it?

The PDF file will be in the same folder as that of the LaTeX source in the CI environment. It is up to you on whether to upload it to some places. Here are some example.

- You can use [`@actions/upload-artifact`](https://github.com/actions/upload-artifact) to upload a zip containing the PDF file to the workflow tab. For example you can add

  ```yaml
    - uses: actions/upload-artifact@v3
      with:
        name: PDF
        path: main.pdf
  ```

  It will result in a `PDF.zip` being uploaded with `main.pdf` contained inside.

- You can use [`@softprops/action-gh-release`](https://github.com/softprops/action-gh-release) to upload PDF file to the Github Release.

- You can use [`@JamesIves/github-pages-deploy-action`](https://github.com/JamesIves/github-pages-deploy-action) to upload PDF file to a git branch. For example, you can upload to the `gh-pages` branch in your repo, so you can view the document using Github Pages.

- You can use normal shell tools such as `scp`/`git`/`rsync` to upload PDF file anywhere.

### How to add additional paths to the LaTeX input search path?

Sometimes you may have custom package (`.sty`) or class (`.cls`) files in other directories. If you want to add these directories to the LaTeX input search path, you can add them in `TEXINPUTS` environment variable. For example:

```yaml
  - name: Download custom template
    run: |
      curl -OL https://example.com/custom_template.zip
      unzip custom_template.zip
  - uses: zydou/latex-action@v3
    with:
      root_file: main.tex
    env:
      TEXINPUTS: '.:./custom_template//:'
```

You can find more information of `TEXINPUTS` [here](https://tex.stackexchange.com/a/93733).

### It fails to build the document, how to solve it?

- Try to solve the problem by examining the build log.
- Try to build the document locally.
- You can also try to narrow the problem by creating a [minimal working example][mwe] to reproduce the problem.
- [Open an issue](https://github.com/xu-cheng/latex-action/issues/new) if you need help. Please include a [minimal working example][mwe] to demonstrate your problem.

## License

MIT

[mwe]: https://tex.meta.stackexchange.com/questions/228/ive-just-been-asked-to-write-a-minimal-working-example-mwe-what-is-that
