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
```

## Usage

This project is primarily designed to be run within a Jupyter Notebook environment.

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/pasqualeraimo/ComplexNets-Final-Project](https://github.com/pasqualeraimo/ComplexNets-Final-Project)
    cd YourRepoName
    ```
2.  **Place your dataset:** Ensure your `04_Recipe-Ingredients_Aliases.csv` file (or your equivalent dataset) is located in the specified `file_path` (e.g., `./culinaryDB/`).
3.  **Open the Jupyter Notebook:** Organize the provided Python code into separate cells as outlined in the provided Jupyter Notebook Markdown structure.
4.  **Adjust Parameters:**
    * Update `file_path` in the main execution block to correctly point to your dataset.
    * Modify `sample_percentage` (e.g., `0.20` for 20% of recipes) and `threshold_weight` (e.g., `7` for sharing more than 7 ingredients) parameters in the `build_cooccurrence_matrix_fast` function call based on your dataset size and desired network density.
5.  **Execute Cells:** Run the Jupyter Notebook cells sequentially from top to bottom.

## Output

Upon successful execution, the script will:

* Print various debugging and progress messages to the console, including matrix dimensions, number of non-zero entries, and graph statistics.
* Generate a `.net` file (e.g., `recipe_similarity_network.net`) in the project directory. This file represents the final recipe co-occurrence graph and can be imported into network visualization software (like Gephi) for interactive exploration and advanced analysis.

## Acknowledgements & References

This project draws inspiration from methodologies used in the complex network analysis of culinary systems. Specifically, related work often explores the bipartite networks of recipes and ingredients to derive co-occurrence patterns, similar to the approach found in research papers such as:

* Caprioli, C., Kulkarni, S., Battiston, F., Iacopini, I., Santoro, A., & Latora, V. (Year). *The networks of ingredient combination in cuisines around the world*. (You might want to check the full citation if it's the `cuisine.pdf` paper you referenced).
* 