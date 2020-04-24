In this study, AmExpert’s data from Kaggle has been used. The measurement of a consumer’s propensity towards coupon usage and the prediction of the redemption behaviour are crucial parameters in assessing the effectiveness of a marketing campaign. So, the ultimate goal is to predict whether a customer will redeem a coupon or not. Five different tables were available with information on different aspects related to a customer. The detailed schema is provided in here https://www.kaggle.com/bharath901/amexpert-2019


•	Train: This table contains information related to customer’s ID, campaign ID, coupon used and redemption status (Yes/No).
•	Campaign: Data related to start and end date of a campaign along with type of campaign (anonymous, X/Y).
•	Item: Item information for each item sold by the retailer including brand (5528), brand type (established/local), selling price and category (Grocery, Miscellaneous, Bakery, Pharmaceutical, Packaged Meat, Seafood, Natural Products, Dairy, Juices & Snacks, Prepared Food, Skin & Hair Care, Meat, Travel, Flowers & Plants, Fuel, Salads, Alcohol, Garden, Restaurant, Vegetables (cut).
•	Coupon Item Mapping: Contains coupon ID and Item ID.
•	Customer Transaction: It contains date, customer ID, item ID, quantity purchased, amount of coupon discount and other discount.
•	Customer Demographics: Data related to customer ID, age range (18-25, 26-35, 46-55, 56-70 and 70+), marital status (Married/Single), Rented (0 - not rented accommodation, 1 - rented accommodation), family size (1,2,3,4 or 5), no. of children (0,1,2 or 3) and income bracket (1-12, higher income corresponding to higher number).

Customers receive coupons under various campaigns and may choose to redeem it. They can redeem the given coupon for any valid product for that coupon as per coupon item mapping within the duration between campaign start date and end date Next, the customer will redeem the coupon for an item at the retailer store and that will reflect in the transaction table in the column coupon discount. Promotions are shared across various channels including email, notifications, etc. A number of these campaigns include coupon discounts that are offered for a specific product/range of products. The aim is to predict whether customers redeem the coupons received across channels, to enable to accurately design coupon construct, and develop more precise and targeted marketing strategies.

1. Merging
Based on the above schema, tables were merged as follows:
i.	Train data was merged with campaign data using an inner join on campaign ID, resulting in 78,369 data points.
ii.	The above data was merged with coupon item mapping using an inner join on coupon ID, resulting in 6,420,694 data points.
iii.	Again, this data was merged with item data using an inner join on item ID, resulting in 6,420,693 data points.
iv.	Finally, this data was merged with customer data using a left join on customer ID, resulting in 6,420,693 data points.
v.	On removing duplicate values on the basis of campaign, coupon, customer, item IDs and redemption status, customer transaction data was merged using left join on customer ID and item ID, obtaining a total of 6,469,802 data points with 23 variables.

2. Pre-Processing
The following treatment was performed on null values:
•	Replacing age range, marital status, family size, no. of children, income bracket, rented and quantity with their respective modal values.
•	Replacing selling price, coupon discount and other discount with their mean values.
The following 10 variables were retained for final prediction of redemption status: Age Range, Rented, Marital Status, Family Size, No. of Children, Income Bracket, Quantity, Selling Price, Coupon Discount and Other Discount.

3. Prediction
For predicting coupon redemption propensity, with 10 independent variables, CatBoost, XGBoost and LightGBM were applied.
The three models were then compared based on accuracy and F-score to determine the best one.

