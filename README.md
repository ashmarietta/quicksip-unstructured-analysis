# ReadMe


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

------------------------------------------------------------------------

## Project Overview

This project analyzes menu and pricing data from QuickSip, a coffee shop
in Pittsburg, Kansas. Using web scraping, I collected unstructured menu
data and performed exploratory analysis to provide strategic business
suggestions.

------------------------------------------------------------------------

## Data Source

- **Website Scraped:** https://quicksip.co/menu
- **Date Scraped:** December 1, 2025

All data was extracted using publicly available links and the requests
library in Python.

------------------------------------------------------------------------

## Installation and Requirements

To run the analysis, install the following:

``` bash
# Clone the repository
git clone https://github.com/ashmarietta/quicksip-unstructured-analysis.git
cd quicksip-unstructured-analysis

# Install dependencies
pip install -r requirements.txt
```

Requirements include: - pandas - requests - json - matplotlib

------------------------------------------------------------------------

## Analysis Workflow

Below is an excerpt of the code used to analyze menu data:

``` python
import json
with open('menu.json', 'r') as f:
        data = json.load(f)
data = json.loads(data)

menu_items1 = data[1].get('data', {}).get('paginatedMenuItems', {}).get('items') or []
menu_items2 = data[2].get('data', {}).get('paginatedMenuItems', {}).get('items') or []

all_items = menu_items1 + menu_items2

for item in all_items:
    name = item['name']
    price = item.get('priceMoney', {}).get('amount')
    print(name, price)
```

## BREAK DOWN THE DATASET

``` python
# shows most basic keys
data[4].get('data').keys()
```

    dict_keys(['__typename', 'paginatedMenuItems', 'popularItems'])

``` python
# shows dictionary keys
data[4].get('data').get('paginatedMenuItems').get("menus")[0].get('groups')[0].keys()
```

    dict_keys(['__typename', 'description', 'guid', 'items', 'name'])

