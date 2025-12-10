# Data Analyst Project: Logistics Analysis

Welcome to the **Employee Retention & Attrition** repository! This project explores data-driven solutions to key business challenges in [Logistics]. Follow along as we uncover insights and deliver actionable recommendations.

---

## Table of Contents

- [Background & Business Problem](#background--business-problem)
- [Project Objectives](#project-objectives)
- [Data Collection & Understanding](#data-collection--understanding)
- [Data Cleaning & Preprocessing & Modeling](#data-cleaning--preprocessing--modeling)
- [Initial Exploratory Data Analysis](#initial-exploratory-data-analysis)
- [Main Insights](#main-insights)
- [Solutions & Recommendations](#solutions--recommendations)
- [Summary](#summary)
- [How to Reproduce](#how-to-reproduce)

---

## Background & Business Problem

The Brazilian e-commerce sector, as exemplified by Olist’s marketplace, operates in a dynamic yet challenging environment where maximizing growth and profitability requires overcoming significant operational and customer-centric hurdles. Despite strong gross merchandise volumes and a broad customer base, Olist faces persistent business problems related to cost management, customer retention, service reliability, and revenue leakage. These challenges manifest as high order cancellation rates, substantial logistics costs, uneven customer satisfaction, and low repeat purchase rates. Addressing these core business issues is critical for driving sustainable growth, enhancing profitability, and solidifying Olist’s competitive position in the rapidly evolving e-commerce landscape.

## Project Objectives

- Increase Customer Retention: Identify key drivers of customer churn and develop targeted strategies to boost repeat purchase rates and customer lifetime value.
- Reduce Revenue Loss from Cancellations: Analyze the root causes of high order cancellation rates and implement measures to minimize lost revenue, especially in high-impact regions.
- Optimize Logistics and Delivery Performance: Streamline the delivery process to decrease late shipments, enhance customer satisfaction, and improve Net Promoter Scores.
- Improve Profitability: Assess freight and operational costs relative to product categories and payment types, and devise cost-control strategies to maximize profit margins.
- Enhance Customer Satisfaction: Pinpoint pain points in the customer journey across different product lines and geographies, and take targeted actions to raise overall review scores and reduce detractor rates.
- Support Data-Driven Decision Making: Leverage data insights to inform business strategy, product assortment, and marketing initiatives.

## Data Collection & Understanding

| file | type |
| ------- | ----------- |
| olist_customers_dataset | .csv |
| olist_geolocation_dataset | .csv |
| olist_order_items_dataset | .csv |
| olist_order_payments_dataset | .csv |
| olist_order_reviews_dataset | .csv |
| olist_orders_dataset | .csv |
| olist_products_dataset | .csv |
| olist_sellers_dataset | .csv |
| product_category_name_translation | .csv |

olist_customers_dataset Table Columns

| columnName | Description |
| -----------| ------------|
| customer_id	| customer id|
| customer_unique_id	| purpose of having a customer_unique_id on the dataset is to allow you to identify customers that made repurchases at the store|
| customer_zip_code_prefix | zip code of customer location|	
| customer_city	 | city where the customer lives |
| customer_state | state where the customer lives |



olist_geolocation_dataset Table Columns

| columnName | Description |
| -----------| ------------|
| geolocation_zip_code_prefix	| location zip code |
| geolocation_lat	 | location latitude |
| geolocation_lng	 | location longitude |
| geolocation_city	| corresponding location city |
| geolocation_state | corresponding location state |



olist_order_items_dataset Table Columns

| columnName | Description |
| -----------| ------------|
| order_id	 | order unique identifier |
| order_item_id	| item id in the order |
| product_id	| product id |
| seller_id	| seller id |
| shipping_limit_date	| limit date for shipping the product |
| price	| product price |
| freight_value | product freight cost |



olist_order_payments_dataset Table Columns

| columnName | Description |
| -----------| ------------|
| order_id	 | order identifier |
| payment_sequential	| a customer may pay an order with more than one payment method. If he does so, a sequence will be created |
| payment_type	| type of the payment method (e.g. credit) |
| payment_installments	| number of installments chosen by the customer | 
| payment_value | overall payment value |



olist_order_reviews_dataset Table Columns

| columnName | Description |
| -----------| ------------|
| review_id	| unique review identifier |
| order_id	| unique review identifier |
| review_score	| Note ranging from 1 to 5 given by the customer on a satisfaction survey. |
| review_comment_title	| Comment title from the review left by the customer, in Portuguese. |
| review_comment_message	| Comment message from the review left by the customer, in Portuguese. |
| review_creation_date	 | the date review was created |
| review_answer_timestamp | Shows satisfaction survey answer timestamp. |


olist_orders_dataset Table Columns 

| columnName | Description |
| -----------| ------------|
| order_id	 | unique order identifier |
| customer_id	| customer identifier |
| order_status	| Reference to the order status (delivered, shipped, etc). |
| order_purchase_timestamp	| the date the customer purchased the order |
| order_approved_at	  | Shows the payment approval timestamp. |
| order_delivered_carrier_date	| Shows the order posting timestamp. When it was handled to the logistic partner. |
| order_delivered_customer_date	 | Shows the actual order delivery date to the customer. |
| order_estimated_delivery_date  | Shows the estimated delivery date that was informed to customer at the purchase moment. |

olist_products_dataset Table Columns 

| columnName | Description |
| -----------| ------------|
| product_id	| product unique identifier |
| product_category_name	| product category |
| product_name_lenght	 | number of characters extracted from the product name. |
| product_description_lenght	| number of characters extracted from the product description. |
| product_photos_qty	| number of product published photos |
| product_weight_g	| product weight measured in grams. |
| product_length_cm	 | product length measured in centimeters. |
| product_height_cm	 | product height measured in centimeters. |
| product_width_cm   | product width measured in centimeters. |


olist_sellers_dataset Table Columns 

| columnName | Description |
| -----------| ------------|
| seller_id	 | seller unique identifier |
| seller_zip_code_prefix	| first 5 digits of seller zip code |
| seller_city	 | seller city name  |
| seller_state | seller state |




## Data Cleaning & Preprocessing & Modeling 

Data Cleaning

- Dim_Products: removing duplicates and replacing null values in product name english with "Other" word and for photo quantity column replacing null with zeros 
- Fact_order_line_items: deriving columns from some date columns and changing the data type of them to only include date & removed duplicates

Data Modeling:

- The data was upload to google Big Query to make the data model you will find the sql queries for building the data model in model.sql
- Notice how the data model follows the galaxy schema (>1 fact table) that is for the elimination of many-to-many relationship

  <img width="923" height="709" alt="datamodel" src="https://github.com/user-attachments/assets/8877f763-491a-413a-a4bc-5a641615d91b" />

## Sample Report:

https://github.com/user-attachments/assets/b96fbe51-0482-4603-87d1-cbf42591b222


---------------------------------------------------------------------------------------------

## Initial Exploratory Data Analysis


1. Order & Revenue Patterns
   
  - Gross Merchandise Volume (GMV):
      Total GMV of delivered orders is R$15.49M.
      GMV is distributed across Brazil but is concentrated in certain states.
      Most revenue comes from credit card payments (about 78% of GMV), with boleto and voucher accounting for the rest.

  - Average Order Value (AOV):
      Highest AOVs are seen for categories like computers and for "high" price segments.
      Considerable variation in AOV across product categories and geographic regions.
    
2. Cost, Margins & Profitability
   
  - Freight Cost:
      Freight to GMV ratio averages 14.27%; certain categories like "home_comfort_2" have ratios exceeding 50%.
      Cost efficiency fluctuates by product and weight, with heavier/larger items showing less favorable ratios.
    
3. Cancellations & Wasted Revenue

  - Order Cancellations:
      Revenue loss due to cancellations is R$106.54K.
      Cancellations are disproportionately high in some states, with São Paulo leading by a wide margin.
      Product categories and regions both influence cancellation rates.
    
4. Customer Satisfaction (CSAT) & NPS

  - Review Scores:
      The average customer review score is 4.08 out of 5, based on 111K reviews.
      Net Promoter Score (NPS) stands at 42.44, but is much lower for late deliveries.
      Detractor rates are highest in categories like "security_and_services" (over 40%) and specific states (e.g., Amazonas).
      Delivery timeliness strongly impacts satisfaction; late deliveries lead to negative NPS.
    
5. Customer Retention & Value
   
  - Repeat Purchase Behavior:
      Repeat purchase rate is low at 3%, with only about 3K repeat buyers from 93K customers.
      CLV (Customer Lifetime Value) is R$139.75.
      Repeat purchase rates are higher among promoters, lower for detractors and those experiencing late delivery.

6. Regional and Product Variation
   
  - Geographical Trends:
      There are pronounced differences across Brazilian states in GMV, CLV, cancellation rates, and satisfaction.
      Both customer and seller states influence performance metrics.

------------------------------------------------------------------------------------------------

## Main Insights

Revenue & Order Metrics

  - Delivered orders have a GMV of R$15.49M, with average order value (AOV) highest in the “high” price segment and for “computers”.
  - There’s a clear spike in GMV over time, but also volatility in some periods.
    
Cost & Profitability

  - Several product categories have freight-to-price ratios exceeding 40-50%, which can undermine profitability.
  - Cost control on freight, especially for bulky or low-margin goods, is a recurring issue.
    
Wasted Revenue

  - The majority of wasted revenue due to cancellations is concentrated in a few states.
  - Cancellations correlate with both product categories and customer locations.
    
Customer Satisfaction

  - The average review score is 4.08, yet NPS is heavily affected by delivery delays.
  - Payment type does not strongly affect review scores, but certain product categories and seller states suffer higher detractor rates.
    
Retention & Value

  - Repeat rates are lowest among detractors and those experiencing delivery issues.
  - Promoters (customers with high review scores) have much higher repeat rates, suggesting satisfaction is crucial for retention.

## Solutions & Recommendations

a. Improve Delivery Reliability
  - Prioritize investments in logistics and carrier partnerships to reduce late deliveries, especially in states with high cancellation or detractor rates.
  - Implement predictive delivery time analytics to flag at-risk orders and proactively communicate with customers.
    
b. Optimize Freight & Product Mix
  - Analyze high freight-to-price ratio categories (e.g., home_comfort_2, flowers) for packaging, logistics optimization, or reconsideration in the assortment.
  - Consider differentiated shipping fees, minimum order values, or bundling for low-margin or high-freight categories.
    
c. Customer Segmentation & Loyalty Programs
  - Develop targeted campaigns for regions with low CLV and high detractor rates.
  - Create loyalty incentives focused on promoters to boost repeat purchases and customer lifetime value.
  - Implement post-purchase engagement for customers with satisfactory delivery experiences.
    
d. Reduce Cancellations Through Order Experience
  - Audit and address causes for cancellations in São Paulo and other high-loss states.
  - Use follow-up surveys to gather specific feedback and improve policies or product offerings.
    
e. Enhance Communication & Transparency
  - Provide accurate order tracking and delivery estimates to manage customer expectations.
  - Proactively notify customers about delays and offer compensation or alternatives if late delivery is anticipated.
    
f. Product Category Strategies
  - For categories with high detractor percentages, analyze root causes (e.g., product quality, description accuracy, post-delivery support) and implement improvements.
  - Review seller states with high detractor rates (e.g., Amazonas, Rondônia) for local supply chain or seller training needs.
    
g. Payment Optimization
  - Maintain and expand card payment options as they dominate GMV.
  - For other payment methods, ensure seamless experience to maintain customer satisfaction parity.

--------------------------------------------------------------------------------------

## Summary

 Olist’s e-commerce business, based on the Power BI dashboards, should focus on logistics improvements, cost controls, cancellation reduction, and customer satisfaction enhancements to drive higher repeat rates, reduce wasted revenue, and boost customer lifetime value.

 -----------------------------------------------------------------------------------------------------------
## How to Reproduce

Step-by-step instructions for running the analysis:
1. [Download dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce?select=olist_sellers_dataset.csv)
2. Open your bi tool
3. feel free to refer to data model to reproduce

