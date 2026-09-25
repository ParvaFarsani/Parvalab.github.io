# DSCI 521 Milestone 3

This repository contains the source files for my personal Quarto website for DSCI 521 Milestone 3. The website includes two computational posts: one written in R and one written in Python.

The project uses `renv` to manage the R environment and `uv` to manage the Python environment.

## Software Requirements

The following software is required to rebuild the website:

- Quarto 1.10.18
- R 4.6.1
- `uv` 0.12.6

The R package environment is managed using `renv`. The required R packages and their versions are recorded in `renv.lock`.

The Python environment is managed using `uv`. The required Python packages and their versions are recorded in `pyproject.toml` and `uv.lock`.

## Clone the Repository

From a terminal, clone the repository:

```bash id="7h8fdm"
git clone git@github.com:ParvaFarsani/Parvalab.github.io.git
cd Parvalab.github.io
```

All remaining commands should be run from the top level of the repository unless otherwise stated.

## Restore the Python Environment

From the top level of the repository, run:

```bash id="9yl8mc"
uv sync
```

This creates the project's `.venv` and installs the Python packages recorded in `uv.lock`.

The Python environment includes the packages required to execute the Python computational post.

## Restore the R Environment

Start R from the top level of the repository.

The project `.Rprofile` activates the `renv` environment. In the R console, run:

```r id="vn8pwr"
renv::restore()
```

This installs the R packages and versions recorded in `renv.lock`.

After the packages have been restored, exit R and return to the terminal.

## Render the Website

From the top level of the repository, run:

```bash id="hpswvk"
uv run quarto render
```

Using `uv run` ensures that Quarto uses the Python environment associated with this project when executing the Python computational post.

Quarto also starts R from the top level of the repository, allowing the project's `.Rprofile` to activate the `renv` environment.

The rendered website is written to:

```text id="fjox0m"
docs/
```

The main rendered page is:

```text id="h6rmq5"
docs/index.html
```

## Preview the Website Locally

To preview the website locally, run the following command from the top level of the repository:

```bash id="crlrcf"
uv run quarto preview
```

Quarto will provide a local URL that can be opened in a web browser.

## Computational Posts

The website contains two new computational posts.

### R Post

The R post explores the Palmer Penguins dataset using data summaries and visualizations. It investigates differences in body mass among penguin species and the relationship between flipper length and body mass.

### Python Post

The Python post also uses the Palmer Penguins dataset and performs computational analysis using Python.

Both posts contain executable code and generated output that are produced when the website is rendered.

## Data Source

Both computational posts use the Palmer Penguins dataset from Palmer Station Antarctica LTER:

https://allisonhorst.github.io/palmerpenguins/

The dataset is provided through the `palmerpenguins` packages used by the project rather than being stored as a separate data file in this repository.

Because the dataset is distributed with the required packages, the computational posts do not need to download the dataset from an external website each time the site is rendered.

However, an internet connection is required when initially restoring the R and Python environments if the required packages are not already available locally.

## Project Structure

```text id="c21i6x"
.
├── _quarto.yml
├── README.md
├── index.qmd
├── about.qmd
├── blog.qmd
├── pyproject.toml
├── uv.lock
├── .python-version
├── renv.lock
├── .Rprofile
├── renv/
│   └── activate.R
├── posts/
│   ├── first-weeks/
│   ├── penguins-r/
│   │   └── index.qmd
│   └── penguins-python/
│       └── index.qmd
└── docs/
```

The `posts/` directory contains the source files for the website posts.

The Python environment is defined by `pyproject.toml`, `uv.lock`, and `.python-version`.

The R environment is defined by `renv.lock`, `.Rprofile`, and `renv/activate.R`.

The `docs/` directory contains the rendered website published using GitHub Pages.