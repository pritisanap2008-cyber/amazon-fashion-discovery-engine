# Amazon Fashion Discovery Engine

A content-based recommender that finds similar Amazon fashion products from their text (title, brand, features, description).

## Data
- smartcat/Amazon-2023-GenQ (Hugging Face, MIT license), read with streaming
- Random sample of 40,000 products, kept the category AMAZON FASHION: 26,350 products
- After removing short and duplicate titles: 25,994 products
- The category also includes shoes, jewellery, watches and accessories

## Method
- Two text versions: short (title + brand) and full (title + brand + features + description)
- Cleaning: lowercase, removed symbols and extra spaces
- TF-IDF (single words and word pairs) and cosine similarity, top 5 most similar products
- Compared short text, full text and a mix of both

## Evaluation
No shopper data is available, so I used precision@5: the share of the 5 recommendations that have the same product type as the chosen product. The type comes from keywords in the title (12 types, 15,400 products labeled). Tested on 1,000 random labeled products.

| Method | Precision@5 |
|---|---|
| Random guess | 0.134 |
| Short text | 0.635 |
| Full text | 0.672 |
| Mix of both | 0.672 |

Final method: full text.

## Limitations
- The type comes from the title, so the test favours methods that use the title
- 41% of products have no type and are not tested
- TF-IDF matches words, not meaning
- Images, colour and price are not used

## Tools
Python, pandas, numpy, scikit-learn, Hugging Face datasets, Google Colab
