## Market Basket Analysis

# Introduction

Instacart is a same-day grocery delivery service operating over a mobile/web application. The service sends the store/employee to shop for the customer and delivers to their home. Instacart&#39;s main source of revenue earned by adding a 15+ percentage markup to items and adds a service fee. In some cases, Instacart has made    deals with the grocery firms to offer in-store prices (noted on their site while shopping)1.

# Objective

To predict the items customers are likely reorder in the future. The business objective is to be able to identify, not only returning customers, but understand what causes these customers to return. First, a market basket analysis conducted to analyze products that couple well together. Using the data from market basket, a recommender system will generate products that suggests the user&#39;s next most likely reorders. In addition, with a better understanding of the market segmentation, I will increase my predictions. The business result is projected to increase sales by 5% in the short-term, within the year, and 20% in the long-run, estimated 2 years. This will be measured being able to identify more reorders of products by users, in addition

# Process

## Data Acquisition

 The datasets were provided to Kaggle from Instacart as a data-science competition. Items that were provided were as followed: aisles.csv.zip, departments.csv.zip, order\_products\_\_prior.csv.zip, order\_products\_\_train.csv.zip, orders.csv.zip, products.csv.zip, sample\_submission.csv.zip. Additional information was scraped from their website, which was primarily for locations; to understand their market segmentation.

## Exploratory Data Analysis (EDA)

  The primary dataset used was the &quot;order\_products\_\_train.csv.zip&quot;. It was the backbone that connected all other elements of the data. Layout of the data is visualized like the graphic as followed, to show levels of granularity. The departments, aisles, and products have names along with ID&#39;s. The ID&#39;s assigned at random and were easily linked to the ID&#39;s.

Other values are relating to the customer orders, which are as follows: Order ID, &quot;added\_to\_cart&quot;, and reorder. Order ID&#39;s are repeated sequential values that are used to track of each product purchased per order. Items placed into the basket used the &quot;added\_to\_cart&quot; denoting the order of items placed into the cart. Reorder, which was the focus, was used to denote whether that customer that customer had ordered the product before, also personal customer information was not provided.

Exploring the data, the aisle field was analyzed to help guide the research. When observed, the aisles of greatest number of records are as follows: fruits and vegetables were among the highest, along with, with packaged cheese, yogurt, and sparkling water (_see figure 2_). This may be something that causes inflation in some of the recommendations. There also appears to be a lot of organic food choices, which is something that could be indicative of the market segmentation. Although the data was well structured, it was not quite ready for modeling.

## Methodology (preprocessing)

To pass this data into a market basket analysis model, the aisle and product data needed to be One Hot Encoded (OHE), to get the data in a form that would not be increasing the magnitude per each aisle or product. In addition, once the data was O.H.E., the data would be summed by product ID and then re-encoded to using binary classification: using a 1 for presence and 0 for absence of an item in the basket. Once the data was encoded, the Apriori (market basket) model from &quot;mlxtend&quot; was imported to identify common item complements. The aisle data was easily used since there were only about 134 unique aisles. However, the product data was not the same story.

During the product preprocessing, there were issues due to memory errors, requiring more processing power. O.H.E of the products was the main reason for this problem. The creation of this, resulted in a matrix that was several million rows long and 50 thousand columns long, too much for a regular laptop.  Apriori requires that data is entered in as a pandas dataframe and not a compressed Numpy array. To compute the data, Google Cloud VM Instance was used to run the data through their datalabs (a notebook used for iterative programming). Although the data was able to be put into a large dataframe in the cloud, when ran in the model, the kernel would terminate due to excessive memory usage. To combat, the product data was filtered by items that had been reordered, which significantly reduced the dataframe to be run through the model. Once this was complete, a market basket for products was able to be conducted.

 After processing the market basket analysis, the recommender system was much easier to construct User ID, Order ID and Product were extracted from the original dataset. Next, the cosine similarity was imported from scikit learn, to find the relationship between users reordering pattern. To be more inclusive of finding other items, Order ID was used to captures a broader audience to find the general items among many users that are being reordered. Once the model was finished running, the data frame was then filtered by the top 3 products, to return the top 3 most likely items that similar users add to their carts.

# Results

  The market basket results show antecedents, consequences, confidence, leverage, lift, and support. Antecedents are the original item, combined with the consequences that are used to compare possible combinations of items in a given basket. Confidence, leverage, lift and support are metrics used to evaluate the relationship between items and their frequency they occur. The metrics that are of primary features of importance are confidence and lift. Confidence if between 0 and 1 that measures the amount of times that the pair shows up in the dataset. Lift can be any number from 1 to infinity: 1 being independent of each other while the higher it is, the greater the relationship between the two products. With the products, I found that majority of products bought together are health conscious consumers that primarily buy organic and low-carbohydrate options. With the market basket complete, it has helped to understand the market segmentation (_see figure 4_) and see what likely combinations of items were included in the market baskets of many users. In addition, will be used to enhance the recommender system.

 For the recommender system, the cosine similarity compares each user, to find similarity amongst users, as well as the similarity between product reorders, and then makes a recommendation based on the user ID. A function was created to allow the user ID to be input and passed through the model, and then return the top items for that user.

# Continuity

 In further investigations, to increase the value of the recommender system, an analysis will be carried out on finding common ingredients in recipes. With the recipes, I will be able to construct another dimension that will improve results by avoiding recommending items that not just popular reorders.

#
 7 Mar. 2017, [https://newfoodeconomy.org/a-reddit-user-calculated-instacarts-markup-its-pretty-high/](https://newfoodeconomy.org/a-reddit-user-calculated-instacarts-markup-its-pretty-high/). Accessed 13 Mar. 2018.
