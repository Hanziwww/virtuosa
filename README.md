# Virtuosa Project Structure Documentation

## Overview

**Virtuosa** is a command-line tool and Python package designed for single-cell RNA-sequencing (scRNA-seq) data analysis. It provides an end-to-end workflow, including preprocessing, analysis, and visualization of single-cell datasets. The project is structured to facilitate easy navigation, extensibility, and collaboration. The main functionalities are distributed across four core components: 'Butler', 'Servant', 'Painter', and 'Musician'.

- **Servant**: Responsible for direct interactions with `adata`, recording all operations performed on `adata`, as well as handling internal property operations. The 'Servant' records everything that happens to `adata` and is also responsible for saving data.
- **Butler**: Handles basic quality control, dimensionality reduction, visualization, and other preprocessing tasks prior to cell annotation.
- **Painter**: Manages all visualization functions, including color and palette assignment, and plotting.
- **Musician**: Responsible for downstream analysis workflows, such as intercellular communication.

## Project Structure

```
virtuosa/
├── .github/                         # GitHub Actions configuration
│   └── workflows/
│       └── ci.yml                   # Continuous Integration workflow configuration
├── docs/                            # Documentation directory
│   ├── conf.py                      # Sphinx configuration file
│   ├── index.rst                    # Documentation index
│   └── usage.md                     # Usage documentation
├── examples/                        # Example scripts and data
│   ├── example_analysis.py          # Example analysis script
│   └── example_data.h5ad            # Example single-cell data
├── src/                             # Source code root directory
│   └── virtuosa/                    # Virtuosa package source code
│       ├── __init__.py              # Package initialization file, exposes core API
│       ├── cli.py                   # CLI entry point, defines command line logic
│       ├── butler/                  # Butler module
│       │   ├── __init__.py          # Butler module initialization file
│       │   └── butler.py            # Preprocessing functions (e.g., QC, dimensionality reduction)
│       ├── servant/                 # Servant module
│       │   ├── __init__.py          # Servant module initialization file
│       │   └── servant.py           # Data handling, recording, and saving
│       ├── painter/                 # Painter module
│       │   ├── __init__.py          # Painter module initialization file
│       │   └── painter.py           # Visualization functions (e.g., plotting, color management)
│       ├── musician/                # Musician module
│       │   ├── __init__.py          # Musician module initialization file
│       │   └── musician.py          # Downstream analysis functions (e.g., intercellular communication)
│       ├── utils/                   # Utility functions module
│       │   ├── __init__.py          # Helper functions
│       │   └── helpers.py           # Common utility functions
│       └── data/                    # Data processing module
│           ├── __init__.py          # Data module initialization file
│           └── loaders.py           # Functions for data loading and saving
├── tests/                           # Tests directory
│   ├── test_cli.py                  # CLI tests
│   ├── test_butler.py               # Butler module unit tests
│   ├── test_servant.py              # Servant module unit tests
│   ├── test_painter.py              # Painter module unit tests
│   ├── test_musician.py             # Musician module unit tests
│   └── conftest.py                  # Pytest configuration and shared fixtures
├── .gitignore                       # Git ignore file
├── pyproject.toml                   # PEP 517/518 compliant project configuration
├── setup.cfg                        # Package metadata and dependencies
├── README.md                        # Project README file
├── LICENSE                          # License file (e.g., MIT, GPL)
└── requirements.txt                 # Dependency list
```

## Directory and File Descriptions

### .github/

- **workflows/**: Contains GitHub Actions workflow configuration files for CI/CD processes.
    - **ci.yml**: Configuration file for the continuous integration workflow. Runs tests and checks code quality on each push or pull request.

### docs/

- **conf.py**: Configuration file for Sphinx documentation. Defines settings for building the documentation.
- **index.rst**: The main entry point for the documentation, linking to various sections and modules.
- **usage.md**: Documentation detailing how to use the Virtuosa package and CLI commands.

### examples/

- **example\_analysis.py**: A script demonstrating how to use the Virtuosa package for single-cell analysis.
- **example\_data.h5ad**: Sample single-cell RNA-seq data for demonstration purposes.

### src/

- **virtuosa/**: The main source code for the Virtuosa package.
    - **__init__.py**: Initializes the package and exposes key functionalities.
    - **cli.py**: Entry point for the command-line interface, defining the available commands and their logic.
    - **butler/**: Butler module for basic quality control, dimensionality reduction, and visualization.
        - **__init__.py**: Initializes the butler module.
        - **butler.py**: Implements preprocessing functions.
    - **servant/**: Servant module responsible for interacting with `adata`, recording operations, and saving.
        - **__init__.py**: Initializes the servant module.
        - **servant.py**: Handles data operations, including recording and saving actions.
    - **painter/**: Painter module for creating plots and managing colors and palettes.
        - **__init__.py**: Initializes the painter module.
        - **painter.py**: Implements visualization functions.
    - **musician/**: Musician module responsible for downstream analyses such as intercellular communication.
        - **__init__.py**: Initializes the musician module.
        - **musician.py**: Contains functions for advanced downstream analysis.
    - **utils/**: Utility functions that support various operations within the package.
        - **__init__.py**: Initializes the utilities module.
        - **helpers.py**: Contains common helper functions.
    - **data/**: Data handling module for loading and saving datasets.
        - **__init__.py**: Initializes the data module.
        - **loaders.py**: Implements functions for data loading and format conversion.

### tests/

- **test\_cli.py**: Contains tests for the CLI functionality, ensuring command-line commands work as intended.
- **test\_butler.py**: Unit tests for the butler module.
- **test\_servant.py**: Unit tests for the servant module.
- **test\_painter.py**: Unit tests for the painter module.
- **test\_musician.py**: Unit tests for the musician module.
- **conftest.py**: Configuration file for pytest, defining shared fixtures and test configurations.

### .gitignore

Specifies files and directories to be ignored by Git, such as virtual environments and compiled files.

### pyproject.toml

Configuration file compliant with PEP 517/518, defining build system requirements and project metadata.

### setup.cfg

Configuration file that contains metadata for the package (e.g., name, version, author) and dependencies for the project.

### README.md

The main documentation file for the project, providing an overview, installation instructions, and usage examples.

### LICENSE

Contains the license under which the project is distributed (e.g., MIT, GPL).

### requirements.txt

Lists the package dependencies required to run the project. Used for easy installation of dependencies.

## Design Philosophy

The design philosophy of the **Virtuosa** package centers on interacting with `adata` through well-defined objects, which also keep a detailed record of every operation performed. By standardizing workflows, **Virtuosa** aims to ensure high-quality data analysis and allow researchers to plan their analysis paths effectively. This approach maintains data integrity, reproducibility, and transparency, thus facilitating collaborative and rigorous research.

## Getting Started

1. **Installation**:
   Clone the repository and install the package in editable mode:

   ```bash
   git clone https://github.com/yourusername/virtuosa.git
   cd virtuosa
   pip install -e .
   ```

2. **Using the CLI**:
   After installation, you can use the Virtuosa CLI commands:

   ```bash
   she-summon [core_object] [parameters]
   ```

   Example usage:

   ```bash
   she-summon butler --min-genes 200 --max-genes 2500
   she-summon servant --save-path output_data.h5ad
   she-summon painter --plot umap
   she-summon musician --analyze cell_communication
   ```

3. **Running Tests**:
   To run the tests, ensure you have installed the required dependencies and execute:

   ```bash
   pytest tests/
   ```