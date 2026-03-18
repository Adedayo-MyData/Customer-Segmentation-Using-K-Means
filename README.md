# Customer Segmentation Using K-Means

## Project Overview

This project applies unsupervised machine learning to identify natural customer groups based on behavioral patterns. Using a dataset of 5,000 customers, clustering techniques were used to detect segments that differ in spending habits, loyalty levels, satisfaction, and store visit frequency.

The analysis pipeline includes:

1. Data quality validation  
2. Outlier detection using the Interquartile Range (IQR) method  
3. Feature scaling using RobustScaler  
4. Dimensionality reduction using Principal Component Analysis (PCA)  
5. Customer segmentation using K-Means clustering  

The goal is to uncover actionable customer segments that can support targeted marketing strategies, customer retention, and revenue optimization.

---

## Dataset Overview

The dataset contains 5,000 customer records with the following variables:

| Variable                     | Description |
|----------------------------|------------|
| Customer_Satisfaction       | Satisfaction score collected from customer feedback |
| Customer_Loyalty_Score      | Loyalty indicator reflecting engagement level |
| Annual_Spending_USD         | Total yearly spending by the customer |
| Visits_Per_Month            | Average number of store visits per month |

---

## Initial Observations

### Summary Statistics

| Metric | Satisfaction | Loyalty Score | Spending (USD) | Visits |
|--------|-------------|--------------|----------------|--------|
| Mean   | 5.67        | 0.035        | 534            | 7.7    |
| Median | 5.59        | 0.0077       | 422            | 6.8    |
| Max    | 10.63       | 2.96         | 2021           | 25.3   |

### Key Observations

- Customer satisfaction generally falls between 5 and 7, indicating moderate satisfaction levels  
- Visit frequency varies significantly, with some customers visiting more than 20 times per month  
- Spending distribution contains extreme high-value customers, suggesting the presence of potential outliers  

---

## Data Quality Checks

### Missing Values
The dataset was examined for missing values.

**Result:**  
No missing values were detected across all variables.

### Duplicate Records
The dataset was also checked for duplicate rows.

**Result:**  
0 duplicate records were found.

These checks confirmed that the dataset required minimal cleaning before analysis.

---

## Outlier Detection

Outliers were identified using the Interquartile Range (IQR) method on the **Annual_Spending_USD** variable.

Customers exceeding the upper IQR bound were identified as extreme spending outliers. Detecting these values is important because unusually large spending amounts can distort clustering results.

---

## Correlation Analysis

A correlation heatmap was created to explore relationships between customer behavior variables.

### Key Discoveries

- All variables show positive relationships with each other  
- Customers who visit more frequently tend to spend more annually  
- Higher loyalty scores are associated with higher spending levels  

These patterns suggest that customer engagement is strongly connected to revenue generation.

---

## Feature Scaling

Because the dataset variables operate on different numerical scales (for example spending vs. satisfaction scores), the data was scaled using **RobustScaler**.

RobustScaler was selected because it:

- Uses the median and IQR instead of the mean and standard deviation  
- Is less sensitive to outliers  
- Preserves the structure of the data when extreme values are present  

---

## Dimensionality Reduction with PCA

To simplify the dataset and improve visualization, Principal Component Analysis (PCA) was applied.

| Component | Variance Explained |
|----------|-------------------|
| PC1      | 83.6%             |
| PC2      | 7.4%              |

**Total variance retained:** ~90.98%

This indicates that two principal components capture almost all behavioral variation in the dataset, making it ideal for visualization and clustering.

---

## Determining the Optimal Number of Clusters

The Elbow Method was used to determine the optimal number of clusters.

The inertia curve showed a clear bend at:

**K = 3**

This indicates that the dataset naturally forms three distinct customer groups.

---

## K-Means Clustering Results

The final clustering model used:

KMeans (n_clusters = 3, random_state = 42)

### Cluster Distribution

| Cluster   | Customers |
|----------|----------|
| Cluster 0 | 1,723    |
| Cluster 1 | 1,146    |
| Cluster 2 | 2,045    |

Cluster 2 represents the largest portion of customers, while Cluster 1 represents a smaller but higher-value segment.

---

## Clustering Quality

The clustering model achieved a **Silhouette Score of 0.60**.

### Interpretation

- Scores above 0.5 generally indicate strong cluster separation  
- This suggests that the clustering structure is well-defined and meaningful  

---

## Customer Segment Profiles

Cluster averages reveal clear behavioral differences between customer groups.

| Metric           | Cluster 0 | Cluster 1 | Cluster 2 |
|------------------|----------|----------|----------|
| Satisfaction     | 6.02     | 7.97     | 3.98     |
| Loyalty Score    | 0.20     | 1.20     | -0.80    |
| Annual Spending  | $499.97  | $1,179.29| $153.09  |
| Visits / Month   | 8.04     | 14.99    | 3.02     |

---

