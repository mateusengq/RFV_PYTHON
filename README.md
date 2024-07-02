# RFM_PYTHON
 
# 1. INTRODUCTION

- In this project, I applied a **RFM** and **unsupervised learning clustering using KMeans** to segment and profile clients.
- After the segmentation, a **Marketing Strategy** was recommended for each group.
- For this project, I had some limitations in data. The company shared the following informations: `id_client`, `product value` and `purchase_date`. The RFM was choosen because of the available data.

## 1.1. Business Problem
The company sells digital education products and has a platform with training, short and long courses, tutoring, and free content. The free content works as a hook to show the clients the metodology and the quality of the material. The company has B2B and B2C products.
The company has many iniciatives for B2B clients and new B2C clients, but once the clients are in the company, they don't have any iniciatives for them.

They believe that once clients are in the company, they don't purchase more products, but they are not certain about it.
    - To address this, we conducted a preliminary analysis and identify that this is true. After identifying this, they decided to take actions to engaje the clients.

Considering this point, one iniciative was to segment the clients into groups, offer discounts,  and change the way to contact and maintain the relationship with them.

## 1.2. Objectives
- Identify and profile different customer groups.
- Develop a personalized marketing strategy to the ideal customer group, aiming to improve client retention and increase revenue.

*IMPORTANT:* For this problem, I will apply the RFM analysis and clustering. RFM was chosen because it is a technique used in the company in other projects, and people are familiar with it, so they decided to follow the same strategy. It is also important to mention that we have a limited number of variables.

## 1.3. Solution Pipeline

1. Define the business problem.
2. Initial data understanding and Exploratory data analysis.
3. Data cleaning and preprocessing.
4. Group customers into clusters, modelling.
5. Analyze the groups created, profiling them (personas).
6. Suggesting strategies for each group

# 2. RFM MODEL

**RFM** or **RFV** is a common technique used in Marketing to segment customer data by plotting customers into a three-dimensional space using three metrics:

    - Recency: a mensure of how recently a customer last purchased.
    - Frequency: how often they purchase within a given time period.
    - Monetary (Value): the amount they spend within a given time period.

Using these parameters, customers are classified into nine categories. This customer segmentation helps in the decision-making process for targeted marketing strategies and customer success, offering discounts and promotions, different kinds of products, etc.

For this project, I dediced to use a clustering technique to classied into groups instead of using the nine groups used from RFM. I choose to use clustering because it allows for a more flexible and data-driven approach to customer segmentation compared to the traditional RFM method. This can lead to more accurate and actionable insights about customer behavior, preferences and needs.

# 3. CLUSTERING

Clustering is a type of unsupervised learning technique in data analysis to group similar data points together based on their caracteristics. In the conxtext of customer segmentation, clustering algorithms analyze customer data and identify natural groupings or clusters of customers who share similar behaviors and attributes. Unlike predefined segmentation methods, clustering does not require prior knowledge of the categories and can reveal unexpected patterns and relationships within the data.
The main ideia of k-means algotithm is to choose *k* random points as centroids, label the instances, calculate a reference metric, then update the centroid points, label the instances again and recalculate the reference metric, continuing this process until the centroids stop moving.

## 3.1. The silhoutte score
A more precise metric used to define the best value for the number of the clusters is the silhoutte score, which is the mean silhoutte coefficient over all the instances. A sillhoutte score can be written as:

$Silhoutte\_Score = \frac{(b-a)}{max(a,b)}$

Where:
    - *a* is the mean distance to the other instance in the same cluster.
    - *b* is the mean nearest-cluster distance.

The sillhoutte score can very between -1 and +1. A value close to +1 means that the instance is well with its own cluster and far from other cluster, while a coefficient close to 0 means that it is near boundary; a value close to -1 means that the instance may have been assigned the wrong cluster.


# 4. RESULTS



# 5. FURTHER STEPS

