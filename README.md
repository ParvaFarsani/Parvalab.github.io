# DSCI 521 Milestone 3

This repository contains the source files for my personal Quarto website for DSCI 521 Milestone 3.

The website includes computational posts written in both R and Python. The two main Milestone 3 computational posts analyze the Palmer Penguins dataset separately in R and Python. The repository also contains a bonus computational post that uses R and Python together in the same Quarto document and passes a result calculated in R to Python.

The project is designed to be reproducible. The R environment is managed with `renv`, and the Python environment is managed with `uv`.

## Software Requirements

The following software versions were used to build and test this project:

- Quarto 1.10.18
- R 4.6.1
- Python 3.14
- `uv` 0.12.6

The R package environment is managed using `renv`. The required R packages and their versions are recorded in `renv.lock`.

The Python environment is managed using `uv`. The Python dependencies are defined in `pyproject.toml`, exact resolved versions are recorded in `uv.lock`, and the Python version is pinned in `.python-version`.

The bonus R and Python post uses the R package `reticulate` to allow Python code to access an object created in R. `reticulate` and its dependencies are included in `renv.lock`.

## Clone the Repository

Clone the repository from a terminal:

```bash
git clone git@github.com:ParvaFarsani/Parvalab.github.io.git
cd Parvalab.github.io
```

All commands below should be run from the top level of the repository unless otherwise stated.

## Restore the Python Environment

From the top level of the repository, run:

```bash
uv sync
```

This creates the project's `.venv` and installs the Python packages recorded in `uv.lock`.

The Python version for the project is specified in:

```text
.python-version
```

The project uses Python 3.14.

The Python environment includes the packages required for the Python computational post and for executing Python code during the website build.

## Restore the R Environment

Start R from the top level of the repository:

```bash
R
```

The project-level `.Rprofile` activates the `renv` environment.

Inside the R console, run:

```r
renv::restore()
```

This restores the R packages and package versions recorded in `renv.lock`.

The R environment includes the packages required for the R computational post as well as `reticulate`, which is used by the bonus post to allow R and Python to communicate in the same Quarto document.

After the packages have been restored, exit R:

```r
q()
```

If prompted to save the workspace image, it is not necessary to save it.

## Render the Website

After restoring both environments, render the complete website from the top level of the repository:

```bash
uv run quarto render
```

Using `uv run` makes the project's Python environment available while Quarto renders the website.

When R documents are rendered, the project `.Rprofile` activates the `renv` environment. This allows the R computational code to use the package versions recorded in `renv.lock`.

The same build command renders the R post, Python post, bonus R/Python post, and the other pages of the website.

A successful full render creates the website in:

```text
docs/
```

The main rendered page is:

```text
docs/index.html
```

## Preview the Website Locally

To preview the website locally, run:

```bash
uv run quarto preview
```

Quarto will start a local preview server and display a local URL. Open that URL in a web browser to view the website.

## Computational Posts

### R: Palmer Penguins Analysis

Source file:

```text
posts/penguins-r/index.qmd
```

This post uses R to explore the Palmer Penguins dataset.

The analysis includes data inspection, cleaning and summarization, comparisons among penguin species, and visualizations. It examines body mass differences among species and relationships between penguin measurements such as flipper length and body mass.

The code and generated output are visible in the rendered post. Figures and numerical results are generated from the R code when the website is rendered.

### Python: Palmer Penguins Analysis

Source file:

```text
posts/penguins-python/index.qmd
```

This post analyzes the Palmer Penguins dataset using Python.

The analysis includes data inspection and cleaning, grouped summaries, comparisons of body mass among species, correlations among numerical variables, and visualizations of relationships between penguin measurements.

The Python post uses packages including `pandas`, `matplotlib`, and `palmerpenguins`.

The figures, tables, and numerical results are generated directly from the Python code during rendering.

### Bonus: R and Python Together

Source file:

```text
posts/r-and-python/index.qmd
```

The bonus post demonstrates communication between R and Python within a single Quarto document.

The workflow is:

```text
Palmer Penguins data
        |
        v
        R
        |
        v
penguin_summary
        |
        v
      Python
        |
        v
Additional calculation
```

