---
layout: default
title: "Machine Learning Practice Datasets — Documentation and Guides"
description: "CSV datasets for learning classification, regression, sentiment analysis, time-series forecasting and data cleaning."
permalink: /documentation/
---

Browse the published guides, examples and reference pages for **Machine Learning Practice Datasets**. Each guide has a readable web page; the Markdown sources remain available on GitHub.

## 🔎 Schema and quality reference

Use the [README](readme.md) for dataset selection and pandas examples. This reference records the exact columns and empty-cell counts in the committed CSV files; suggested modeling targets are exercises, not an assertion that the tables are representative or well-labeled.

Empty-cell counts below include empty or whitespace-only field values, excluding headers. They do not count every possible missing-value marker. The additional checks below cover exact duplicate rows, selected numeric bounds and date parsing; they do not establish validity or provenance.

| File | Rows | Columns | Empty cells |
|---|---:|---:|---:|
| [College.csv](College.csv) | 777 | 19 | 0 |
| [customer_data.csv](customer_data.csv) | 1000 | 9 | 878 |
| [Iris.csv](Iris.csv) | 150 | 5 | 0 |
| [Purchase.csv](Purchase.csv) | 10 | 4 | 2 |
| [reviews_data.csv](reviews_data.csv) | 1000 | 6 | 0 |
| [Salary.csv](Salary.csv) | 205 | 2 | 0 |
| [sales_data.csv](sales_data.csv) | 1000 | 8 | 640 |
| [sensor_data.csv](sensor_data.csv) | 1000 | 5 | 493 |
| [Titanic.csv](Titanic.csv) | 891 | 12 | 866 |

## 📚 Data dictionary

### College.csv

`(unnamed college-name column)`, `Private`, `Apps`, `Accept`, `Enroll`, `Top10perc`, `Top25perc`, `F.Undergrad`, `P.Undergrad`, `Outstate`, `Room.Board`, `Books`, `Personal`, `PhD`, `Terminal`, `S.F.Ratio`, `perc.alumni`, `Expend`, `Grad.Rate`.

### customer_data.csv

`Customer_ID`, `Name`, `Age`, `Gender`, `Email`, `Phone`, `Country`, `Signup_Date`, `Purchase_Amount`.

### Iris.csv

`sepal_length`, `sepal_width`, `petal_length`, `petal_width`, `species`.

### Purchase.csv

`Employee`, `Age`, `Salary`, `Purchased`.

### reviews_data.csv

`Review_ID`, `Customer_ID`, `Review_Text`, `Rating`, `Sentiment`, `Review_Date`.

### Salary.csv

`years_experience`, `salary`.

### sales_data.csv

`Transaction_ID`, `Customer_ID`, `Transaction_Date`, `Product_Category`, `Payment_Method`, `Transaction_Amount`, `Discount_Applied`, `Is_Fraudulent`.

### sensor_data.csv

`Sensor_ID`, `Timestamp`, `Temperature`, `Humidity`, `Pressure`.

### Titanic.csv

`PassengerId`, `Survived`, `Pclass`, `Name`, `Sex`, `Age`, `SibSp`, `Parch`, `Ticket`, `Fare`, `Cabin`, `Embarked`.

## 🧪 Interpretation notes

- College's first column has no header. Using `index_col=0` leaves 18 data columns plus the college-name index.
- Customer gender values mix labels such as `M`, `F`, `Male` and `Female`; define a normalization policy rather than assuming one encoding.
- Purchase has ten rows and two empty cells, so it is a small preprocessing example.
- Sales includes a fraud label and Reviews a sentiment label, but neither labeling methodology nor ground-truth quality is documented.
- Sensor has timestamps, but no acquisition or sampling specification; inspect it before any forecasting exercise.
- No generator, provenance record or license file is present. Do not infer that named or generated-looking records are proven synthetic.

## 🧪 Additional full-file quality checks

All records were parsed with the CSV reader. Every row has the expected field count. `Iris.csv` has **three duplicate rows beyond the first occurrence** when comparing all five fields exactly; the other eight files have no exact full-row duplicates. This does not establish whether repeated measurements are errors, and removing them should be an explicit analysis choice.

In `College.csv`, one `PhD` value exceeds 100 (maximum **103**) and one `Grad.Rate` value exceeds 100 (maximum **118**). Investigate these values before interpreting those fields as percentages; this review does not correct or explain their source.

Use explicit date formats instead of relying on locale inference:

| File / field | Python or pandas format | Observed ordering |
|---|---|---|
| `customer_data.csv` / `Signup_Date` | `%m/%d/%Y` | Unsorted; 770 distinct dates |
| `sales_data.csv` / `Transaction_Date` | `%Y-%m-%d` | Unsorted; 770 distinct dates |
| `reviews_data.csv` / `Review_Date` | `%d-%m-%Y` | Unsorted; 552 distinct dates |
| `sensor_data.csv` / `Timestamp` | `%Y/%m/%d %H:%M:%S` | 1,000 unique timestamps, ascending with 600 seconds between adjacent rows |

Every nonempty date in each field parses with its listed format. The sensor table interleaves ten sensor IDs, so the global ten-minute spacing is not a per-sensor sampling guarantee. Group by `Sensor_ID` and inspect each series before resampling. No time-zone or measurement-unit metadata is committed.

`Customer_ID` is unique in the customer table, and all sales/review customer references match an ID there. A join still needs an explicit purpose and careful feature selection: identifier consistency does not verify record provenance or predictive validity.

The generated page/source navigation below is retained for the documentation site.

## Read online

<table>
<thead><tr><th>Guide</th><th>Markdown or HTML source</th></tr></thead>
<tbody>
{% assign guides = site.html_pages | sort: 'url' %}
{% for guide in guides %}{% if guide.sitemap != false and guide.url != page.url and guide.url != '/404.html' %}
<tr><td><a href="{{ guide.url | absolute_url }}">{{ guide.title | default: guide.name | escape }}</a></td><td><a href="https://github.com/{{ site.repository }}/blob/main/{{ guide.path | uri_escape }}">View source</a></td></tr>
{% endif %}{% endfor %}
{% for guide in site.static_files %}{% if guide.extname == '.html' and guide.sitemap != false %}
<tr><td><a href="{{ guide.path | uri_escape | absolute_url }}">{% if guide.path == '/Linux_Commands/index.html' %}Linux Command Reference{% elsif guide.path contains 'AI-Learning-Atlas' %}AI Learning Atlas{% elsif guide.path contains 'ai_coding_plugins_beginners_guide' %}AI Coding Add-ons: Beginner’s Guide{% elsif guide.path contains 'Wifi Radar' %}WiFi Radar — static interface preview{% else %}{{ guide.name | escape }} — {{ guide.path | escape }}{% endif %}</a></td><td><code>{{ guide.path | escape }}</code></td></tr>
{% endif %}{% endfor %}
</tbody>
</table>

## Markdown source library

[View this documentation index source](https://github.com/{{ site.repository }}/blob/main/documentation.md). These are the authored Markdown files. Some are package-specific documents or alternate source formats of the same guide.

{% assign sources = site.static_files | sort: 'path' %}
{% for source in sources %}{% if source.extname == '.md' %}
- [{{ source.path | escape }}](https://github.com/{{ site.repository }}/blob/main{{ source.path | uri_escape }})
{% endif %}{% endfor %}

## Explore more

[All developer projects](https://gcfernando.github.io/gcfernando/projects/) · [Repository on GitHub](https://github.com/gcfernando/datasets) · [XML sitemap](https://gcfernando.github.io/datasets/sitemap.xml)
