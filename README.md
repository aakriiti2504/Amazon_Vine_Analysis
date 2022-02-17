# Amazon_Vine_Analysis

## Background

## Purpose
Since my work with Jennifer on the SellBy project was so successful, I have been tasked with another, larger project: analyzing Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

In this project, I will have access to approximately 50 datasets. Each one contains reviews of a specific product, from clothing apparel to wireless products. I will pick one of these datasets and use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Next, will use PySpark, Pandas, or SQL to determine if there is any bias toward favorable reviews from Vine members in the dataset. For this project I will be analyzing Amazon reviews for office products and determine if the members are biased or not.


## What I am creating 
This new assignment consists of two technical analysis deliverables and a written report as following:

- Deliverable 1: Perform ETL on Amazon Product Reviews
- Deliverable 2: Determine Bias of Vine Reviews
- Deliverable 3: A Written Report on the Analysis (README.md)


## Resources
- Software: Google Colab Notebook, PostgreSQL , pgAdmin 4, AWS
- AWS
    - RDS
    - S3 bucket
- Python
    - pySpark
    - Pandas
Data Source: https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt was used to get the office products source of https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Office_Products_v1_00.tsv.gz


## Results 

### 1. Deliverable 1: Perform ETL on Amazon Product Reviews - 
Using the cloud ETL process, I will create an AWS RDS database with tables in pgAdmin, pick the office products dataset from the Amazon Review datasets (https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Office_Products_v1_00.tsv.gz), and extract the dataset into a DataFrame. Then will transform the DataFrame into four separate DataFrames that match the table schema in pgAdmin. Next, will upload the transformed data into the appropriate tables and run queries in pgAdmin to confirm that the data has been uploaded.

Hence in this deliverable, 
- The Amazon  Review dataset is extracted as a DataFrame 

![5](https://user-images.githubusercontent.com/23488019/154587836-98c60a43-cf12-434f-94b0-c3e8d50c586a.PNG)

- The extracted dataset is transformed into four DataFrames with the correct columns 
![4](https://user-images.githubusercontent.com/23488019/154587855-e0667986-37ff-4cde-a645-0f27993e9cff.PNG)
![3](https://user-images.githubusercontent.com/23488019/154587866-b0dc4b6d-387c-472b-a763-67526a355c14.PNG)
![2](https://user-images.githubusercontent.com/23488019/154587872-5f4c5a0f-613a-4081-a238-d235b95afd38.PNG)
![1](https://user-images.githubusercontent.com/23488019/154587879-132b51de-7fb3-4668-bfb6-5b562dd4af9e.PNG)


- All four DataFrames are loaded into their respective tables in pgAdmin 

![666](https://user-images.githubusercontent.com/23488019/154588196-82525c1e-8372-467a-8c8b-3dccbf477d6e.PNG)


### 2. Deliverable 2 : Determine Bias of Vine Reviews - 

Using PySpark, Pandas, and SQL, we will determine if there is any bias towards reviews that were written as part of the Vine program. For this analysis, we will determine if having a paid Vine review makes a difference in the percentage of 5-star reviews. Steps followed for this deliverable are given below - 

![16](https://user-images.githubusercontent.com/23488019/154587085-6f090f79-8a2c-45a5-adae-324970a70f34.PNG)

1. Filter the data and create a new DataFrame or table to retrieve all the rows where the total_votes count is equal to or greater than 20 to pick reviews that are more likely to be helpful and to avoid having division by zero errors later on.
![15](https://user-images.githubusercontent.com/23488019/154587124-a109d88f-b029-4cf1-9494-a47cc576d459.PNG)

2. Filter the new DataFrame or table created in Step 1 and create a new DataFrame or table to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.
![14](https://user-images.githubusercontent.com/23488019/154587157-86adf9e1-ea9d-4529-a638-431a947f4371.PNG)

3. Filter the DataFrame or table created in Step 2, and create a new DataFrame or table that retrieves all the rows where a review was written as part of the Vine program (paid), vine == 'Y'.
![13](https://user-images.githubusercontent.com/23488019/154587196-d10bdcec-ccae-4979-9c59-b218be9f6043.PNG)

4. Repeat Step 3, but this time retrieve all the rows where the review was not part of the Vine program (unpaid), vine == 'N'.
![12](https://user-images.githubusercontent.com/23488019/154587212-1eb41eb5-abe7-4a02-b3ed-c64c16667383.PNG)

5. Determine the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid).
![11](https://user-images.githubusercontent.com/23488019/154587222-422057dc-2c7a-4b4e-890c-8fd07068dbc8.PNG)

##### Using PySpark
- Create a new Google Colab Notebook, and name it Vine_Review_Analysis.
- Extract the dataset used in Deliverable 1.
- Recreate the vine_table, and perform your analysis using the steps above.
- Export your Vine_Review_Analysis Google Colab Notebook as an ipynb file, and save it to your Amazon_Vine_Analysis GitHub repository.


##### Using Pandas
- From pgAdmin, export the vine_table as a CSV file, and save it to your Amazon_Vine_Analysis GitHub repository.
- Create a new Jupyter Notebook, and name it Vine_Review_Analysis.ipynb.
- Read in the vine_table.csv file as a DataFrame, and perform your analysis using the steps above.
- Save your Vine_Review_Analysis.ipynb file to your Amazon_Vine_Analysis GitHub repository.

##### Using SQL in pgAdmin
- From your AWS database, export the vine_table as a CSV file and save it to your Amazon_Vine_Analysis GitHub repository.
- In pgAdmin, create a new database that is not linked to your AWS RDS instance. This way, you don’t have to keep incurring charges while connected to your AWS RDS instance.
- Create a new SQL file and name it Vine_Review_Analysis.sql.
- Recreate the vine_table using the schema provided in the challenge_schema.sql file.
- Import the vine_table.csv file into the table, and perform your analysis using the steps above.
- Save all your SQL queries to the Vine_Review_Analysis.sql file, then add it to your Amazon_Vine_Analysis GitHub repository.

For this project I chose to use PySpark and followed the steps mentioned above. Hence it can be noted that there is a DataFrame or table for the vine_table data using one of three methods above. The data is filtered to create a DataFrame or table where there are 20 or more total votes. 
The data is filtered to create a DataFrame or table where the percentage of helpful_votes is equal to or greater than 50%, there is a Vine review and where there isn’t a Vine review. The total number of reviews, the number of 5-star reviews, and the percentage 5-star reviews are calculated for all Vine and non-Vine reviews. 

The final results can be summarized as below :

##### 1. How many Vine reviews and non-Vine reviews were there?

##### 2. How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?

##### 3. What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

## Summary
For reviews in the vine program, we can see that there is any positivity bias 
 One additional analysis is that, 