First, R loads the Palmer Penguins data and calculates the mean body mass for each penguin species. This result is stored in an R object named:

```text
penguin_summary
```

A Python code chunk then accesses the R object through:

```python
r.penguin_summary
```

The transferred object is stored in Python and used to determine which species has the highest mean body mass.

Therefore, the Python section does not independently repeat the original R calculation. It uses a result that was first computed in R.

The R/Python communication is supported by `reticulate`, which is included in the project's R environment and recorded in `renv.lock`.

## Data Source

The computational posts use the Palmer Penguins dataset from Palmer Station Antarctica LTER.

Dataset website:

https://allisonhorst.github.io/palmerpenguins/

The dataset is accessed through the `palmerpenguins` packages used by the project rather than being stored as a separate data file in this repository.

Because the data are distributed with the installed packages, the computational posts do not need to download the dataset from an external website each time the website is rendered.

An internet connection is therefore not required to retrieve the dataset during a normal render after the environments have been restored.

However, an internet connection may be required during the initial environment restoration to download R and Python packages that are not already available locally.

## Reproducible Environments

### Python

The Python environment is defined by:

```text
pyproject.toml
uv.lock
.python-version
```

`pyproject.toml` defines the Python project and its required dependencies.

`uv.lock` records the resolved Python dependency versions.

`.python-version` pins the Python version used by the project.

To recreate the Python environment:

```bash
uv sync
```

The generated `.venv/` directory is local to the computer and is not committed to the repository.

### R

The R environment is defined by:

```text
renv.lock
.Rprofile
renv/activate.R
```

`renv.lock` records the R packages and package versions required by the project.

`.Rprofile` activates the project's `renv` environment when R starts from the repository.

`renv/activate.R` contains the project activation code used by `renv`.

To recreate the R package environment:

```r
renv::restore()
```

The local `renv/library/` directory is not committed to the repository.

## Rebuild From a Fresh Clone

The complete fresh-clone workflow is:

```bash
git clone git@github.com:ParvaFarsani/Parvalab.github.io.git
cd Parvalab.github.io
uv sync
R
```

Then, inside R:

```r
renv::restore()
q()
```

After returning to the terminal, render the complete website:

```bash
uv run quarto render
```

The finished website will be generated in:

```text
docs/
```

The homepage is:

```text
docs/index.html
```

To preview it using Quarto:

```bash
uv run quarto preview
```

## Project Structure

```text
.
├── _quarto.yml
├── README.md
├── index.qmd
├── about.qmd
├── blog.qmd
├── styles.css
├── pyproject.toml
├── uv.lock
├── .python-version
├── renv.lock
├── .Rprofile
├── renv/
│   └── activate.R
├── posts/
│   ├── first-weeks/
│   │   └── index.qmd
│   ├── penguins-r/
│   │   └── index.qmd
│   ├── penguins-python/
│   │   └── index.qmd
│   └── r-and-python/
│       └── index.qmd
└── docs/
    ├── .nojekyll
    └── index.html
```

The `posts/` directory contains the source files for the website posts.

The main Milestone 3 computational posts are:

```text
posts/penguins-r/index.qmd
posts/penguins-python/index.qmd
```

The bonus mixed-language post is:

```text
posts/r-and-python/index.qmd
```

The `docs/` directory contains the rendered website used for GitHub Pages.

The `docs/.nojekyll` file ensures that GitHub Pages serves the rendered Quarto website without Jekyll processing.

## Files Not Committed

Generated environments, temporary Quarto files, and operating-system metadata should not be committed.

The top-level `.gitignore` excludes:

```text
.quarto/
_site/
.DS_Store
.venv/
renv/library/
```

This keeps local environments and temporary build files out of version control while keeping the reproducibility files such as `uv.lock` and `renv.lock` in the repository.

## Reproducibility Summary

To reproduce this project from a fresh clone:

1. Clone the repository.
2. Run `uv sync` to restore the Python environment.
3. Start R and run `renv::restore()` to restore the R environment.
4. Return to the repository root.
5. Run `uv run quarto render`.
6. Open or preview the website generated in `docs/`.

The website can therefore be rebuilt from the source files and committed environment specifications without using the original local Python `.venv` or R package library.