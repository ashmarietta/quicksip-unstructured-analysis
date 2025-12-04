# QuickSip Unstructured Data Analysis

## Table of Contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Installation and Requirements](#installation--requirements)
- [Analysis Workflow](#analysis-workflow)
- [Results and Discussion](#results--discussion)
- [Business Suggestions](#business-suggestions)
- [Limitations and Future Work](#limitations--future-work)
- [References](#references)

---

## Project Overview

This project analyzes menu and pricing data from QuickSip, a coffee shop in Pittsburg, Kansas. Using web scraping, I collected unstructured menu data and performed exploratory analysis to provide strategic business suggestions.

---

## Data Source

- **Website Scraped:** https://quicksip.co/menu
- **Date Scraped:** December 1, 2025

All data was extracted using publicly available links and the requests library in Python.

---

## Installation and Requirements

To run the analysis, install the following:

```bash
# Clone the repository
git clone https://github.com/ashmarietta/quicksip-unstructured-analysis.git
cd quicksip-unstructured-analysis

# Install dependencies
pip install -r requirements.txt
```

Requirements include:
- pandas
- requests
- json
- matplotlib

---

## Analysis Workflow

Below is an excerpt of the code used to scrape menu data:

```python
import requests

url = "https://ws-api.toasttab.com/do-federated-gateway/v1/graphql"

headers = {
    "content-type": "application/json",
    "apollographql-client-name": "sites-web-client",
    "apollographql-client-version": "2717",
    "origin": "https://quicksip.co",
    "referer": "https://quicksip.co/",
    "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.1 Safari/605.1.15",
    "toast-graphql-operation": "PaginatedMenuItems,PaginatedMenuItems,PaginatedMenuItemsWithPopularItems,Restaurant,loyaltyFeatures",
    "toast-persistent-query-hash": "525542dec492a54f5b7112b1fbb8d71b1c1210a8,e429e87160545347ef3608bfcd681a72dbff49df,e429e87160545347ef3608bfcd681a72dbff49df,884252f38431e8a38fe86e6e0af7dfdd0c5f2dca,96a3da4f2fe8858e7fe5810b963e78db6e814b13",
    "toast-session-id": "192v0pj1rBoDZit2j9ARiSiLvfLbluh7LEY9wQPdvQ2"
}

cookies = {"toast-session-id": "192v0pj1rBoDZit2j9ARiSiLvfLbluh7LEY9wQPdvQ2"}
response = requests.post(url, json=payload, headers=headers, cookies=cookies)
```

This script defines the GraphQL API URL and builds a header dictionary that will be sent with the payload later in the GET request.

---

## Results and Discussion

- **Menu Size Comparison:** QuickSip offers mostly specialty coffee drinks, including holiday beverages, followed by food items.  
- **Average Pricing:** The mean price of seasonal beverages is the highest, which possibly indicates the business' perceived highest demand.

Discussion:
The data suggests QuickSip's pricing strategy is oriented towards high-end specialty beverages. The coffee shop might be missing opportunities by not focusing on menu items that competitors do not offer, such as food items like pizzas or breakfast sandwiches. It could also potentially bring in more revenue by moving locations to the other side of town where they would have a monopoly on the coffee market.

---

## Business Suggestions

Based on the analysis:

- **Expand Non-Coffee Offerings:** There may be a higher local demand for food items and smoothies.
- **Location Adjustment:** The coffee shop could consider moving to the south side of town to target the college-aged market and move further from competitors.

---

## Limitations and Future Work

- **Data Limitations:** Data is current as of early December 2025, but menu offerings can change rapidly.
- **Data Gaps:** I was not able to analyze customer reviews due to lack of data.
- **Future Work:** I would analyze the scraped data with customer surveys or sales data.

---

## References

- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [QuickSip Menu](https://quicksip.co)
