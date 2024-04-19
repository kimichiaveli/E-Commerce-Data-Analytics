# E-Commerce-Data-Analytics
Provided with the transaction data and relevant user information of an e-commerce platform, find out:

1. What factors contribute to users making a purchase?
2. What factors contribute to users generating higher basket amounts?

#### Quick notes on the dataset:
1. Imbalanced datasets, purchase convertion rate almost 97% (Q1 2019 Average Conversion Rate only around 2.72% as mentioned in https://sleeknote.com/blog/e-commerce-statistics). For now, lets assume that conversion rate is realy 97%.
2. While analyzing conversion rate, we’re gonna use a method called SMOTE to reduced the effect of an imbalance dataset.
3. There are outliers in Basket Amount (median around 0.000027, while max value is 1.0) that need to be removed first for better understanding.

### Approach

1. Explore the Datasets
2. Find relevant features (in which the e-commerce can control to maximize the output)
3. Find correlation and pattern to prioritize the biggest deciding feature to the output.
4. Explore the user’s behaviour to find the best strategy for each of them.

### Insight

#### Purchases Analysis
I used SHAP value as a tool to get a better understanding on how each feature will contributes to the model.<br>
![alt text](https://github.com/kimichiaveli/E-Commerce-Data-Analytics/blob/255ce6d5404b49308f1ddef15ceca043f3dba515/purchase.png 'Purchase SHAP Value')<br><br>
Example: trx_is_voucher has mean SHAP value of almost 0.5, this means that if a voucher is available to use, probability of the user to make the purchase increase by 0.5 (50%)

#### Basket Amount Analysis
I used the same methods to visualize each feature's contribution and also used Feature Importance as a comparison. Here are the Top 10 Contributor of Basket Amount using SHAP.<br>
![alt text](https://github.com/kimichiaveli/E-Commerce-Data-Analytics/blob/255ce6d5404b49308f1ddef15ceca043f3dba515/basket_amount.png 'Basket Amount SHAP Value')<br><br>
While here are the top contributors of Basket Amount using Feature Importance.<br>
![alt text](https://github.com/kimichiaveli/E-Commerce-Data-Analytics/blob/255ce6d5404b49308f1ddef15ceca043f3dba515/basket_amount_fi.png 'Basket Amount Feature Importance')<br><br>
Using insights from above we can make a business decisions such as:
1. Maximize promotion to province 1 users
2. Give out voucher/promo code to users who already purchased something in the same month (users who have not bought anything yet don't really need to be given voucher/promo code)
3. By giving voucher/promo code to users who already purchased something in the same month, especially in province 1 they probably will purchased something again with higher basket_amount
4. user_group 1 tends to do transaction with higher basket_amount, but note that there's only slight difference in the median
5. Increasing window shopping experience will lead to longer session length (aov) of a user and will likely to be persuaded into buying something of a higher value/basket_amount

### Recommendations to Stakeholders
1. Promoting vouchers to new users with the probability of them making their first purchase below 50% to increase conversion rate.
2. Promoting to vouchers to users who live in province 1 and already made their purchase in the same month to increase basket_amount
3. Optimize voucher’s system to ensure users making purchase.
