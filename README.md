# Grocery-Cart-Synergies
Unveiling Hidden Associations with Market Basket Analysis

----

## Market Basket Analysis with [Groceries Market Basket Dataset](https://www.kaggle.com/datasets/irfanasrullah/groceries)

### Objective:
The primary objective of this analysis is to uncover associations between different items in the groceries dataset using Market Basket Analysis (MBA). By identifying these associations, businesses can strategize their marketing efforts, optimize their product placements, and potentially increase sales.

### Data Loading:
The dataset used for this analysis is the "groceries - groceries.csv" file. It contains transactional data representing items purchased together in a single transaction.

```python
data = pd.read_csv('groceries - groceries.csv', header=None)
```

### Data Preprocessing:
The data was preprocessed to convert it into a list of transactions, where each transaction is a list of items.

```python
transactions = []
for i in range(0, len(data)):
    transactions.append([str(data.values[i, j]) for j in range(0, 20) if pd.notna(data.values[i, j])])
```

### Frequent Itemset Generation:
Using the `apriori` algorithm, frequent itemsets were generated with a minimum support threshold of 0.01.

```python
from mlxtend.frequent_patterns import apriori
frequent_itemsets = apriori(df, min_support=0.01, use_colnames=True)
```

### Association Rule Mining:
Association rules were derived from the frequent itemsets. The metric used for evaluation was 'lift', and a minimum threshold of 1 was set.

```python
from mlxtend.frequent_patterns import association_rules
rules = association_rules(frequent_itemsets, metric='lift', min_threshold=1)
```

### Visualizations:
A scatter plot was generated to visualize the association rules based on Support vs Confidence, with the color intensity representing the lift value.

```python
plt.figure(figsize=(12, 8))
plt.scatter(filtered_rules['support'], filtered_rules['confidence'], c=filtered_rules['lift'], cmap='YlGnBu', s=100)
plt.colorbar(label='Lift')
plt.xlabel('Support')
plt.ylabel('Confidence')
plt.title('Association Rules - Support vs Confidence')
plt.show()
```

![Association Rules - Support vs Confidence](https://chat.noteable.io/origami/o/99e82694745e4153b62a30b56301ed53.png)

### Final Insights and Recommendations:
The scatter plot provides insights into the relationships between different items. Items with higher support and confidence values are more frequently bought together, and the lift value indicates the strength of that relationship.

Businesses can leverage these insights to:
- Bundle products that are frequently bought together.
- Offer discounts on complementary products.
- Optimize the placement of products in stores to encourage cross-selling.

### Sources:
- Dataset: [Groceries Market Basket Dataset](https://www.kaggle.com/datasets/irfanasrullah/groceries)
