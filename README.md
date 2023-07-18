# Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning

## Data Understanding
- Description
  - This dataset contains several features based on customer behavior that is carried out on a website.
- Shapes
  - Consists of 2240 lines, 29 Features
- Data Types
  - Float64: 1 Features
  - Int64: 25 Features
  - Object: 3 Features
- Missing Values
  - There are missing values in the Income feature
- Duplicated Data
  - There are no duplicate data

## Feature Engineering
- Conversion Rate: Response/NumWebVisitsMonth
- Customers Age: Difference between the current year and the year of birth ('Year_Birth')
- Customer Age Group:
  - young adults (18–35 years old)
  - middle-aged adults (36–55 years old)
  - older adults (older than 55 years old)
- Total Accepted Campaign: Add up all accepted campaign fields marked with the prefix 'AcceptedCmp'
- Total Spent: Add up all the amount spent columns marked with the prefix 'Mnt'
- Total Purchase: Add up all purchase columns marked with the prefix 'Num'
- Number of Children: Add up two features/columns, namely Kidhome and Teenhome
- Total Days Joined: The number of days since you first became a member
- Years Customer: The number of years since you first became a member

## Conversion Rate Analysis
There are 3 features that have a high correlation with conversion_rate, namely response, total_acc_camp, and total_spent. 
These three features have a positive correlation, meaning that if Response, Total Accepted Campaign, and Total Spend increase, 
the Conversion Rate will also increase and vice versa.

![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/8771c8da-e4f6-466f-b116-99e33b4bb61f)

![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/7caa83ec-a219-4201-8728-5edfc20b13e3)

The three top 3 features that correlate with the conversion rate have enough evidence that the correlation is significant 
because these three features have a p-value <0.05.

## Total Accepted Campaign Analysis
There are 3 features that have a high correlation with the total accepted campaign, namely conversion_rate, response, and total_spent. 
These three features have a positive correlation, meaning that if the Conversion Rate, Response, and Total Spend increase, 
the Total Accepted Campaign will also increase.

![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/91c5bbc4-ea66-43bc-a2d1-3b1f70cfcb13)

![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/7dbf5b23-a346-4768-8482-f129e25b6cc4)

The three top 3 features correlate with the total accepted campaign. 
There is sufficient evidence that the correlation is significant because the p-value of the three features is < 0.05.

## Data Cleaning and Preprocessing
- Missing Values
  
Missing values are found in the Income feature, which is 24 data (1.07% of data).

Handling way:
The mean and median values for the Income feature tend to be the same. However, to fill in the missing value in the Income feature, the median value will be used because the median is relatively robust from the outliers (not affected by very high or low values).
- Duplicated Data
  
There are no duplicate data, so there is no need to delete duplicate data.

- Feature Encoding
  
The data to be used for modeling is a numeric data type, so feature encoding is not necessary.

- Feature Selection
  There are 4 components to choose from:
  - L (Loyalty/Length): the number of days the customer has since becoming a member for the first time -> total_days_joined
  - R (Recency): the number of days since the customer's last purchase -> Recency
  - F (Frequency): total number of purchases made -> total_purchase
  - M (Monetary): amount spent on the whole product -> total_spent

- Handling Outliers
  Perform outlier removal on 2 features, namely:
  - total_purchase
  - total_spent

## Final Distribution for Data Modelling

![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/25dc4452-55c5-4d31-853e-e9782d18b7b8)

## Data Modelling

- Number of Clusters

  From the output results, the number of clusters that have a balanced composition with each cluster member and taking into account the average shilouette score of each cluster is 3 clusters. Although 6 clusters have a higher average shilouette score than 3 clusters, 6 clusters have an unequal composition of each cluster member compared to 3 clusters, as well as 2 clusters have an unequal composition of each cluster member even though the silhouette score is higher.
  
- PCA

  ![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/a6116095-f4e6-4597-8d47-17f11bf7d98e)

  The selected n_components are 3 components because the variation in the data that is covered is around 90%.

- Clustering Visualization

  ![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/065b0e30-4258-49a2-9d24-c95be14ef739)

## Customer Personality Analysis for Marketing Retargeting

![image](https://github.com/nunuufdlh01/Predict-Customer-Personality-to-boost-marketing-campaign-by-using-Machine-Learning/assets/89932073/724563ae-d82b-4190-b71d-e5e88f51dda0)

<p style="text-align: center;">
Table - Accumulated LRFM Value Results in Each Cluster
</p>

|  Cluster  | High Value | Average Value | Low Value |
| :-------- | :--------: | :-----------: | :-------: |
| **Cluster 0** | R | L | F M |
| **Cluster 1** | L F M | R |  |
| **Cluster 2** |  |  | L R F M |

## Clustering Interpretation
- Cluster 0 - Medium Customers
  - There are 650 customers (29.25%).
  - Customers in this group have a high average recency, around 76 days since the last purchase, a moderate average loyalty (number of days since becoming a member), around 3578 days, as well as an average frequency (total_purchase) and an average monetary (total_spent) is low, about 6 times and 167K respectively.
- Cluster 1 - Customer Loyalty
  - There are 896 customers (40.32%)
  - Customers in this group have a moderate average recency, around 49 days since the last purchase, the average loyalty (number of days since becoming a member) is very high, meaning this customer has been a member for a long time, which is around 3680 days, the average frequency (total_purchase) is also high in the sense that this customer often makes purchases, which is about 14 times, and the monetary average (total_spent) is also high in the sense that this customer spends a lot of money to make purchases on the company's platform, around 983K.
- Cluster 2 - New Customers
  - There are 676 customers (30.42%)
  - Customers in this group have a low average recency, around 24 days since the last purchase, a low average loyalty, around 3554 days, meaning this customer is a customer who has just subscribed to the company's platform, the average frequency (total_purchase) is low, about 5 times the purchase, and the average monetary (total_spent) is also low, around 138K.

## Business Recommendations
- Cluster 0 - Medium Customer: provide a special email to this customer with the title 'we miss you', provide special discounts, free shipping, and special promos based on customer behavior to avoid churn on this customer, because this customer's membership is in an intermediate condition and transactions the last thing that was done was quite a long time with the number of purchases and funds spent quite a bit.

- Cluster 1 - Loyalty Customer: this group must be given treatment so that they feel that the company values their loyalty by giving a special email to this customer in the form of a thank you for being loyal to using our company's platform, it can also be in the form of giving points for each transaction if the points are enough reaching a certain amount can be exchanged for free shipping vouchers and/or product offers from platforms based on customer behavior.

- Cluster 2 - New Customers: provide even more treats so that this group can shop longer and more frequently on this platform, which can be in the form of free shipping discount vouchers, personalized campaigns, or promos for various products offered through personal accounts on the platform or via email privately owned.

Applies to all clusters: creates a membership level program, in the form of bronze, silver, and gold with each membership level having its own features as measured by how often transactions are made and the price of the products purchased.

## Potential Impact

If we continue to prioritize customers in this group and none of them churn, then we still have a potential GMV (Gross Merchandise Value) of IDR 1.08 billion, with the following details:

- Medium Customers: IDR 109 Million
- Loyalty Customers: IDR 880 Million
- New Customers: IDR 93 Million