``` python
# returns the whole menu in a dictionary format
data[4].get('data').get('paginatedMenuItems').get("menus")
```

    [{'__typename': 'Menu',
      'groups': [{'__typename': 'MenuGroup',
        'description': '',
        'guid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '6e7dc402-c7a9-45d4-9888-1536b7f95983',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713920303',
          'name': 'Frozen Hot Chocolate',
          'outOfStock': False,
          'prices': [3.75, 6.25, 7.25, 9.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'c4d00e0b-6e19-4c2c-a456-5dbf6bee5018',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000000787599445',
          'name': 'Hot Chocolate',
          'outOfStock': False,
          'prices': [2.5, 4, 4.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Hot Chocolate with Espresso. ',
          'guid': 'f2044363-cc00-42bc-b740-b72f03c34f1d',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000001649972645',
          'name': "Hot Choc'o'latte",
          'outOfStock': False,
          'prices': [6.25, 6.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '7e7fcb91-3494-4c9b-8876-ad2594f5f205',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713458661',
          'name': 'Caramel Cookie Butter Latte',
          'outOfStock': False,
          'prices': [6.25, 7, 6.25, 7, 8, 7.25, 8, 9],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'bee20d9b-53db-4920-9852-05e410f4184e',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713835153',
          'name': 'Maple English Toffee Latte',
          'outOfStock': False,
          'prices': [6, 6.5, 6, 6.5, 7.5, 7, 7.5, 8.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'df1f8455-22a5-4f93-9646-960213e7f72a',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713458662',
          'name': 'Gingerbread Latte',
          'outOfStock': False,
          'prices': [6, 6.5, 6, 6.5, 7.5, 7, 7.5, 8.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '4208515f-035a-4023-82f3-22d9b9386ca3',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713806910',
          'name': 'Hazelnut Fudge Latte',
          'outOfStock': False,
          'prices': [5.5, 6.25, 5.5, 6.25, 7.25, 6.5, 7.25, 8.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '730989af-9a4e-4739-8257-f38262b44d4f',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713806911',
          'name': 'Peppermint Mocha',
          'outOfStock': False,
          'prices': [5.5, 6.25, 5.5, 6.25, 7.25, 6.5, 7.25, 8.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'ba318c99-b8a6-4c09-b179-8160378c3f90',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713717569',
          'name': 'Holiday Chai',
          'outOfStock': False,
          'prices': [6.25, 7, 6.25, 7, 8, 7.25, 8, 9],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '6c19ecdf-5069-4051-9921-7c47f90ac8fe',
          'imageUrls': None,
          'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
          'itemTags': [],
          'masterId': '1400000002713451838',
          'name': "Santa's Punch",
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Holiday Drinks'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Pumpkin Sauce, Espresso, and Whole Milk. ',
          'guid': '09fdd043-110c-41e4-9f50-3e631f012d6a',
          'imageUrls': None,
          'itemGroupGuid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
          'itemTags': [],
          'masterId': '1400000001613454137',
          'name': 'Pumpkin Spice Latte',
          'outOfStock': False,
          'prices': [6, 6, 6.5, 7.95, 7, 7.5, 8.95, 6.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Toasted Marshmallow, Chocolate, Honey, Espresso, Whole Milk, and Cold Foam. ',
          'guid': '40440f67-3c4a-4e81-94df-50c1881dbec0',
          'imageUrls': None,
          'itemGroupGuid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
          'itemTags': [],
          'masterId': '1400000001613877299',
          'name': "S'mores Latte",
          'outOfStock': False,
          'prices': [6.25, 6.25, 7, 8.95, 7.25, 8, 9.95, 7],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Pumpkin Sauce, Cold Brew, and Pumpkin Cold Foam.',
          'guid': '71f3cb35-1154-4f90-972a-1ec40b821ece',
          'imageUrls': None,
          'itemGroupGuid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
          'itemTags': [],
          'masterId': '1400000001651829308',
          'name': 'Pumpkin Foam Brew',
          'outOfStock': False,
          'prices': [5.5, 5.75, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Pumpkin Sauce, Chai, and Whole Milk. ',
          'guid': '758ee6c2-ad9f-4bfb-83f0-c45f33f3b21a',
          'imageUrls': None,
          'itemGroupGuid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
          'itemTags': [],
          'masterId': '1400000001651514944',
          'name': 'Pumpkin Chai',
          'outOfStock': False,
          'prices': [6, 6, 6.5, 7.95, 6.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Hot Chocolate with Espresso. ',
          'guid': 'f2044363-cc00-42bc-b740-b72f03c34f1d',
          'imageUrls': None,
          'itemGroupGuid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
          'itemTags': [],
          'masterId': '1400000001649972645',
          'name': "Hot Choc'o'latte",
          'outOfStock': False,
          'prices': [6.25, 6.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Pumpkin Sauce, Pumpkin Spice, and Half & Half, blended. ',
          'guid': '93cc48b1-6987-49ce-aa93-1777d834ea10',
          'imageUrls': None,
          'itemGroupGuid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
          'itemTags': [],
          'masterId': '1400000001651829319',
          'name': 'Pumpkin Frappe',
          'outOfStock': False,
          'prices': [3.75, 6.25, 7.25, 9.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Toasted Marshmallow, Chocolate, Honey, and Half & Half, blended. ',
          'guid': 'e576d7c8-a5ae-4440-9dd3-d277c7b1baf0',
          'imageUrls': None,
          'itemGroupGuid': 'eecd6c3d-0d73-4fa1-9317-0bfd1f7b9a9d',
          'itemTags': [],
          'masterId': '1400000001649972646',
          'name': "S'mores Frappe",
          'outOfStock': False,
          'prices': [3.75, 6.25, 7.25, 9.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Fall Drinks'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Cane Sugar, Espresso, and Half & Half. ',
          'guid': 'b5c8c606-1e70-4134-9a42-a92fb317b54a',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624230',
          'name': 'Coal Miner',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 6.5, 7.25, 8.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Honey, Vanilla, Cinnamon, Espresso, and Whole Milk. ',
          'guid': '8ef51e7b-0a08-4dca-a2e2-dad29a222df8',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624232',
          'name': 'Quick Sip Delight',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'White Chocolate, Irish Cream, Espresso, and Half & Half. ',
          'guid': 'e0447a27-09e9-4550-8eef-cc3467f2e318',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624234',
          'name': 'Sipster',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Chocolate, Espresso, and Whole Milk. ',
          'guid': '1b036180-29e3-4736-944f-093a043ae464',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624236',
          'name': 'Mocha',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'White Chocolate, Chocolate, Espresso, and Whole Milk.',
          'guid': '69b59f61-c19f-4451-a6c9-9293e7006aed',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624238',
          'name': 'Tuxedo',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Cinnamon Bun, White Chocolate, Espresso, and Whole Milk. ',
          'guid': 'cbf7cff6-01cb-460c-b943-2a56aa422c2c',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624240',
          'name': 'Cinnamon Roll',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Caramel Sauce, Vanilla, Espresso, and Half & Half. ',
          'guid': '8805f33a-dfbc-48df-acc0-ed5572f36111',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624242',
          'name': 'Creamy Caramel',
          'outOfStock': False,
          'prices': [6, 6, 6.5, 7.25, 6, 6.5, 7.25, 6.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Irish Cream, Espresso, and Whole Milk. ',
          'guid': '1907c61c-1ab9-41f5-b411-d4fb1354f88e',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624244',
          'name': 'Irish Latte',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Lavender, Honey, Espresso, and Whole Milk. ',
          'guid': 'd5009990-766f-49e1-b9b0-146fd7542647',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624246',
          'name': 'Lauv & Honey',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Choose your flavors, espresso shots, and milk!',
          'guid': '259f2285-0c20-4fce-b7fe-9af5a2529666',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787624248',
          'name': 'Latte',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Choose your flavors, milk, and topped with espresso shots.',
          'guid': 'e3a1d447-6aaa-40c5-87e5-88e6e0993dc4',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787625000',
          'name': 'Macchiato',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Chai, Espresso, and Whole Milk. ',
          'guid': '436005b9-3039-45f5-9b7e-1a0a5dc8c515',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787625002',
          'name': 'Dirty Chai',
          'outOfStock': False,
          'prices': [5.5, 5.5, 6.25, 7.25, 5.5, 6.25, 7.25, 6.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Espresso and Water, over ice.',
          'guid': '279f3e96-45db-47ee-8e01-9f136c3177d2',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787625004',
          'name': 'Iced Americano',
          'outOfStock': False,
          'prices': [3.5, 3.99, 4.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '79ea79af-c30b-4d52-ac65-019bd74a0a80',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787599423',
          'name': 'Hot Cappuccino',
          'outOfStock': False,
          'prices': [5.5, 5.75],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Espresso and Hot Water. ',
          'guid': '114d4d20-8f36-4ebb-aa89-7285ef68e226',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787599425',
          'name': 'Hot Americano',
          'outOfStock': False,
          'prices': [3.5, 3.75],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '31aa4269-e08b-4e4e-b718-f170b171e00f',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787599427',
          'name': 'Hot Drip',
          'outOfStock': False,
          'prices': [1.59, 1.79],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '835e5b1f-325f-41eb-bf54-c56717648dbd',
          'imageUrls': None,
          'itemGroupGuid': 'd40c06c4-8d2a-4185-b41d-1b25a68f02a2',
          'itemTags': [],
          'masterId': '1400000000787599429',
          'name': '3 Shots',
          'outOfStock': False,
          'prices': [2.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Coffee'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': 'ae9c181a-6624-4858-ba49-bbfa51cd72c1',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'a1a0f3fa-17ee-406a-ab66-3d5ad048daea',
          'imageUrls': None,
          'itemGroupGuid': 'ae9c181a-6624-4858-ba49-bbfa51cd72c1',
          'itemTags': [],
          'masterId': '1400000000787655275',
          'name': 'Cold Brew',
          'outOfStock': False,
          'prices': [4, 4.5, 5.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Caramel, Cinnamon Bun, and Cold Brew, topped with Half & Half.',
          'guid': 'abe37a14-db61-4bdd-8fbb-f7bd07f387c3',
          'imageUrls': None,
          'itemGroupGuid': 'ae9c181a-6624-4858-ba49-bbfa51cd72c1',
          'itemTags': [],
          'masterId': '1400000000787655277',
          'name': 'Caramel Cinnamon Brew',
          'outOfStock': False,
          'prices': [4.5, 4.99, 5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Caramel, Chocolate, and Cold Brew, topped with Half & Half.',
          'guid': 'cbf99965-2426-4198-93e4-f373311a9768',
          'imageUrls': None,
          'itemGroupGuid': 'ae9c181a-6624-4858-ba49-bbfa51cd72c1',
          'itemTags': [],
          'masterId': '1400000000787655279',
          'name': 'Twix Brew',
          'outOfStock': False,
          'prices': [4.5, 4.99, 5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Hazelnut, Chocolate, and Cold Brew, topped with Half & Half.',
          'guid': 'ac270d00-1e48-4483-9f0f-b4ac50b7321f',
          'imageUrls': None,
          'itemGroupGuid': 'ae9c181a-6624-4858-ba49-bbfa51cd72c1',
          'itemTags': [],
          'masterId': '1400000000787655281',
          'name': 'Hazelnut Snickers Brew',
          'outOfStock': False,
          'prices': [4.5, 4.99, 5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'English Toffee, Chocolate, and Cold Brew, topped with Half & Half.',
          'guid': 'd50066be-3824-4fe4-a0f8-a48fb2442be7',
          'imageUrls': None,
          'itemGroupGuid': 'ae9c181a-6624-4858-ba49-bbfa51cd72c1',
          'itemTags': [],
          'masterId': '1400000000787655285',
          'name': 'Heath Bar Brew',
          'outOfStock': False,
          'prices': [4.5, 4.99, 5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Cold Brew'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Chai and Whole Milk. ',
          'guid': '7c9961fb-8c7f-4bd7-b9c0-cd64229eadbf',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787660000',
          'name': 'Chai Tea Latte',
          'outOfStock': False,
          'prices': [5.5, 5.5, 5.99, 6.99, 5.5, 5.99, 6.99, 5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Vanilla, Vanilla Bean, and Half & Half, blended. ',
          'guid': 'caacf60b-f852-4fcb-9ed2-60ed5ad67c4d',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787660002',
          'name': 'Vanilla Bean Frappe',
          'outOfStock': False,
          'prices': [2.75, 5.99, 6.99, 8.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '728e1809-3816-4ab4-be61-6f1194914809',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787660004',
          'name': 'Iced Matcha',
          'outOfStock': False,
          'prices': [5.5, 5.99, 6.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Honey, Vanilla, Matcha Green Tea, and Whole Milk. ',
          'guid': 'a79f1583-ce47-4a17-9c75-a391222ff236',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787659498',
          'name': 'The Jungle',
          'outOfStock': False,
          'prices': [5.5, 5.5, 5.99, 6.99, 5.5, 5.99, 6.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'bfac5ace-dcbb-40fa-a427-f64e1ad6a851',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787599437',
          'name': 'Hot The Jungle',
          'outOfStock': False,
          'prices': [5.5, 5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'e94ff0eb-bcf8-4a61-acdd-83bb5260e9ee',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787599439',
          'name': 'Hot Chai Tea Latte',
          'outOfStock': False,
          'prices': [5.5, 5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'd10afd52-db30-4d08-919d-6c9b50c3ba01',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787599441',
          'name': 'Chocolate Milk',
          'outOfStock': False,
          'prices': [],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'b03b7ec4-ed0c-4a4a-9078-c8eefede277b',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787599443',
          'name': 'Louisburg Cider',
          'outOfStock': False,
          'prices': [4.5, 3, 4.5, 5.25, 6.5, 5.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'c4d00e0b-6e19-4c2c-a456-5dbf6bee5018',
          'imageUrls': None,
          'itemGroupGuid': 'ea481cae-c60f-48ed-b053-94b173e8ef83',
          'itemTags': [],
          'masterId': '1400000000787599445',
          'name': 'Hot Chocolate',
          'outOfStock': False,
          'prices': [2.5, 4, 4.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Non Coffee'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': '37490f25-8490-41af-b639-ab21828b9881',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Orange Energy, Cherry, and Sprite. ',
          'guid': '20d60e74-18ba-4a8b-9251-a421e9c86a51',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667751',
          'name': 'Mimosa',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Citrus energy, lemonade powder, and peach. Made with water and sugar-free. ',
          'guid': '3d010dc1-8c7e-4c0f-866b-5687f7562f77',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667753',
          'name': 'Citrus Peach',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Citrus energy, lemonade powder, and cherry. Made with water and sugar-free. ',
          'guid': 'd7dcb875-acc9-4ec8-91a4-d3ba0cdc09ed',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667755',
          'name': 'Wild Cherry',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Berry energy and grape. Made with water and sugar-free. ',
          'guid': '36f0bdf9-058e-41d6-adc0-222ee058a545',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667757',
          'name': 'Purple Punch',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Citrus energy, raspberry lemonade powder, and grape. Made with water and sugar-free. ',
          'guid': 'e17d458f-a081-4535-a587-c99a6c52e1ec',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667759',
          'name': 'Sangria',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Strawberry energy, cherry, and coconut. Made with water and sugar-free. ',
          'guid': '05d14875-9fea-4085-a583-b6f502577267',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667761',
          'name': "Tiger's Blood",
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Citrus energy, cherry, and lime powder. Made with sparkling water and sugar-free. ',
          'guid': '667bade8-aad0-4694-ade6-0e7bd9e5ead3',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667763',
          'name': 'Sparkling Cherry Lime',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Citrus energy, peach, and lime powder. Made with sparkling water and sugar-free. ',
          'guid': 'd9432752-f7c1-4853-a231-dc82002f463e',
          'imageUrls': None,
          'itemGroupGuid': '37490f25-8490-41af-b639-ab21828b9881',
          'itemTags': [],
          'masterId': '1400000000787667765',
          'name': 'Sparkling Tropical Punch',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Energy Teas'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': 'adce55a5-f952-433f-9cba-1bbc55dee74b',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Blueberry, Raspberry, Monster, and Cream. ',
          'guid': '1ddab647-beb7-492d-b123-152a47a9d123',
          'imageUrls': None,
          'itemGroupGuid': 'adce55a5-f952-433f-9cba-1bbc55dee74b',
          'itemTags': [],
          'masterId': '1400000000787669539',
          'name': 'Dragon',
          'outOfStock': False,
          'prices': [4.25, 4.5, 5.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Blue Raspberry, Coconut, Monster, and Cream. ',
          'guid': '2c76b590-108d-4b29-9893-14dd661d9ea1',
          'imageUrls': None,
          'itemGroupGuid': 'adce55a5-f952-433f-9cba-1bbc55dee74b',
          'itemTags': [],
          'masterId': '1400000000787669541',
          'name': 'Panther',
          'outOfStock': False,
          'prices': [4.25, 4.5, 5.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Blackberry, Lemon, Monster, and Cream. ',
          'guid': '7fc03b4a-6fed-4478-8013-2650005c1537',
          'imageUrls': None,
          'itemGroupGuid': 'adce55a5-f952-433f-9cba-1bbc55dee74b',
          'itemTags': [],
          'masterId': '1400000000787669543',
          'name': 'Raider',
          'outOfStock': False,
          'prices': [4.25, 4.5, 5.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Strawberry, Banana, Monster, and Cream. ',
          'guid': '9fb3a769-255a-4efc-a02d-eec556129f79',
          'imageUrls': None,
          'itemGroupGuid': 'adce55a5-f952-433f-9cba-1bbc55dee74b',
          'itemTags': [],
          'masterId': '1400000000787669545',
          'name': 'Splitface',
          'outOfStock': False,
          'prices': [4.25, 4.5, 5.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Choose your flavors, Monster, and Cream!',
          'guid': '32e012c2-9f88-4163-88d9-1826a90653a7',
          'imageUrls': None,
          'itemGroupGuid': 'adce55a5-f952-433f-9cba-1bbc55dee74b',
          'itemTags': [],
          'masterId': '1400000000787669547',
          'name': 'Create Your Own Italian Soda',
          'outOfStock': False,
          'prices': [4.25, 4.5, 5.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Italian Sodas'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Coconut, Lime Juice, Diet Coke, and Cream.',
          'guid': '36ca6ac8-92a0-4639-9107-28428ddf4207',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673192',
          'name': 'The Classic',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Butterscotch, Root Beer, and Cream.',
          'guid': '2fb6cddd-d143-47d2-9553-593faf046e85',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673194',
          'name': 'Butterbeer',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Orange Fanta and Cream.',
          'guid': 'c0976d56-ca57-46d9-a689-a30099fc848d',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673196',
          'name': 'Dreamsicle',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Strawberry, Sprite, and Cream. ',
          'guid': '195e491e-cf07-492b-87b0-59708d88590c',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673198',
          'name': 'Strawberry Daiquiri',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Strawberry, Mango, Lemon, Coconut, Sprite, and Cream. ',
          'guid': 'c606ef83-d916-48e6-8100-a0a7a8fe7783',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673450',
          'name': 'Strawberry Twist',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'English Toffee, Dr. Pepper, and Cream. ',
          'guid': '7f3c9f96-f1ac-4e42-be0c-9c77107998a4',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673452',
          'name': 'The Mud',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Cherry, Vanilla, Coke, and Cream. ',
          'guid': '23f387e4-d955-4e74-91b2-14ef4ed122d5',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673454',
          'name': 'Cherry Vanilla',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Blackberry, Coconut, Dr. Pepper, and Cream. ',
          'guid': '4dda025e-3346-484d-a879-0ed74fbd3211',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673456',
          'name': 'The Bliss',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Coconut, Sprite, and Cream. ',
          'guid': '6144228a-f994-405f-8bb0-df60524ae7d4',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673458',
          'name': 'Malibu Knight',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Choose your flavors, soda, and cream!',
          'guid': 'dd749531-a353-452f-9352-47de5aa77ab3',
          'imageUrls': None,
          'itemGroupGuid': '74635ed2-945f-491f-b506-b70b07bbd4fe',
          'itemTags': [],
          'masterId': '1400000000787673460',
          'name': 'Create Your Own Dirty Soda',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Dirty Sodas'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': '759e8d9d-ad14-4969-b1f8-52d43247cf4c',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Acai berry Liquid IV and raspberry lemonade powder, made with water. ',
          'guid': 'def878a9-1270-45cf-9ed7-12d02995a159',
          'imageUrls': None,
          'itemGroupGuid': '759e8d9d-ad14-4969-b1f8-52d43247cf4c',
          'itemTags': [],
          'masterId': '1400000000787675342',
          'name': 'Acai Berry',
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Blue Gatorade powder and coconut, made with water. ',
          'guid': 'ca6f34d9-2363-4787-83a2-5a920192106e',
          'imageUrls': None,
          'itemGroupGuid': '759e8d9d-ad14-4969-b1f8-52d43247cf4c',
          'itemTags': [],
          'masterId': '1400000000787675344',
          'name': 'Blue Hawaiian',
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Watermelon Liquid IV, lemonade powder, and cherry, made with water. ',
          'guid': '26d2714a-0814-4bd5-aa74-4dc0a8c556b4',
          'imageUrls': None,
          'itemGroupGuid': '759e8d9d-ad14-4969-b1f8-52d43247cf4c',
          'itemTags': [],
          'masterId': '1400000000787675346',
          'name': 'Jolly Rancher',
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Strawberry lemonade Liquid IV lemonade powder, and strawberry, made with water. ',
          'guid': '5d8b587f-9f39-4b88-8e8a-e264cfc18e34',
          'imageUrls': None,
          'itemGroupGuid': '759e8d9d-ad14-4969-b1f8-52d43247cf4c',
          'itemTags': [],
          'masterId': '1400000000787675348',
          'name': 'Strawberry Lemonade',
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Lemon Lime Gatorade powder and raspberry lemonade powder, made with water. ',
          'guid': '6e71111c-8718-43cd-8970-d4b8e387df44',
          'imageUrls': None,
          'itemGroupGuid': '759e8d9d-ad14-4969-b1f8-52d43247cf4c',
          'itemTags': [],
          'masterId': '1400000000787676200',
          'name': 'Sunset Surge',
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Tropical punch Liquid IV, coconut, and peach made with water. ',
          'guid': 'bb0ccb33-a10f-4354-94c3-d48c0cd6ff7c',
          'imageUrls': None,
          'itemGroupGuid': '759e8d9d-ad14-4969-b1f8-52d43247cf4c',
          'itemTags': [],
          'masterId': '1400000000787676202',
          'name': 'Tropical Tide',
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Hydraters'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': 'cbabe420-6e35-4f07-b01e-e4ba7886d71d',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Peach, Mango, and Monster. ',
          'guid': 'ce64891a-0863-4f11-932a-de1825edca7b',
          'imageUrls': None,
          'itemGroupGuid': 'cbabe420-6e35-4f07-b01e-e4ba7886d71d',
          'itemTags': [],
          'masterId': '1400000000787680236',
          'name': "Gold'Rilla",
          'outOfStock': False,
          'prices': [4.5, 5.5, 6.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Cherry, Lime, and Sprite. ',
          'guid': 'fda96303-b729-462d-af62-68bbf86f7e45',
          'imageUrls': None,
          'itemGroupGuid': 'cbabe420-6e35-4f07-b01e-e4ba7886d71d',
          'itemTags': [],
          'masterId': '1400000000787680238',
          'name': "Sippin' Limeade",
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Strawberry, Mango, and Mtn. Dew. ',
          'guid': '6ba41077-2164-48f3-832e-7d670989e3f2',
          'imageUrls': None,
          'itemGroupGuid': 'cbabe420-6e35-4f07-b01e-e4ba7886d71d',
          'itemTags': [],
          'masterId': '1400000000787680240',
          'name': 'Sunrise',
          'outOfStock': False,
          'prices': [3, 3.25, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Mojito Mint, Lime Juice, and Sprite. ',
          'guid': '62b05c31-7f2b-4622-9a53-dda5a76f84b4',
          'imageUrls': None,
          'itemGroupGuid': 'cbabe420-6e35-4f07-b01e-e4ba7886d71d',
          'itemTags': [],
          'masterId': '1400000000787680242',
          'name': 'Mojito',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Mojito Mint, Lavender, Lime Juice, and Sprite. ',
          'guid': '9ebda7eb-7c75-4d9a-81d4-bfedc3c43441',
          'imageUrls': None,
          'itemGroupGuid': 'cbabe420-6e35-4f07-b01e-e4ba7886d71d',
          'itemTags': [],
          'masterId': '1400000000787680244',
          'name': 'Lavender Mojito',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Mojito Mint, Watermelon, Lime Juice, and Sprite. ',
          'guid': '9de295e2-f0bf-43d8-85b4-0d82c0663495',
          'imageUrls': None,
          'itemGroupGuid': 'cbabe420-6e35-4f07-b01e-e4ba7886d71d',
          'itemTags': [],
          'masterId': '1400000000787680246',
          'name': 'Watermelon Mojito',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Specialty Soft Drinks'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': '49c8ee4b-7c91-4edc-87bf-fe1f7c90a703',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '310b86a1-59d4-40bb-96ae-1ee6fe7f1446',
          'imageUrls': None,
          'itemGroupGuid': '49c8ee4b-7c91-4edc-87bf-fe1f7c90a703',
          'itemTags': [],
          'masterId': '1400000000787682927',
          'name': 'Fountain Drinks',
          'outOfStock': False,
          'prices': [0.89, 1.59, 1.69, 1.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'b8847073-9377-4197-beda-2bfa7626489b',
          'imageUrls': None,
          'itemGroupGuid': '49c8ee4b-7c91-4edc-87bf-fe1f7c90a703',
          'itemTags': [],
          'masterId': '1400000000787682929',
          'name': 'Iced Tea',
          'outOfStock': False,
          'prices': [0.89, 1.59, 1.69, 1.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '590e9f8a-ea51-4ca8-b974-c6d9cac63176',
          'imageUrls': None,
          'itemGroupGuid': '49c8ee4b-7c91-4edc-87bf-fe1f7c90a703',
          'itemTags': [],
          'masterId': '1400000000787682931',
          'name': 'Snow Cones',
          'outOfStock': False,
          'prices': [1.79, 3],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'b370ebeb-093a-4089-939a-fa51da42576c',
          'imageUrls': None,
          'itemGroupGuid': '49c8ee4b-7c91-4edc-87bf-fe1f7c90a703',
          'itemTags': [],
          'masterId': '1400000000787682933',
          'name': 'Non-Alcoholic Slush',
          'outOfStock': False,
          'prices': [1.75, 3, 3.5, 4.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Fountain Drinks & More'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': 'dc89ecee-17bb-4709-87b0-497bb312d558',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'ef54e4d8-4d7c-4787-9556-3f99169a033b',
          'imageUrls': None,
          'itemGroupGuid': 'dc89ecee-17bb-4709-87b0-497bb312d558',
          'itemTags': [],
          'masterId': '1400000000787687678',
          'name': 'Strawberry Banana',
          'outOfStock': False,
          'prices': [3.99, 4.99, 5.99, 7.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '62b968ea-a772-4076-80a9-2088df3f317a',
          'imageUrls': None,
          'itemGroupGuid': 'dc89ecee-17bb-4709-87b0-497bb312d558',
          'itemTags': [],
          'masterId': '1400000000787687680',
          'name': 'Mixed Berry',
          'outOfStock': False,
          'prices': [3.99, 4.99, 5.99, 7.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'fabde06a-9c2c-43c5-ad0e-bf0ff91d916b',
          'imageUrls': None,
          'itemGroupGuid': 'dc89ecee-17bb-4709-87b0-497bb312d558',
          'itemTags': [],
          'masterId': '1400000000787687682',
          'name': 'Mango',
          'outOfStock': False,
          'prices': [3.99, 4.99, 5.99, 7.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '369c54a2-f47a-46bd-99b8-9ac0ef0bd6e9',
          'imageUrls': None,
          'itemGroupGuid': 'dc89ecee-17bb-4709-87b0-497bb312d558',
          'itemTags': [],
          'masterId': '1400000000787687684',
          'name': 'Peach',
          'outOfStock': False,
          'prices': [3.99, 4.99, 5.99, 7.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '867953a9-b73f-47f8-bf91-95546850295d',
          'imageUrls': None,
          'itemGroupGuid': 'dc89ecee-17bb-4709-87b0-497bb312d558',
          'itemTags': [],
          'masterId': '1400000000787687686',
          'name': 'Pina Colada',
          'outOfStock': False,
          'prices': [3.99, 4.99, 5.99, 7.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Smoothies'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'a0ebc629-10f7-4e09-b432-26a0e33eca81',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787599686',
          'name': 'Bomb Pop',
          'outOfStock': False,
          'prices': [2, 3.25, 3.5, 4.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'fc170eb8-bc08-46f8-81af-e7ae04177bf9',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787599688',
          'name': 'Banana Bread Latte',
          'outOfStock': False,
          'prices': [5.99, 5.99, 6.99, 8.99, 6.99, 7.99, 9.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '2601e7d9-aead-417f-b966-595affaed9b2',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787599691',
          'name': 'Patriotic Punch',
          'outOfStock': False,
          'prices': [3.5, 3.75, 4.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '47cc614f-8f4b-4f67-a135-e633c74a930a',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787599693',
          'name': 'Freedom Fizz',
          'outOfStock': False,
          'prices': [4.25, 4.5, 5.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '0368ead7-974d-496a-a145-2ebbaffa2919',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787599695',
          'name': 'Frozen Firecracker',
          'outOfStock': False,
          'prices': [1.75, 3, 3.5, 4.25],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '7b04f788-218b-48cb-b5a0-af06ee185cae',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787599697',
          'name': 'Boozy Firecracker',
          'outOfStock': False,
          'prices': [6.5, 6.99, 7.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'b2113624-cdf9-4b61-8314-e5c19ac29527',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787697669',
          'name': 'Red, White, & Blue Snow Cone',
          'outOfStock': False,
          'prices': [1.79, 3],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '2f461b5e-4233-436a-b46b-0d39b78f230f',
          'imageUrls': None,
          'itemGroupGuid': '4fe9c09b-a11e-4512-a283-52a5353ae6c2',
          'itemTags': [],
          'masterId': '1400000000787697671',
          'name': 'Strawberries & Cream Frappe',
          'outOfStock': False,
          'prices': [2.75, 5.99, 6.99, 8.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Summer Drinks'},
       {'__typename': 'MenuGroup',
        'description': '',
        'guid': '4eaca444-d740-4308-820c-0884bb5954ad',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '6d33d304-fe61-4201-ad70-69ff8ac6ce7b',
          'imageUrls': None,
          'itemGroupGuid': '4eaca444-d740-4308-820c-0884bb5954ad',
          'itemTags': [],
          'masterId': '1400000000787600001',
          'name': 'Blackberry Vanilla Chai',
          'outOfStock': False,
          'prices': [6, 6, 6.5, 7.95],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '288fce4f-fcb3-4643-a6b8-ab2ac216f19d',
          'imageUrls': None,
          'itemGroupGuid': '4eaca444-d740-4308-820c-0884bb5954ad',
          'itemTags': [],
          'masterId': '1400000000787600005',
          'name': 'Golden Matcha',
          'outOfStock': False,
          'prices': [6, 6, 6.5, 7.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '51259c39-98d6-4dd9-9c6e-1d8833af4d6c',
          'imageUrls': None,
          'itemGroupGuid': '4eaca444-d740-4308-820c-0884bb5954ad',
          'itemTags': [],
          'masterId': '1400000000787600007',
          'name': 'Berry Cheesecake Frappe',
          'outOfStock': False,
          'prices': [2.75, 5.99, 6.99, 8.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '7a2395a5-9a69-46be-9487-2452dc0f6f6d',
          'imageUrls': None,
          'itemGroupGuid': '4eaca444-d740-4308-820c-0884bb5954ad',
          'itemTags': [],
          'masterId': '1400000000787600009',
          'name': 'Berry Punch Energy Tea',
          'outOfStock': False,
          'prices': [3.25, 3.5, 4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Seasonal'}],
      'guid': 'b880ceee-d4db-42a9-bcda-0588543c18aa',
      'name': 'Drink Menu'},
     {'__typename': 'Menu',
      'groups': [{'__typename': 'MenuGroup',
        'description': '',
        'guid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
        'items': [{'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '6a6e5cdc-95c0-4ac5-b0f9-d20aa346f23c',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600019',
          'name': 'Bacon, Egg, & Gouda Sandwich',
          'outOfStock': False,
          'prices': [3.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '777eb8a8-eb2e-4297-8c9b-04dbcc9c1b35',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600021',
          'name': 'Sausage Cheddar Bagel Roll',
          'outOfStock': False,
          'prices': [3.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '955ce3ab-b111-4514-a504-d06aee58c6a3',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600023',
          'name': 'Sausage, Egg, & Cheese Biscuit',
          'outOfStock': False,
          'prices': [3.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '61b4e236-3ca6-47af-b4b6-3af900378284',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600025',
          'name': 'Sausage, Egg, & Cheese Everything Bagel Sandwich',
          'outOfStock': False,
          'prices': [4.59],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'b9a9a50f-1c8d-4df3-98b9-1338d26b6afa',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600027',
          'name': 'Bagels',
          'outOfStock': False,
          'prices': [1.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'f6067836-267d-4a11-aaf5-af17790be819',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600029',
          'name': 'Cinni Mini',
          'outOfStock': False,
          'prices': [2.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': 'fabdd96f-51b0-46bf-8569-cfcea8ccdfd1',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600031',
          'name': 'Small Cheese Pizza',
          'outOfStock': False,
          'prices': [3.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '5f326825-c073-4297-a00a-59aa71face91',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600033',
          'name': 'Large Cheese Pizza',
          'outOfStock': False,
          'prices': [5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '04341b6f-0307-4da3-b786-d4f5b455c7f0',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600035',
          'name': 'Large Pepperoni Pizza',
          'outOfStock': False,
          'prices': [5.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '2 Pizza Sticks',
          'guid': '38cde532-9a82-44bc-b249-f8f68067b388',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600037',
          'name': 'Pizza Sticks',
          'outOfStock': False,
          'prices': [2.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '0d26fedc-a2aa-4498-a125-0cd34fbe75e8',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600039',
          'name': 'Pepperoni & Cheese Bosco Stick',
          'outOfStock': False,
          'prices': [2.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '2 Pretzel Sticks- With cheese or cinnamon & sugar',
          'guid': 'ce72a542-62cc-4720-85b8-f47cf40b4a99',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600041',
          'name': 'Pretzel Sticks',
          'outOfStock': False,
          'prices': [3.5],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '',
          'guid': '2178dda7-1f06-4f4b-a401-58b58cde276b',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600043',
          'name': 'Corn Dog',
          'outOfStock': False,
          'prices': [0.99],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': '3 Chicken Strips',
          'guid': '449a0063-fea6-4d94-9da4-b4a19572e23d',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600045',
          'name': 'Chicken Strips',
          'outOfStock': False,
          'prices': [],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False},
         {'__typename': 'MenuItem',
          'defaultModifiersPrice': 0,
          'description': 'Bavarian Roasted Cinnamon Glazed Nuts',
          'guid': '4b4ef56d-635c-4a88-ab80-b79b484a6707',
          'imageUrls': None,
          'itemGroupGuid': '5adc1ddb-13d2-41b8-9a92-a66f645f5efa',
          'itemTags': [],
          'masterId': '1400000000787600047',
          'name': 'Cinnamon Roasted Nuts',
          'outOfStock': False,
          'prices': [4],
          'timeBasedRules': None,
          'unitOfMeasure': 'NONE',
          'usesFractionalQuantity': False}],
        'name': 'Food'}],
      'guid': 'a549101c-be61-4697-a98e-fb32bcafc938',
      'name': 'Food Menu'},
     {'__typename': 'Menu',
      'groups': [],
      'guid': '06810168-2228-4263-8dd4-606cb54d2313',
      'name': 'Boozy Slush Menu'}]

``` python
# returns group list
data[4].get('data').get('paginatedMenuItems').get("menus")[0].get('groups')[0].get('items')[0]
```

    {'__typename': 'MenuItem',
     'defaultModifiersPrice': 0,
     'description': '',
     'guid': '6e7dc402-c7a9-45d4-9888-1536b7f95983',
     'imageUrls': None,
     'itemGroupGuid': 'd95f32ea-92ec-47d4-a2ea-8c5f0178ef34',
     'itemTags': [],
     'masterId': '1400000002713920303',
     'name': 'Frozen Hot Chocolate',
     'outOfStock': False,
     'prices': [3.75, 6.25, 7.25, 9.25],
     'timeBasedRules': None,
     'unitOfMeasure': 'NONE',
     'usesFractionalQuantity': False}

``` python
# returns name of product
data[4].get('data').get('paginatedMenuItems').get("menus")[0].get('groups')[0].get('items')[0].get('name')
```

    'Frozen Hot Chocolate'

``` python
# returns price
data[4].get('data').get('paginatedMenuItems').get("menus")[0].get('groups')[0].get('items')[0].get('prices')
```

    [3.75, 6.25, 7.25, 9.25]

## EVALUATE BUSINESS FOCUS

How many menu items does each major category have, and what does that
say about the business focus?

``` python
# count number of items in each group
menus = data[4].get('data').get('paginatedMenuItems').get("menus")

group_counts = {}

for menu in menus:
    groups = menu.get('groups', [])
    
    for g in groups:
        group_name = g.get("name", "UNKNOWN GROUP")
        items = g.get("items", [])
        count = len(items)
        group_counts[group_name] = group_counts.get(group_name, 0) + count

group_counts
```

    {'Holiday Drinks': 10,
     'Fall Drinks': 7,
     'Coffee': 17,
     'Cold Brew': 5,
     'Non Coffee': 9,
     'Energy Teas': 8,
     'Italian Sodas': 5,
     'Dirty Sodas': 10,
     'Hydraters': 6,
     'Specialty Soft Drinks': 6,
     'Fountain Drinks & More': 4,
     'Smoothies': 5,
     'Summer Drinks': 8,
     'Seasonal': 4,
     'Food': 15}

``` python
# show menu items in each group
for menu in menus:
    for g in menu.get("groups", []):
        print("\nGROUP:", g.get("name"))
        for item in g.get("items", []):
            print("   •", item.get("name"))
```


    GROUP: Holiday Drinks
       • Frozen Hot Chocolate
       • Hot Chocolate
       • Hot Choc'o'latte
       • Caramel Cookie Butter Latte
       • Maple English Toffee Latte
       • Gingerbread Latte
       • Hazelnut Fudge Latte
       • Peppermint Mocha
       • Holiday Chai
       • Santa's Punch

    GROUP: Fall Drinks
       • Pumpkin Spice Latte
       • S'mores Latte
       • Pumpkin Foam Brew
       • Pumpkin Chai
       • Hot Choc'o'latte
       • Pumpkin Frappe
       • S'mores Frappe

    GROUP: Coffee
       • Coal Miner
       • Quick Sip Delight
       • Sipster
       • Mocha
       • Tuxedo
       • Cinnamon Roll
       • Creamy Caramel
       • Irish Latte
       • Lauv & Honey
       • Latte
       • Macchiato
       • Dirty Chai
       • Iced Americano
       • Hot Cappuccino
       • Hot Americano
       • Hot Drip
       • 3 Shots

    GROUP: Cold Brew
       • Cold Brew
       • Caramel Cinnamon Brew
       • Twix Brew
       • Hazelnut Snickers Brew
       • Heath Bar Brew

    GROUP: Non Coffee
       • Chai Tea Latte
       • Vanilla Bean Frappe
       • Iced Matcha
       • The Jungle
       • Hot The Jungle
       • Hot Chai Tea Latte
       • Chocolate Milk
       • Louisburg Cider
       • Hot Chocolate

    GROUP: Energy Teas
       • Mimosa
       • Citrus Peach
       • Wild Cherry
       • Purple Punch
       • Sangria
       • Tiger's Blood
       • Sparkling Cherry Lime
       • Sparkling Tropical Punch

    GROUP: Italian Sodas
       • Dragon
       • Panther
       • Raider
       • Splitface
       • Create Your Own Italian Soda

    GROUP: Dirty Sodas
       • The Classic
       • Butterbeer
       • Dreamsicle
       • Strawberry Daiquiri
       • Strawberry Twist
       • The Mud
       • Cherry Vanilla
       • The Bliss
       • Malibu Knight
       • Create Your Own Dirty Soda

    GROUP: Hydraters
       • Acai Berry
       • Blue Hawaiian
       • Jolly Rancher
       • Strawberry Lemonade
       • Sunset Surge
       • Tropical Tide

    GROUP: Specialty Soft Drinks
       • Gold'Rilla
       • Sippin' Limeade
       • Sunrise
       • Mojito
       • Lavender Mojito
       • Watermelon Mojito

    GROUP: Fountain Drinks & More
       • Fountain Drinks
       • Iced Tea
       • Snow Cones
       • Non-Alcoholic Slush

    GROUP: Smoothies
       • Strawberry Banana
       • Mixed Berry
       • Mango
       • Peach
       • Pina Colada

    GROUP: Summer Drinks
       • Bomb Pop
       • Banana Bread Latte
       • Patriotic Punch
       • Freedom Fizz
       • Frozen Firecracker
       • Boozy Firecracker
       • Red, White, & Blue Snow Cone
       • Strawberries & Cream Frappe

    GROUP: Seasonal
       • Blackberry Vanilla Chai
       • Golden Matcha
       • Berry Cheesecake Frappe
       • Berry Punch Energy Tea

    GROUP: Food
       • Bacon, Egg, & Gouda Sandwich
       • Sausage Cheddar Bagel Roll
       • Sausage, Egg, & Cheese Biscuit
       • Sausage, Egg, & Cheese Everything Bagel Sandwich
       • Bagels
       • Cinni Mini
       • Small Cheese Pizza
       • Large Cheese Pizza
       • Large Pepperoni Pizza
       • Pizza Sticks
       • Pepperoni & Cheese Bosco Stick
       • Pretzel Sticks
       • Corn Dog
       • Chicken Strips
       • Cinnamon Roasted Nuts

``` python
# count of menu items by group in a dataframe
import pandas as pd
pd.DataFrame(group_counts.items(), columns=["Group", "ItemCount"])
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
&#10;    .dataframe tbody tr th {
        vertical-align: top;
    }
&#10;    .dataframe thead th {
        text-align: right;
    }
</style>

|     | Group                  | ItemCount |
|-----|------------------------|-----------|
| 0   | Holiday Drinks         | 10        |
| 1   | Fall Drinks            | 7         |
| 2   | Coffee                 | 17        |
| 3   | Cold Brew              | 5         |
| 4   | Non Coffee             | 9         |
| 5   | Energy Teas            | 8         |
| 6   | Italian Sodas          | 5         |
| 7   | Dirty Sodas            | 10        |
| 8   | Hydraters              | 6         |
| 9   | Specialty Soft Drinks  | 6         |
| 10  | Fountain Drinks & More | 4         |
| 11  | Smoothies              | 5         |
| 12  | Summer Drinks          | 8         |
| 13  | Seasonal               | 4         |
| 14  | Food                   | 15        |

</div>

Based solely on the count of menu items, it appears that QuickSip
focuses primarily on coffee drinks, which also include a large portion
of the holiday, fall, and summer drinks, and on food items. I find this
interesting because, while Pittsburg is a small town of around 20,000
residents, it has multiple chain coffee shops, including Starbucks,
Scooters, and 7 Brew, and two local coffee shops all on the north side
of town. I often see many cars in the parking lots for the other chain
coffee shops, but QuickSip is rarely busy. While they do advertise being
fast as their business model, I wonder if moving further south near
Pittsburg State University or if altering their menu to focus more on
food items or smoothies would make more financial sense. I selfishly
hope their menu stays the same because I love all of their holiday and
fall drinks, but I also would love to see the business thrive!

## BRING IN AVERAGE PRICE BY GROUP

How do seasonal items (fall/holiday/summer drinks) compare in price to
the regular menu items?

``` python
group_avg_prices = {}

def extract_price_dollars(item):
    prices = item.get("prices", None)
    if prices is None:
        return None
    if isinstance(prices, list):
        if not prices:
            return None
        p = prices[0]
    else:
        p = prices
    if isinstance(p, dict):
        unit = p.get("unitPrice") or p.get("price") or p.get("unit_price")
        if isinstance(unit, dict) and "amount" in unit:
            cents = unit["amount"]
            if isinstance(cents, (int, float)):
                return cents
        if "amount" in p and isinstance(p["amount"], (int, float)):
            return p["amount"]
        return None
    if isinstance(p, (int, float)):
        return float(p)
    return None

for menu in menus:
    for g in menu.get("groups", []):
        group_name = g.get("name", "UNKNOWN GROUP")
        items = g.get("items", [])

        if group_name not in group_avg_prices:
            group_avg_prices[group_name] = {"total_price": 0.0, "count": 0}

        for item in items:
            price = extract_price_dollars(item)
            if price is not None:
                group_avg_prices[group_name]["total_price"] += price
                group_avg_prices[group_name]["count"] += 1

for group, stats in group_avg_prices.items():
    if stats["count"] > 0:
        stats["avg_price"] = round(stats["total_price"] / stats["count"], 2)
    else:
        stats["avg_price"] = None

group_avg_prices
```

    {'Holiday Drinks': {'total_price': 51.25, 'count': 10, 'avg_price': 5.12},
     'Fall Drinks': {'total_price': 37.5, 'count': 7, 'avg_price': 5.36},
     'Coffee': {'total_price': 82.84, 'count': 17, 'avg_price': 4.87},
     'Cold Brew': {'total_price': 22.0, 'count': 5, 'avg_price': 4.4},
     'Non Coffee': {'total_price': 37.25, 'count': 8, 'avg_price': 4.66},
     'Energy Teas': {'total_price': 26.0, 'count': 8, 'avg_price': 3.25},
     'Italian Sodas': {'total_price': 21.25, 'count': 5, 'avg_price': 4.25},
     'Dirty Sodas': {'total_price': 20.0, 'count': 10, 'avg_price': 2.0},
     'Hydraters': {'total_price': 18.0, 'count': 6, 'avg_price': 3.0},
     'Specialty Soft Drinks': {'total_price': 20.25,
      'count': 6,
      'avg_price': 3.38},
     'Fountain Drinks & More': {'total_price': 5.32,
      'count': 4,
      'avg_price': 1.33},
     'Smoothies': {'total_price': 19.950000000000003,
      'count': 5,
      'avg_price': 3.99},
     'Summer Drinks': {'total_price': 28.53, 'count': 8, 'avg_price': 3.57},
     'Seasonal': {'total_price': 18.0, 'count': 4, 'avg_price': 4.5},
     'Food': {'total_price': 51.000000000000014, 'count': 14, 'avg_price': 3.64}}

``` python
import pandas as pd

df_counts = pd.DataFrame(list(group_counts.items()), columns=["Group", "ItemCount"])

df_prices = pd.DataFrame(
    [{"Group": g, "AvgPrice": v["avg_price"]} for g, v in group_avg_prices.items()]
)

df_final = df_counts.merge(df_prices, on="Group", how="inner")

df_final
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }
&#10;    .dataframe tbody tr th {
        vertical-align: top;
    }
&#10;    .dataframe thead th {
        text-align: right;
    }
</style>

|     | Group                  | ItemCount | AvgPrice |
|-----|------------------------|-----------|----------|
| 0   | Holiday Drinks         | 10        | 5.12     |
| 1   | Fall Drinks            | 7         | 5.36     |
| 2   | Coffee                 | 17        | 4.87     |
| 3   | Cold Brew              | 5         | 4.40     |
| 4   | Non Coffee             | 9         | 4.66     |
| 5   | Energy Teas            | 8         | 3.25     |
| 6   | Italian Sodas          | 5         | 4.25     |
| 7   | Dirty Sodas            | 10        | 2.00     |
| 8   | Hydraters              | 6         | 3.00     |
| 9   | Specialty Soft Drinks  | 6         | 3.38     |
| 10  | Fountain Drinks & More | 4         | 1.33     |
| 11  | Smoothies              | 5         | 3.99     |
| 12  | Summer Drinks          | 8         | 3.57     |
| 13  | Seasonal               | 4         | 4.50     |
| 14  | Food                   | 15        | 3.64     |

</div>

``` python
import matplotlib.pyplot as plt

df_plot = df_final.sort_values("AvgPrice", ascending=False)

plt.figure(figsize=(10, 6))
plt.bar(df_plot["Group"], df_plot["AvgPrice"])
plt.xticks(rotation=45, ha="right")
plt.xlabel("Menu Category")
plt.ylabel("Average Price")
plt.title("Average Menu Item Price by Category (Highest to Lowest)")
plt.tight_layout()
plt.show()
```

![](readme_files/figure-commonmark/cell-14-output-1.png)

In looking at the average prices for each menu category, it is clear
that specialty drinks do have a higher price. Taking into account that
the price is for the smallest size without any modifications (such as
alternative milks or extra syrups), there could also be some price
variability that is not accounted for in specialty beverages that may
not be as prevalent for fountain drinks or food. Overall, the menu shows
a clear emphasis on higher-priced specialty beverages, suggesting that
QuickSip focuses on premium, customizable drink offerings rather than
low-cost commodity beverages. As mentioned above, with so many other
coffee companies on the same street, I wonder if QuickSip could do
better by diversifying more heavily into other product categories or by
moving closer to the university.

------------------------------------------------------------------------

## Results and Discussion

- **Menu Size Comparison:** QuickSip offers mostly specialty coffee
  drinks, including holiday beverages, followed by food items.  
- **Average Pricing:** The mean price of seasonal beverages is the
  highest, which possibly indicates the business’ perceived highest
  demand.

Discussion: The data suggests QuickSip’s pricing strategy is oriented
towards high-end specialty beverages. The coffee shop might be missing
opportunities by not focusing on menu items that competitors do not
offer, such as food items like pizzas or breakfast sandwiches. It could
also potentially bring in more revenue by moving locations to the other
side of town where they would have a monopoly on the coffee market.

------------------------------------------------------------------------

## Business Suggestions

Based on the analysis:

- **Expand Non-Coffee Offerings:** There may be a higher local demand
  for food items and smoothies.
- **Location Adjustment:** The coffee shop could consider moving to the
  south side of town to target the college-aged market and move further
  from competitors.

------------------------------------------------------------------------

## Limitations and Future Work

- **Data Limitations:** Data is current as of early December 2025, but
  menu offerings can change rapidly.
- **Data Gaps:** I was not able to analyze customer reviews due to lack
  of data.
- **Future Work:** I would analyze the scraped data with customer
  surveys or sales data.

------------------------------------------------------------------------

## References

- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [QuickSip Menu](https://quicksip.co)
