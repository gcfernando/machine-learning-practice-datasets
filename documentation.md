---
layout: default
title: "Machine Learning Practice Datasets — Documentation and Guides"
description: "CSV datasets for learning classification, regression, sentiment analysis, time-series forecasting and data cleaning."
permalink: /documentation/
---

Browse the published guides, examples and reference pages for **Machine Learning Practice Datasets**. Each guide has a readable web page; the Markdown sources remain available on GitHub.

## 🔎 Schema and quality reference

Use the [README](readme.md) for dataset selection and pandas examples. This reference records the exact columns and empty-cell counts in the committed CSV files; suggested modeling targets are exercises, not an assertion that the tables are representative or well-labeled.

Empty-cell counts below include empty or whitespace-only field values, excluding headers. They do not count every possible missing-value marker or assess duplicate rows, outliers, validity or provenance.

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
<tr><td><a href="{{ guide.path | replace: '/index.html', '/' | absolute_url }}">{% if guide.path == '/Linux_Commands/index.html' %}Linux Command Reference{% elsif guide.path contains 'ai_coding_plugins_beginners_guide' %}AI Coding Add-ons: Beginner’s Guide{% else %}{{ guide.name | escape }} — {{ guide.path | escape }}{% endif %}</a></td><td><a href="https://github.com/{{ site.repository }}/blob/main{{ guide.path | uri_escape }}">View HTML source</a></td></tr>
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