## Segment Interpretation

### Cluster 1 — High Value Customers

This segment represents the most profitable customers.

**Characteristics**

- Highest satisfaction: 7.97  
- Highest loyalty score: 1.20  
- Average spending: $1,179  
- Visit frequency: ~15 visits per month  

**Insights**

These customers are highly engaged and loyal, contributing the largest share of revenue.

**Business Implications**

- Priority segment for loyalty programs  
- Ideal targets for premium products and services  

---

### Cluster 0 — Regular Customers

This group represents stable mid-tier customers.

**Characteristics**

- Satisfaction around 6.0  
- Moderate loyalty levels  
- Average spending: ~$500  
- Visit frequency: ~8 visits per month  

**Insights**

These customers generate consistent revenue, but their loyalty could be improved.

**Business Implications**

- Opportunity to increase loyalty  
- Promotions may convert them into high-value customers  

---

### Cluster 2 — Low Value Customers

This segment includes the least engaged customers.

**Characteristics**

- Lowest satisfaction: 3.98  
- Negative loyalty score  
- Spending: $153  
- Visits: ~3 per month  

**Insights**

These customers interact with the business very infrequently and contribute minimal revenue.

**Business Implications**

- Requires re-engagement campaigns  
- May represent customers at risk of churn  

## Key Insights from the Analysis

Several important behavioral patterns emerged:

1. **Customer Loyalty Strongly Predicts Spending**  
   The highest spending segment also has the highest loyalty score  

2. **Visit Frequency Is the Strongest Behavioral Differentiator**  
   High-value customers visit the business five times more frequently than low-value customers  

3. **Satisfaction Levels Differ Across Segments**  
   Low-value customers show significantly lower satisfaction scores, indicating potential service issues  

4. **Customer Segments Are Clearly Separable**  
   The 0.60 silhouette score confirms that customers naturally form distinct groups  

---

## Power BI Dashboard

An interactive Power BI dashboard was developed to visualize segmentation results.

The dashboard allows users to:

- Explore cluster distributions  
- Compare spending behavior across segments  
- Analyze visit frequency patterns  
- Evaluate loyalty levels  
- Monitor customer satisfaction  

This enables stakeholders to explore segmentation results without requiring Python or machine learning knowledge.

---

## Business Applications

The segmentation model supports several business strategies:

### Targeted Marketing
High-value customers can receive exclusive promotions and personalized offers  

### Retention Strategies
Low-value customers can be targeted with re-engagement campaigns  

### Customer Lifetime Value Optimization
Marketing resources can be allocated based on segment profitability  

---

## Technologies Used

- Python  
- Pandas  
- NumPy  
- Scikit-Learn  
- Seaborn  
- Matplotlib  
- Power BI  

---

## Project Structure

customer-segmentation-project

customer-segmentation-project

¦  
+-- data  
¦   +-- Customer_segment_raw.csv  
¦  
+-- notebooks  
¦   +-- CustomerSegmtatn.ipynb  
¦  
+-- images  
¦   +-- Correlation_Matrix.png  
¦   +-- Customer_Clusters_Using_PCA.png  
¦   +-- Elbow_Method.png  
¦   +-- Outlier_Detection.png  
¦   +-- PCA_Projection_of_Customers.png  
¦   +-- Power_Bi_Visualization_1.png  
¦   +-- Power_Bi_Visualization_2.png  
¦  
+-- dashboard  
¦   +-- Customer Segmentation Visuals In Power Bi.pbix  
¦  
+-- outputs  
¦   +-- customer_segments_results.csv  
¦  
+-- README.md  

---

## Conclusion

This project demonstrates how unsupervised learning techniques can uncover meaningful behavioral patterns in customer data.

By combining PCA for dimensionality reduction and K-Means clustering, the analysis identified three distinct customer segments that differ significantly in satisfaction, loyalty, spending behavior, and visit frequency.

These insights highlight the importance of customer engagement and loyalty in driving revenue, and provide a foundation for data-driven marketing and retention strategies.

---

## Future Improvements

Several enhancements could further improve this project and increase its business value.

1. **Include Additional Customer Features**  
   Future analysis could incorporate more variables such as customer demographics, product preferences, or purchase channels to produce richer and more detailed customer segments  

2. **Evaluate Alternative Clustering Algorithms**  
   Other clustering methods such as Hierarchical Clustering, DBSCAN, or Gaussian Mixture Models could be tested to determine whether they produce more meaningful customer groupings than K-Means  

3. **Dynamic Customer Segmentation**  
   Customer behavior evolves over time. Implementing a system that updates clusters periodically would allow businesses to track changes in customer engagement and spending patterns  

4. **Integration with Marketing Strategy**  
   The segmentation results could be integrated into marketing systems to support personalized promotions, customer retention campaigns, and improved loyalty programs  

---

## Author

**Adedayo Adebayo**  
Data Scientist | Business Analyst
