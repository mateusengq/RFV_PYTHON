# RFM_PYTHON
 
# 1. INTRODUCTION

- In this project, I applied a **RFM** and **unsupervised learning clustering using KMeans** to segment and profile clients.
- After the segmentation, a **Marketing Strategy** was recommended for each group.
- For this project, I had some limitations in data. The company shared the following informations: `id_client`, `product value` and `purchase_date`. The RFM was chosen because of the available data.

## 1.1. Business Problem
The company sells digital education products and has a platform with training, short and long courses, tutoring, and free content. The free content works as a hook to show the clients the methodology and the quality of the material. The company has B2B and B2C products.

The company has many initiatives for B2B clients and new B2C clients, but once the clients are in the company, they don't have any initiatives for them.

They believe that once clients are in the company, they don't purchase more products, but they are not certain about it.
    - To address this, we conducted a preliminary analysis and identified that this is true. After identifying this, they decided to take actions to engage the clients.

Considering this point, one initiative was to segment the clients into groups, offer discounts,  and change the way to contact and maintain the relationship with them.

## 1.2. Objectives
- Identify and profile different customer groups.
- Develop a personalized marketing strategy for the ideal customer group, aiming to improve client retention and increase revenue.

*IMPORTANT:* For this problem, I will apply the RFM analysis and clustering. RFM was chosen because it is a technique used in the company in other projects, and people are familiar with it, so they decided to follow the same strategy. It is also important to mention that we have a limited number of variables.

## 1.3. Solution Pipeline

1. Define the business problem.
2. Initial data understanding and Exploratory data analysis.
3. Data cleaning and preprocessing.
4. Group customers into clusters, modeling.
5. Analyze the groups created, profiling them (personas).
6. Suggesting strategies for each group

# 2. RFM MODEL

**RFM** or **RFV** is a common technique used in Marketing to segment customer data by plotting customers into a three-dimensional space using three metrics:
 - Recency: a measure of how recently a customer last purchased.
 - Frequency: how often they purchase within a given time period.
 - Monetary (Value): the amount they spend within a given time period.

Using these parameters, customers are classified into nine categories. This customer segmentation helps in the decision-making process for targeted marketing strategies and customer success, offering discounts and promotions, different kinds of products, etc.

For this project, I dediced to use a clustering technique to classify into groups instead of using the nine groups used from RFM. I choose to use clustering because it allows for a more flexible and data-driven approach to customer segmentation compared to the traditional RFM method. This can lead to more accurate and actionable insights about customer behavior, preferences and needs.

# 3. CLUSTERING

Clustering is a type of unsupervised learning technique in data analysis used to group similar data points together based on their characteristics. In the context of customer segmentation, clustering algorithms analyze customer data and identify natural groupings or clusters of customers who share similar behaviors and attributes. Unlike predefined segmentation methods, clustering does not require prior knowledge of the categories and can reveal unexpected patterns and relationships within the data.

The main idea of k-means algorithm is to choose *k* random points as centroids, label the instances, calculate a reference metric, then update the centroid points, label the instances again and recalculate the reference metric, continuing this process until the centroids stop moving.

## 3.1. The silhoutte score
A more precise metric used to define the best value for the number of the clusters is the silhouette score, which is the mean silhouette coefficient over all the instances. A sillhouette score can be written as:

$Silhoutte\_Score = \frac{(b-a)}{max(a,b)}$

Where:

- *a* is the mean distance to the other instance in the same cluster.
- *b* is the mean nearest-cluster distance.

The sillhouette score can vary between -1 and +1. A value close to +1 means that the instance is well with its own cluster and far from other cluster, while a coefficient close to 0 means that it is near boundary; a value close to -1 means that the instance may have been assigned the wrong cluster.


# 4. RESULTS
## 4.1. EDA
Main insights:
- Price variable issues: 
      - some values in the CRM have negative prices, which is an anomaly.
      - Some prices exceed the highest known product price, indicating possible data entry errors or inconsistencies.
