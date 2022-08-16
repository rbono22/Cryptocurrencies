# Cryptocurrencies

## Project Overview
The purpose of this project is to analyze cryptocurrency data using Unsupervised Machine Learning. The original cryptocurrency data from [CryptoCompare](https://min-api.cryptocompare.com/data/all/coinlist) is preprocessed using Pandas to fit Unsupervised Machine Learning models. A clustering algorithm is used to group data and hvPlot visualization are used to share results.

## Software
- Python 3.7
- scikit-learn 0.24
- hvPlot 0.7.0
- Plotly 4.14.3

## Results

### Elbow Curve

![elbow_curve](https://github.com/Mishkanian/Cryptocurrencies/blob/main/README_images/elbow_curve.png)

From the elbow curve above, it can be determined that the optimal number of clusters is 4 (k=4). This information is used for specifying the number of clusters (n_clusters) when initializing the K-means model:
```python
model = KMeans(n_clusters=4, random_state=0)
```

### 3D Plot

![3d_plot](https://github.com/Mishkanian/Cryptocurrencies/blob/main/README_images/3d_plot.png)

This 3D scatter plot with cluster is generated using the following code:

```python
fig = px.scatter_3d(
    clustered_df,
    x="PC 1",
    y="PC 2",
    z="PC 3",
    hover_data=["Algorithm"],
    hover_name="CoinName",
    color="Class",
    symbol="Class",
    width=800
)
fig.update_layout(legend=dict(x=0, y=1))
fig.show()
```

### hvTable

![hv_table](https://github.com/Mishkanian/Cryptocurrencies/blob/main/README_images/hv_table.png)

The hvTable above displays all of the currently tradeable cryptocurrencies. This table is created using the hvplot.table() function.
```python
columns = ["CoinName", "Algorithm", "ProofType", "TotalCoinSupply", "TotalCoinsMined", "Class"]
clustered_df.hvplot.table(columns)
```

### hvPlot (Scatter)

![hv_plot](https://github.com/Mishkanian/Cryptocurrencies/blob/main/README_images/hv_plot.png)

The graph above is a scatter plot grouped by class. This is created using hvplot.scatter. See the code below:

```python
plot_df.hvplot(
    kind="scatter", 
    x="TotalCoinsMined", 
    y="TotalCoinSupply", 
    by="Class",
    hover_cols=["CoinName"]
)
```
