# Letter Classification

A decision tree analysis that predicts uppercase English letters from 16 numerical image attributes. Developed as a school assignment, this project compares an unrestricted tree with a tree selected through cost-complexity pruning and cross-validation.

## Analysis

The dataset contains 20,000 observations across 26 letter classes. The notebook examines class balance, feature distributions, missing values, duplicate records, and overlap between training and test feature vectors. The first 16,000 rows in the supplied CSV are used for training, and the remaining 4,000 are reserved for testing.

An unrestricted decision tree establishes baseline performance. A two-stage search uses 10-fold cross-validation on the training data to select the pruning parameter. The final models are evaluated using accuracy, macro precision, macro recall, and class-specific errors. Feature importance and the upper levels of the pruned tree support model interpretation.

## Findings

The saved notebook reports the following results:

| Metric | Unrestricted tree | Pruned tree |
| --- | ---: | ---: |
| Training accuracy | 100.00% | 98.00% |
| Test accuracy | 87.38% | 87.05% |
| Macro precision | 0.8747 | 0.8729 |
| Macro recall | 0.8746 | 0.8715 |
| Tree depth | 29 | 26 |
| Leaves | 1,946 | 1,525 |

Pruning reduces the number of leaves by approximately 22%, but it does not improve test accuracy. This analysis illustrates the tradeoff between model simplicity and predictive performance.

Some identical feature vectors appear in both training and test sets. Since the images are represented by a limited set of integer-valued attributes, feature equality does not establish image identity, but this overlap limits how confidently test results describe performance on wholly new feature profiles. Duplicate rows are retained, and cross-validation uses shuffled KFold rather than grouping duplicate feature vectors.

## Files

- [Analysis notebook](Unit6_Assignment.ipynb): code, saved figures, model evaluation, and interpretation.
- `letter.csv`: 16 image attributes and the target column `class`.
- `requirements.txt`: notebook dependencies.

## Run locally

Use Python 3.11 or newer. From the repository directory:

```sh
python -m venv .venv
```

Activate the environment on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

Or on macOS/Linux:

```sh
source .venv/bin/activate
```

Then install dependencies and open the notebook:

```sh
python -m pip install -r requirements.txt
python -m jupyterlab
```

Open `Unit6_Assignment.ipynb` and run all cells from the repository directory. The pruning searches fit hundreds of trees and take longer than the exploratory sections. Saved outputs are included so the analysis can also be read without running it. Dependency versions are not locked to the original environment, so results may vary slightly with software versions.

## Data attribution

Slate, D. (1991). *Letter Recognition* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5ZP40.

The [UCI Letter Recognition dataset](https://archive.ics.uci.edu/dataset/59/letter+recognition) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This project uses a CSV version with adapted column names and the target stored as `class`. The supplied file and its row order are preserved for compatibility with the original notebook.
