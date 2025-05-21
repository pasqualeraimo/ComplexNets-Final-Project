# Recipe Co-occurrence Network Analysis

## Project Overview

This project focuses on analyzing culinary data to construct and explore a network of recipe similarities. Recipes are connected based on the number of ingredients they share, allowing for a quantitative understanding of ingredient combinations and relationships between different dishes.

The core idea is to transform raw recipe-ingredient data into a network graph, enabling the application of network science techniques to uncover hidden structures and patterns in culinary systems.

## Features

* **Data Loading & Preprocessing:** Efficiently loads recipe-ingredient data from a CSV file, focusing on essential columns.
* **Recipe Sampling (Optional):** Includes functionality for random sampling of recipes to manage dataset size and computational load, especially beneficial for large datasets.
* **Data De-duplication:** Crucial step to ensure accurate ingredient counts per recipe by removing duplicate (Recipe ID, Entity ID) pairs, thus preventing inflated co-occurrence weights.
* **Co-occurrence Matrix Construction:** Builds a sparse matrix where each entry represents the number of shared ingredients between any two recipes.
* **Weight Thresholding:** Filters the co-occurrence matrix to retain only significant connections (i.e., recipes sharing more than a specified number of ingredients), reducing noise and focusing on strong relationships.
* **Network Graph Creation:** Converts the processed co-occurrence matrix into an undirected graph using the `NetworkX` library.
* **Node Relabeling:** Maps numerical indices of graph nodes back to their original recipe IDs for improved interpretability.
* **Basic Network Analysis:** Calculates and displays fundamental graph metrics such as:
    * Number of nodes (recipes)
    * Number of edges (significant shared ingredient connections)
    * Average degree
    * Number of connected components
    * Degree centrality (to identify key recipes)
    * Average clustering coefficient (to measure local network density)
* **Graph Export:** Saves the generated network in Pajek `.net` format, compatible with network visualization tools like [Gephi](https://gephi.org/) or [Pajek](http://vlado.fmf.uni-lj.si/pub/networks/pajek/).

## Dataset

The project expects a CSV file containing recipe and ingredient information.
* **Expected File:** `04_Recipe-Ingredients_Aliases.csv` (or a similar CSV file).
* **Required Columns:** The CSV must include at least two columns:
    * `Recipe ID`: Unique identifier for each recipe.
    * `Entity ID`: Identifier for each ingredient.
    Each row represents an instance of an ingredient being part of a recipe.

## Prerequisites

To run this project, you need Python 3.x and the following libraries:

* `pandas`
* `numpy`
* `scipy`
* `networkx`
* `tqdm` (optional, for progress bars during manual graph construction, but good practice for large loops)

You can install these dependencies using pip:
```bash
pip install pandas numpy scipy networkx tqdm