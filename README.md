# Grocery-Cart-Synergies
Unveiling Hidden Associations with Market Basket Analysis
Certainly! Here's a GitHub `README.md` formatted version of the final analysis:

---

# Market Basket Analysis (MBA) Project

## Objective

To uncover associations between items in a grocery dataset and provide insights into potential product bundling or placement strategies.

## Dataset

The dataset used for this analysis is the "groceries - groceries.csv" file, which contains transactional data from a grocery store. Each row represents a transaction, and the items purchased in that transaction are listed.

[Link to Dataset](https://app.noteable.io/p/ff43fb9d-b304-4683-a757-7aa1eab999c6/MBA-Projectv1)

## Steps

### 1. Data Loading

The dataset was loaded into a pandas DataFrame using the `read_csv` function.

```python
import pandas as pd

data = pd.read_csv('groceries - groceries.csv')
```

### 2. Data Preprocessing

The data was preprocessed to transform it into a format suitable for association rule mining. Transactions were extracted, and a one-hot encoded matrix was created.

```python
transactions = data.values.tolist()
transactions = [list(filter(lambda x: str(x) != 'nan', transaction)) for transaction in transactions]
```

### 3. Frequent Itemset Generation

The Apriori algorithm was used to generate frequent itemsets. The `mlxtend` library was utilized for this purpose.

```python
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori

te = TransactionEncoder()
te_ary = te.fit(transactions).transform(transactions)
df = pd.DataFrame(te_ary, columns=te.columns_)
frequent_itemsets = apriori(df, min_support=0.01, use_colnames=True)
```

### 4. Association Rule Mining

Association rules were generated using the `association_rules` function from the `mlxtend` library.

```python
from mlxtend.frequent_patterns import association_rules

rules = association_rules(frequent_itemsets, metric="lift", min_threshold=1)
```

### 5. Visualizations

Visualizations were generated using the `matplotlib` and `seaborn` libraries to provide insights into the association rules. These visualizations included:

- A scatter plot of support vs confidence
- A heatmap of item pairs and their corresponding lift values

### 6. Final Insights and Recommendations

Based on the association rules and visualizations:

- Certain items are frequently bought together, indicating potential for product bundling or co-marketing strategies.
- The placement of items in the store can be optimized based on the association rules to encourage cross-selling.
- Discounts or promotions can be offered on items that have strong associations to drive sales.

## Sources

- Dataset: [groceries - groceries.csv](https://app.noteable.io/p/ff43fb9d-b304-4683-a757-7aa1eab999c6/MBA-Projectv1)
- [mlxtend library documentation](http://rasbt.github.io/mlxtend/)

---

You can use the above markdown content to create a `README.md` file for your GitHub repository. This provides a clear and concise overview of the Market Basket Analysis project, the steps taken, and the insights derived from the analysis.
