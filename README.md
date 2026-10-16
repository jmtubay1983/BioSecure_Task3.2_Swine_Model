![Static Badge](https://img.shields.io/badge/emulsion-1.2rc5-brightgreen) ![Static Badge](https://img.shields.io/badge/pyABC-0.12.15-blue)
# Model of a Farrow-to-Finish Swine Farm

This repository contains code and data for the farrow-to-finish swine farm model. The main components include the farrow-to-finish farm model Emulsion configuration file, a Python add-on script for farmer and animal movement simulation, and a Jupyter notebook for parameter estimation of the transmission parameters using Approximate Bayesian Computation with Sequential Monte Carlo simulation (ABC-SMC).

## Repository Structure

- `data/`: Folder containing the data used in the simulations.
- `data/modified_movements_10yr.csv`: Farmer movement data used in the simulations
- `LICENSE`: License file for the repository.
- `movement_12fatpens_outrans.py`: Python script add-on for simulating movements in the swine model.
- `parameter_estimation_notebook.ipynb`: Jupyter notebook for parameter estimation using ABC.
- `swine_model_weekly-12fatpens-FINAL.yaml`: EMULSION file for the swine model.
- `swine_model_weekly-12fatpens-weight-FINAL-swIAVs.yaml`: EMULSION file for the swine model (swIAVs version).
- `movement_12fatpens_swIAVs.py`: Python script add-on for simulating movements in the swine model (swIAVs version).

## Getting Started

### Prerequisites

Ensure you have the following packages installed:
- `Python 3.x`
- `emulsion==1.2rc5`
- `jupyter`
- `numpy`
- `pandas`
- `matplotlib`
- `pyabc`
- `docopt`
- `shutil`
- `uuid`
- `datetime`
- `csv`
- `dateutil`
- `random`

You can install some of the required packages using pip:
```bash
pip install numpy pandas matplotlib pyabc docopt python-dateutil emulsion==1.2rc5 betapert
```

## Running the Model and Parameter Estimation

### Running an instance of the model
To simulate an instance of the mode, open a terminal in the directory where your files are located, and type the following command:
````bash
emulsion run --plot swine_model_weekly-12fatpens-FINAL.yaml
````

Follow this link for more information and options: [Getting Started with EMULSION](https://sourcesup.renater.fr/www/emulsion-public/pages/Getting_started.html)

### Troubleshooting Python add-ons

Run EMULSION from the repository directory. Its `--code-path` defaults to the
current working directory, rather than the directory containing the YAML file.
If running elsewhere, set `--code-path` to this repository and `--input-dir` to
its `data` directory.

If EMULSION reports `module not found for level metapop`, use the same Python
environment as EMULSION and run this from the repository directory:

```bash
python -c "import movement_12fatpens_outrans"
```

The traceback identifies the underlying import error. EMULSION 1.2rc5 can also
show this message for a missing dependency inside the add-on. For example, if
the traceback names `betapert`, install it with `python -m pip install betapert`.

### Checking the default model

After installing the prerequisites, run the regression check:

```bash
python -m unittest discover -s tests -v
```

This runs two short simulations and checks that they finish, animal counts are
consistent, and life stages remain in their assigned herds. It does not validate
the scientific assumptions or the parameter-estimation notebook.

### Running the parameter estimation
To implement the parameter estimation framework, please open the `parameter_estimation_notebook.ipynb` notebook in Jupyter. Within the notebook, you can modify the values pertinent to the parameter estimation process. While this can be executed on a personal computer, utilizing a cluster for enhanced performance and efficiency is advisable.

For more information about using `pyABC`, please follow this link: [pyABC - distributed, likelihood-free inference](https://pyabc.readthedocs.io/en/latest/).
