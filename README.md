# Fetch-Rewards_Data-Analytics-Internship-Task
Task to be done as per Fetch Rewards Data Analytics Internship Take Home Exercise

## <B> TASK 1: Review Existing Data and Diagram a New Structured Relational Data Model </B>
![FETCH](https://user-images.githubusercontent.com/56999854/216743660-1a6a539b-5a34-4d8d-9f6f-1f3c76e716e5.png)


The reason for choosing BRAND_CODE as the column for joining Brands and Receipt_Items is that it fetches more results in the ensuing combined table.


## <B> Task 2: Write a query that directly answers question(s) from a business stakeholder </B>

### 1. Which brand saw the most dollars spent in the month of June?
```
SELECT B.NAME
FROM Brands B JOIN receipt_items Ri ON (B.BRAND_CODE= Ri.BRAND_CODE) JOIN Receipts as R ON (Ri.REWARDS_RECEIPT_ID = R.ID)
WHERE SUBSTR(R.PURCHASE_DATE, 6, 2) LIKE "06"
GROUP BY B.NAME
ORDER BY SUM(Ri.TOTAL_FINAL_PRICE) DESC LIMIT 1;
```
### 2. Which user spent the most money in the month of August?
```
SELECT U.ID
FROM Users as U JOIN Receipts as R ON (U.ID = R.USER_ID)
WHERE SUBSTR(R.PURCHASE_DATE, 6, 2) LIKE "08"
GROUP BY U.ID
ORDER BY SUM(R.TOTAL_SPENT)  DESC LIMIT 1;
```

### 3. What user bought the most expensive item?
```
SELECT U.ID
FROM (Users as U JOIN Receipts as R ON (U.ID = R.USER_ID)) JOIN Receipt_items as Ri ON (R.ID = Ri.REWARDS_RECEIPT_ID)
ORDER BY Ri.TOTAL_FINAL_PRICE/Ri.QUANTITY_PURCHASED DESC LIMIT 1;
```

### 4. What is the name of the most expensive item purchased?
```
SELECT DESCRIPTION
FROM Receipt_items
ORDER BY TOTAL_FINAL_PRICE/QUANTITY_PURCHASED DESC LIMIT 1;
```

### 5. How many users scanned in each month?
```
SELECT SUBSTR(R.DATE_SCANNED, 6, 2), COUNT( DISTINCT r.USER_ID) 
FROM Receipts r 
GROUP BY SUBSTR(R.DATE_SCANNED, 6, 2)
```

## Task 3: Choose something noteworthy about the data and share with a non-technical stakeholder

### Findings: To gain some insighful observations from the data, I created a Tableau dashboard and with the help of the visualisations I was able to notice the following:
 
#### 1. The first visualisation shows the distribution of users in different categories and the spending in each category. The distribution of users among the categories is fairly distributed, but the spending among the categories is very heavily skewed towards the category of beverages, about 45% of spendings go towards beverages while the category of beauty products has negligible spending in comparison . This graph shows the potential of the categories and can help in terms of marketing and generating new users

![image](https://user-images.githubusercontent.com/56999854/216748484-1f329443-f2da-4118-bd6f-e10ec1d440cf.png)

#### 2. This visualisation shows the spending of users in each state. Using a geographical visualisation shows us that states like New York, Wisconsin and Kentucky have higher average spending per user but when total spending is taken into consideration New York, California, Florida and South Carolina. This data shows the potential of various states where effort can be put into getting more users, or offering better incentives to increase average spending of the users.

![image](https://user-images.githubusercontent.com/56999854/216753837-0ab42f7a-58fe-45f4-a775-7d2dde695d16.png)
![image](https://user-images.githubusercontent.com/56999854/216753899-3b28cd3b-9826-45de-8727-71bcbda4234f.png)
