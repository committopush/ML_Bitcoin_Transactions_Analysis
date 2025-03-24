# Analyzing Bitcoin Transactions with Pandas and Spark

## Project Description
This project analyzes Bitcoin transactions using Pandas, PySpark, and GPU-accelerated libraries like cuDF and cuGraph. It explores the performance and scalability of different tools, builds classification and clustering models, and applies network analysis using PageRank to identify influential Bitcoin addresses. The goal is to provide insights into transaction behavior and address influence within the Bitcoin network.

## Table of Contents
1. [Installation](#installation)
2. [Usage](#usage)
3. [Methodology](#methodology)
4. [Results](#results)
5. [Conclusion](#conclusion)
6. [Contributors](#contributors)

## Installation
To run this project, install the required libraries. You can install them manually or via `requirements.txt`:

```bash
pip install -r requirements.txt
```

Key dependencies:
- Pandas
- PySpark
- Scikit-learn
- Matplotlib
- Seaborn
- cuDF
- cuGraph

> Note: GPU support (for cuDF/cuGraph) is optional but improves performance for large graph operations.

## Usage
Clone the repository and run the notebook:

```bash
git clone https://github.com/committopush/ML_Bitcoin_Transactions_Analysis.git
cd ML_Bitcoin_Transactions_Analysis
jupyter notebook ML_Bitcoin_Transactions_Analysis.ipynb
```

## Methodology

### Part 0: Comparing Spark and Pandas Performance
- Compares the runtime of Spark and Pandas when computing the number of transactions each address has participated in.
- Benchmarks are taken over multiple runs for reliability.

**Insights:**
- PySpark performs significantly better on large datasets due to distributed computation.
- Pandas is faster on smaller datasets but scales poorly.

### Part 1: Basic Statistics Computation
- Calculates high-level transaction statistics such as totals, means, and standard deviations.
- Includes visualizations for transaction trends and value distribution.

### Part 2: Index Creation for Web Queries
Creates indices to support a hypothetical web service providing per-address statistics:

- **Account Balance:** Net balance computed from 'Input' and 'Output' columns.
- **Top-3 Commercial Partners:** Most frequently interacting counterparties.
- **Average Transaction Value:** Calculated over the address’s history.
- Additional metrics include:
  - **Address Age**
  - **Average Daily/Weekly/Monthly Transaction Values**
  - **Number of Inputs/Outputs**

### Part 3: Classification Models
- Builds machine learning models to classify addresses based on activity.
- **Feature Engineering:** Includes transaction frequency, average transaction value, and partner diversity.
- **Models Used:**
  - k-Nearest Neighbors (k-NN)
  - Random Forest
- **Evaluation Metrics:** Accuracy, Precision, Recall, F1 Score

**Results:**
- Random Forest significantly outperformed k-NN.
  - Accuracy: **72.31%**
  - Precision: **71.27%**
  - Recall: **72.31%**
  - F1 Score: **71.51%**

### Part 4: Clustering Addresses
- Applies KMeans clustering to group Bitcoin addresses by behavior.
- **Elbow Method** used to determine optimal number of clusters.
- **Outlier Detection** improves cluster cohesion.
- **PCA** used for 2D visualization of clusters.

**Insights:**
- Initial clusters were influenced by outliers.
- Removing outliers decreased the silhouette score slightly but improved cluster quality.

### Part 5: PageRank Analysis Using cuDF/cuGraph
- Models the transaction network as a directed graph.
  - **Nodes:** Addresses
  - **Edges:** Transactions weighted by BTC value
- Applies **PageRank** to determine influential addresses.

**Discussion:**
- PageRank revealed a few highly influential nodes.
- These may correspond to exchanges, mining pools, or large services.
- The distribution resembled real-world networks with central hubs.

## Results
- Identified the **Top-10 Largest Transactions**
- Visualized the **evolution of transaction volume** over time in both BTC and USD
- Demonstrated strong performance of **classification models**
- Showed effective **clustering of behaviorally similar addresses**
- Uncovered **key influencers** in the network via PageRank

## Conclusion
This project showcases the power of combining traditional data tools (Pandas, Scikit-learn), big data frameworks (PySpark), and GPU-accelerated libraries (cuDF, cuGraph) to analyze cryptocurrency transactions. It demonstrates how to extract behavioral patterns, group similar addresses, and identify key players in a decentralized network like Bitcoin.
