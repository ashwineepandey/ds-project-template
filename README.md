# DS Project Template

## Template Structure
ds-project-template # Parent directory of the template
├── conf            # Project configuration files
├── data            # Local project data (not committed to version control)
├── docs            # Project documentation
├── logs            # Project output logs (not committed to version control)
├── notebooks       # Project related Jupyter notebooks (can be used for experimental code before moving the code to src)
├── README.md       # Project README
├── setup.cfg       # Configuration options for `pytest` when doing `kedro test` and for the `isort` utility when doing `kedro lint`
└── src             # Project source code

### Hidden files and folders
ds-project-template
├── .coveragerc     # Configuration file for the coverage reporting when doing `kedro test`
├── .gitignore      # Prevent staging of unnecessary files to `git`
└── pyproject.toml  # Identifies the project root and [contains configuration information](../faq/architecture_overview.md#kedro-project)

## Some details:

### `conf`

The conf folder contains two subfolders for storing configuration information: `base` and `local`.

`conf/base/`

For project-specific settings to share across different installations (for example, with different users), you should use the base subfolder of conf.

The folder contains three files for the example, but you can add others as you require:

`catalog.yml` - Configures the Data Catalog with the file paths and load/save configuration required for different datasets
`logging.yml` - Uses Python’s default logging library to set up logging
`parameters.yml` - Allows you to define parameters for machine learning experiments e.g. train / test split and number of iterations
conf/local/

The `local` subfolder of `conf` is used for settings that should not be shared, such as access credentials, custom editor configuration, personal IDE configuration and other sensitive or personal content. It is specific to user and installation. The contents of `conf/local/` is ignored by git (through inclusion in `.gitignore`). By default, Kedro creates one file, `credentials.yml`, in `conf/local`.

### `data`

The data folder contains a number of subfolders to store project data. We recommend that you put raw data into raw and move processed data to other subfolders according to data engineering convention.

The example project has a single file, iris.csv, that contains the Iris dataset. The subfolders of data are ignored by git through inclusion in .gitignore since data is more frequently stored elsewhere, such as in an S3 bucket. However, if you are familiar with .gitignore you can edit it, if you are confident that you need to manage your data in git.

### `src`

This subfolder contains the project’s source code. The src folder contains two subfolders:

get_started/ This is the Python package for your project
tests/ The subfolder for unit tests for your project. Projects are preconfigured to run tests using pytest when you call kedro test from the project’s root directory
What best practice should I follow to avoid leaking confidential data?

Do not commit data to version control.
Do not commit notebook output cells (data can easily sneak into notebooks when you don’t delete output cells).
Do not commit credentials in `conf/`. Use only the conf/local/ folder for sensitive information like access credentials.


<!-- ## Overview

This is your new Kedro project, which was generated using `Kedro 0.18.2`.

Take a look at the [Kedro documentation](https://kedro.readthedocs.io) to get started.

## Rules and guidelines

In order to get the best out of the template:

* Don't remove any lines from the `.gitignore` file we provide
* Make sure your results can be reproduced by following a [data engineering convention](https://kedro.readthedocs.io/en/stable/faq/faq.html#what-is-data-engineering-convention)
* Don't commit data to your repository
* Don't commit any credentials or your local configuration to your repository. Keep all your credentials and local configuration in `conf/local/`

## How to install dependencies

Declare any dependencies in `src/requirements.txt` for `pip` installation and `src/environment.yml` for `conda` installation.

To install them, run:

```
pip install -r src/requirements.txt
```

## How to run your Kedro pipeline

You can run your Kedro project with:

```
kedro run
```

## How to test your Kedro project

Have a look at the file `src/tests/test_run.py` for instructions on how to write your tests. You can run your tests as follows:

```
kedro test
```

To configure the coverage threshold, go to the `.coveragerc` file.

## Project dependencies

To generate or update the dependency requirements for your project:

```
kedro build-reqs
```

This will `pip-compile` the contents of `src/requirements.txt` into a new file `src/requirements.lock`. You can see the output of the resolution by opening `src/requirements.lock`.

After this, if you'd like to update your project requirements, please update `src/requirements.txt` and re-run `kedro build-reqs`.

[Further information about project dependencies](https://kedro.readthedocs.io/en/stable/kedro_project_setup/dependencies.html#project-specific-dependencies)

## How to work with Kedro and notebooks

> Note: Using `kedro jupyter` or `kedro ipython` to run your notebook provides these variables in scope: `context`, `catalog`, and `startup_error`.
>
> Jupyter, JupyterLab, and IPython are already included in the project requirements by default, so once you have run `pip install -r src/requirements.txt` you will not need to take any extra steps before you use them.

### Jupyter
To use Jupyter notebooks in your Kedro project, you need to install Jupyter:

```
pip install jupyter
```

After installing Jupyter, you can start a local notebook server:

```
kedro jupyter notebook
```

### JupyterLab
To use JupyterLab, you need to install it:

```
pip install jupyterlab
```

You can also start JupyterLab:

```
kedro jupyter lab
```

### IPython
And if you want to run an IPython session:

```
kedro ipython
```

### How to convert notebook cells to nodes in a Kedro project
You can move notebook code over into a Kedro project structure using a mixture of [cell tagging](https://jupyter-notebook.readthedocs.io/en/stable/changelog.html#release-5-0-0) and Kedro CLI commands.

By adding the `node` tag to a cell and running the command below, the cell's source code will be copied over to a Python file within `src/<package_name>/nodes/`:

```
kedro jupyter convert <filepath_to_my_notebook>
```
> *Note:* The name of the Python file matches the name of the original notebook.

Alternatively, you may want to transform all your notebooks in one go. Run the following command to convert all notebook files found in the project root directory and under any of its sub-folders:

```
kedro jupyter convert --all
```

### How to ignore notebook output cells in `git`
To automatically strip out all output cell contents before committing to `git`, you can run `kedro activate-nbstripout`. This will add a hook in `.git/config` which will run `nbstripout` before anything is committed to `git`.

> *Note:* Your output cells will be retained locally.

## Package your Kedro project

[Further information about building project documentation and packaging your project](https://kedro.readthedocs.io/en/stable/tutorial/package_a_project.html) -->