![VAR PRICE](https://github.com/mateusengq/RFV_PYTHON/blob/main/GRAPH/PRICES_V1.png)
- 63% of the records are clients who made their last purchase before 2018 and have not bought anything since then. These records were excluded from the clustering analysis to focus on more relevant data.
- Considering only the valid records, 57,57% of the clients have not made any purchase.
      - It could be beneficial to analyze these inactive clients to understand the reasons behind their lack of purchases. Beyond the peak, there is a relatively flat distribution of clients over the remaining period, suggesting a steady rate of recent client activity.
![VAR PRICE AFTER AJUST](https://github.com/mateusengq/RFV_PYTHON/blob/main/GRAPH/VAR_PRICE.png)
- The recency graph shows a peak in the lower number,  indicating a significant number of clients have made recent purchases. but there is a kind of flat amount of clients during the period.
- Clients who spent more money on average per purchase tend to have fewer total purchases.
![VAR PRICE](https://github.com/mateusengq/RFV_PYTHON/blob/main/GRAPH/VAR_TOTAL_PURCHASE.png)
- 83% of the clients purchased only one product.

## 4.2. PREPROCESSING
Before the clustering, some tidying and cleaning were made:
    - I removed the prices that are higher than our higher-price product.
    - Negative prices were corrected.
    - Clients who last purchase was before 2018 were removed.
    - For the recency, I used the last purchase as a reference to calculate the number of days between yhe purchases and this reference.
    - For prices, I summed the values for each client using the `id_client` to group them.
    - As the variables have different scales, I applied **StandardScaler** to all of them.


## 4.2. CLUSTER
For clustering, I tried **KMeans**, **Agglomerative Clustering** and **Gaussian Mixture**, and the first showed better results for the Silhouette Score.
![SILHOUTTE SCORE](https://github.com/mateusengq/RFV_PYTHON/blob/main/GRAPH/SILHOUTTE_SCORE.png)

Considering the silhouette scores:
- KMeans (Blue Line):
    - The silhouette score generally increases with the number of clusters, peaking around k = 12 and stabilizing afterward.
    - KMeans performs well with higher values of k.
  
- Agglomerative Clustering (Orange Line):
    - Similar to KMeans, the silhouette score increases and stabilizes around k=12.
    - The silhouette score is consistently, suggesting good clustering performance.

- Gaussian Mixture (Green Line):
   - Shows more variability and generally lower silhouette scores compared to KMeans and Agglomerative Clustering.
    - Indicates less consistent clustering performance across different k values.

Considering the Elbow Method, the Silhouette score and the business strategy (there are some factors that limit the number of clusters), I decided to use 9 clusters.

## 4.3. RESULT
- After training k-means with 9 clusters, I created a boxplot and a scatterplot to visualize the clusters.
![BOXPLOT](https://github.com/mateusengq/RFV_PYTHON/blob/main/GRAPH/BOXPLOT_GROUPS.png)
![SCATTERPLOT](https://github.com/mateusengq/RFV_PYTHON/blob/main/GRAPH/SCATTER_GROUPS.png)

- Then, I analyzed the clusters that were formed and assigned profiles to them based on their variables RFM. These clusters were given the names and summaries:

## 4.3.1. PROFILE AND MARKETING STRATEGY

- **Cluster 0: Infrequent Low Spenders**
    - Name: Emma
    - Profile: Emma is a busy professional who rarely finds time for online learning. When she makes a purchase, it's usually a low-cost course to quickly brush up on a specific skill. She hasn't made any recent purchases, indicating she might have found other priorities.
    - Total Purchase: Low | Recency: High | Amount: Low

**Marketing Strategy:** Offer special discounts and promotions to encourage more frequent purchases.


- **Cluster 1: New Engagers**
    - Name: James
    - Profile: James recently discovered your platform and is exploring various free content and introductory offers. He's excited about learning but hasn’t committed to high-value purchases yet. He shows potential for becoming a loyal customer if nurtured properly with engaging content and special offers.
    - Total Purchase: Low | Recency: Low | Amount: Low

**Marketing Strategy:** Focus on engagement strategies like onboarding emails and introductory offers.


- **Cluster 2: Budget Learners**
    - Name: Sarah
    - Profile: Sarah is a budget-conscious learner who looks for affordable ways to improve her skills. She makes moderate purchases but is consistent is seeking value for her money. She often looks for discounts and bundles to make the most out of her limited budget.
    - She has enrolled in several mid-range courses and occasionally participates in webinars and free training sessions.
    - Total Purchase: Moderate | Recency: Moderate | Amount: Low
  
**Marketing Strategy:** Promote budget-friendly courses and training packages.

- **Cluster 3: Frequent Low Spenders**
    - Name: David
    - Profile: David loves learning new things but prefers smaller, more frequent investments in his education. He often purchases short, low-cost courses. Regularly, he checks for new content and makes frequent small purchases. 
    - Total Purchase: Low | Recency: Low to Moderate | Amount: Low
  
**Marketing Strategy:** Bundle low-cost products and promote subscription-based models.

- **Cluster 4: Engaged Budget Spenders**
  - Name: Linda
  - Profile: Linda is a dedicated learner who engages with the platform regularly. She spends a moderate amount on courses and training. Linda has been with your platform for a while and has steadily invested in various courses.
  - Total Purchase: Moderate | Recency: Moderate | Amount: Moderate

**Marketing Strategy:** Offer loyalty rewards and personalized course recommendations.

- **Cluster 5: Occasional High Spenders**
  - Name: Robert
  - Profile: Robert is selective about his learning investments, preferring to spend on high-quality, high-value courses occasionally. He typically makes a few big purchases a year. He values quality over quantity and looks for courses that offer substantial returns on his investment.
  - Total Purchase: Moderate | Recency: High | Amount: High
  
**Marketing Strategy:** Highlight premium content and high-value training programs.

- **Cluster 6: High Spenders with Low Engagement**
  - Name: Jessica
  - Profile: Jessica has spent a significant amount on our platform but doesn't engage frequently. She makes large purchases.
  - Total Purchase: High | Recency: High | Amount: High
  
**Marketing Strategy: Provide exclusive content and VIP access to keep them engaged.**

- **Cluster 7: High Value, High Engagement**
  - Name: Michael
  - Profile: Michael is one of your top customers, consistently spending a lot and engaging frequently. Regularly, he purchases high-value courses.
  - Total Purchase: High | Recency: Low to Moderate | Amount: High
  
**Marketing Strategy: Focus on retention with personalized communication, exclusive offers, and premium services.**

- **Cluster 8: Elite Learners**
  - Name: Alice
  - Profile: Alice is an elite learner who is highly committed to her personal and professional development. She makes substantial investments in her education and engages with almost all the content offered.
  - Total Purchase: Very High | Recency: Low to Moderate | Amount: Very High
  
**Marketing Strategy: Maintain close relationships through personal touchpoints and offer exclusive content and first access to new products.**


- For clusters 3 and 6, that have a higher recency and lower amount of purchase, a strategy could be to remove them from the client data and focus on the others clients who have "recent" memories of the products.

# 5. FURTHER STEPS

- For new clients, an idea is to create a model using other features to predict the clusters and set up the campaigns and strategies from the beginning of their journey with the company.
  
- Perform a deeper analysis of each cluster to understand the underlying reasons for their behavior. This could involve looking into additional features or segmenting further within the existing clusters.

- Develop personalized marketing strategies for each cluster. For example, groups with high recency but low purchase amounts might benefit from promotional offers or targeted advertising to convert their recent interest into higher spending.

- Focus on retention strategies for high-value clusters with lower recency. Implement loyalty programs, personalized communication, and special offers to re-engage these customers.

- Create new models considering more features such as customer demographics, browsing behavior, and social media interactions. This can provide more dimensions for clustering and reveal more nuanced customer segments.

- Conduct A/B tests in each group considering different kinds of products. This will help in understanding what types of products and offers are most effective for each cluster.