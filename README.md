# Socio-Economic Country Segmentation using PCA and K-Means

This project performs an in-depth analysis of socio-economic and health-related data for 167 countries. The primary objective is to use unsupervised machine learning to segment these countries into distinct groups, which can help non-governmental organizations (NGOs) identify nations that are most in need of aid.

The notebook demonstrates a complete data science workflow, including Exploratory Data Analysis (EDA), data preprocessing, dimensionality reduction using Principal Component Analysis (PCA), and customer segmentation with the K-Means clustering algorithm.

## Dataset
[Kaggle](https://www.kaggle.com/code/emirhanhasrc/country-data-eda-pca-kmeans-ipynb?scriptVersionId=253218375)
The dataset used is `Country-data.csv`, containing key development indicators for 167 countries.

### Dataset Features

The dataset consists of the following 10 features:

| Feature | Description | Type |
| :--- | :--- | :--- |
| **country** | Name of the country. | Categorical |
| **child_mort** | Death of children under 5 years of age per 1000 live births. | Numeric |
| **exports** | Exports of goods and services per capita, given as a percentage of the GDP per capita. | Numeric |
| **health** | Total health spending per capita, given as a percentage of the GDP per capita. | Numeric |
| **imports** | Imports of goods and services per capita, given as a percentage of the GDP per capita. | Numeric |
| **income** | Net income per person. | Numeric |
| **inflation** | The measurement of the annual growth rate of the Total GDP. | Numeric |
| **life_expec** | The average number of years a new born child would live if the current mortality patterns are to remain the same. | Numeric |
| **total_fer** | The number of children that would be born to each woman if the current age-fertility rates remain the same. | Numeric |
| **gdpp** | The GDP per capita. Calculated as the Total GDP divided by the total population. | Numeric |

## Methodology

The project follows a structured approach to segment the countries based on the provided data.

### 1. Exploratory Data Analysis (EDA)

A thorough EDA was conducted to understand the data's underlying structure and relationships.

-   **Data Inspection**: The dataset was confirmed to be clean with **no missing values**.
-   **Distribution Analysis**: Histograms were plotted for all numerical features to visualize their distributions. Many features, such as `child_mort` and `income`, exhibited significant skewness.
-   **Correlation Analysis**: A heatmap of the correlation matrix was generated. It revealed strong correlations between several features, such as:
    -   `gdpp` and `income` (strong positive correlation).
    -   `child_mort` and `life_expec` (strong negative correlation).
    -   `child_mort` and `total_fer` (strong positive correlation).
    This high level of multicollinearity suggests that dimensionality reduction would be beneficial.

### 2. Data Preprocessing

-   The non-numeric `country` column was dropped to prepare the data for machine learning.
-   All features were scaled using **MinMaxScaler** to normalize their ranges to \. This step is crucial for distance-based algorithms like PCA and K-Means, as it prevents features with larger scales from dominating the analysis.

### 3. Dimensionality Reduction with PCA

To address multicollinearity and reduce the number of features, **Principal Component Analysis (PCA)** was applied.

-   A plot of the cumulative explained variance showed that the first **3 principal components** capture approximately **80.5%** of the total variance in the data.
-   Therefore, the dataset was transformed and reduced to these three principal components for the clustering analysis.

### 4. Clustering with K-Means

The K-Means algorithm was used to group the countries into clusters based on the three principal components.

-   **Elbow Method**: The Within-Cluster Sum of Squares (WCSS) was plotted for a range of k-values (1 to 10). The "elbow" point was clearly identified at **k=3**, indicating that 3 is the optimal number of clusters for this dataset.
-   **Model Fitting**: A K-Means model with `n_clusters=3` was fitted to the PCA-transformed data.
-   **Evaluation**: The **silhouette score** for the 3-cluster model was **0.438**, which indicates a reasonably good clustering structure where clusters are fairly dense and well-separated.

## Results and Cluster Analysis

The K-Means algorithm successfully segmented the 167 countries into three distinct groups. By analyzing the original feature values for each cluster (using boxplots for `child_mort` and `income`), we can interpret these groups as follows:

1.  **Cluster 1: Under-developed Countries (Budget Needed)**
    -   **Characteristics**: These countries exhibit very **high child mortality** and extremely **low income** and **GDP per capita**. They are in urgent need of humanitarian aid.
    -   **Countries Include**: Afghanistan, Angola, Benin, Burkina Faso, etc.

2.  **Cluster 2: Developing Countries (In Between)**
    -   **Characteristics**: This group has **moderate levels** of child mortality, income, and GDP per capita. While better off than the first group, they still face significant development challenges.
    -   **Countries Include**: Albania, Algeria, Brazil, Egypt, India, etc.

3.  **Cluster 0: Developed Countries (No Budget Needed)**
    -   **Characteristics**: These countries are characterized by very **low child mortality** and very **high income** and **GDP per capita**. They are economically stable and do not require aid.
    -   **Countries Include**: Australia, Canada, Germany, Japan, United States, etc.

## Conclusion

This analysis effectively demonstrates the power of unsupervised learning in identifying meaningful patterns in complex datasets. The combination of **PCA for dimensionality reduction** and **K-Means for clustering** successfully segmented the countries into three distinct socio-economic tiers: under-developed, developing, and developed.

The results provide a clear, data-driven framework for NGOs and other aid organizations to prioritize their resources. By focusing on the countries in the "Budget Needed" cluster, they can ensure that their efforts are directed towards the nations facing the most critical challenges in health and economic stability.
