# Dataset Playground — CSV Data for Machine Learning Practice

Nine CSV tables for learning data cleaning, exploratory analysis, classification and regression with Python, R or another data tool.

## 🔎 Overview

Start with Iris for classification or Salary for regression, then explore missing values in Titanic and the customer, sales and sensor tables. These files provide practice inputs; the repository includes no trained models, notebooks or evaluation results.

Provenance and licensing are not recorded. Treat the tables as learning material of unverified origin and read the [source and reuse notes](#source-and-reuse-notes) before redistribution.

## ✨ Features

| Dataset | Rows | Columns | Suggested exercise / target |
|---|---:|---:|---|
| [Iris.csv](Iris.csv) | 150 | 5 | Flower classification: `species` |
| [Salary.csv](Salary.csv) | 205 | 2 | Experience/salary regression: `salary` |
| [Purchase.csv](Purchase.csv) | 10 | 4 | Missing-value handling; toy classification: `Purchased` |
| [Titanic.csv](Titanic.csv) | 891 | 12 | Missing values and classification: `Survived` |
| [College.csv](College.csv) | 777 | 19 | Institutional EDA; optional classification: `Private` |
| [customer_data.csv](customer_data.csv) | 1,000 | 9 | Missing values, category cleanup; optional regression: `Purchase_Amount` |
| [sales_data.csv](sales_data.csv) | 1,000 | 8 | Outliers and missing values; optional classification: `Is_Fraudulent` |
| [reviews_data.csv](reviews_data.csv) | 1,000 | 6 | Text preprocessing; sentiment classification: `Sentiment` |
| [sensor_data.csv](sensor_data.csv) | 1,000 | 5 | Timestamp parsing and missing sensor readings |

Counts exclude the header. The first College column is unnamed and contains college names; it is included in the 19-column count. See the [schema and quality reference](documentation.md) for exact fields and empty-cell counts.

## 🚀 Quick start

Clone the repository and load one local file:

```bash
git clone https://github.com/gcfernando/datasets.git
cd datasets
python -m pip install pandas
```

```python
import pandas as pd

iris = pd.read_csv("Iris.csv")
print(iris.shape)  # (150, 5)
print(iris.columns.tolist())
```

## 📦 Prerequisites and installation

The CSV files require no runtime installation. For the examples above, use Python with pandas installed in your chosen environment. Python and pandas versions are not pinned in this repository. Spreadsheet tools and R can also import the tables; preserve exact filename case when scripting on case-sensitive systems.

## 💡 Usage

Inspect missing values and load college names as an index:

```python
import pandas as pd

titanic = pd.read_csv("Titanic.csv")
college = pd.read_csv("College.csv", index_col=0)
print(titanic.shape)         # (891, 12)
print(college.shape)         # (777, 18): name column is now the index
print(titanic.isna().sum())
```

For experiments, split training and evaluation data before fitting imputers, scalers or encoders. For sensor time-series exercises, first inspect ordering, duplicate timestamps and sampling intervals; the presence of a timestamp column alone does not establish suitability for forecasting. Avoid using identifiers, names, email addresses or phone numbers as default predictive features.

## 🏗️ Architecture

All nine CSV files live at the repository root. [documentation.md](documentation.md) is a data dictionary and quality reference. `_config.yml`, `_layouts` and `assets` support the documentation site; they are unrelated to data processing.

## 🧪 Development and testing

There are no committed generators, pipelines or automated tests. A safe local verification with Python's standard library is:

```python
import csv
from pathlib import Path

for path in sorted(Path(".").glob("*.csv")):
    with path.open(encoding="utf-8-sig", newline="") as stream:
        rows = list(csv.reader(stream))
    header, records = rows[0], rows[1:]
    assert all(len(row) == len(header) for row in records), path.name
    print(path.name, len(records), len(header))
```

The documentation review parsed all files to verify counts, headers and empty cells. It did not train models or verify original dataset sources.

## 🛠️ Troubleshooting and limitations

- **Unnamed College column:** use `index_col=0`, or assign an explicit name after import.
- **Missing values:** Purchase, Titanic, customer, sales and sensor tables contain empty cells. Define a preprocessing policy before modeling.
- **Small sample:** Purchase has only ten rows and is unsuitable for reliable model evaluation.
- **Unknown origin:** apparent generated patterns do not prove that data is synthetic. No real-world representativeness or label quality is established.
- **Reuse rights:** a familiar dataset name does not establish the source or license of this particular copy.

## 🤝 Contributing

For a dataset addition or correction, record its source URL, author, license, collection/generation method, schema, units and known quality limitations. Do not add personal or confidential records. Update counts and the data dictionary when changing a CSV.

## 🔒 Security

Keep credentials and private records out of examples and issues. Use a private reporting option if available, or contact the maintainer privately for sensitive data concerns. No dedicated security policy is committed.

## 📄 Support and license

<a id="source-and-reuse-notes"></a>

### Source and reuse notes

No license file or per-dataset provenance record is present in this checkout. Confirm the origin and applicable reuse rights before redistributing any file; this repository's availability does not itself grant a license.

Use [repository issues](https://github.com/gcfernando/datasets/issues) for schema corrections or missing source information.

[Schema and quality reference](documentation.md) · [Python machine-learning examples](https://github.com/gcfernando/python_codes/tree/main/ML)
