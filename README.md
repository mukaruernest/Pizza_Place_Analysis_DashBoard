# Pizza Place Analysis DashBoard

A year's worth of sales from a fictitious pizza place.

Table of Content. 

- [Dashboard View](https://github.com/mukaruernest/Pizza_Place_Analysis_DashBoard#dashboard-view)
- [Dataset](https://github.com/mukaruernest/Pizza_Place_Analysis_DashBoard#dataset)
- [Questions](https://github.com/mukaruernest/Pizza_Place_Analysis_DashBoard#questions)
- [Solutions](https://github.com/mukaruernest/Pizza_Place_Analysis_DashBoard#solution)


## Dashboard View

![image](https://user-images.githubusercontent.com/10958742/212388005-90ed9f8e-2169-4fc9-a5d2-5bfd19f491cc.png)

[Click to Download pbix file](https://github.com/mukaruernest/Pizza_Place_Analysis_DashBoard/raw/main/PizzaPlaceSales.pbix)

## Dataset
Click the Table Name to view the tables. 

<details>
  <summary>Table Name: Orders</summary>
  
| order_details_id | order_id | pizza_id      | quantity |
|------------------|----------|---------------|----------|
| 1                | 1        | hawaiian_m    | 1        |
| 2                | 2        | classic_dlx_m | 1        |
| 3                | 2        | five_cheese_l | 1        |
| 4                | 2        | ital_supr_l   | 1        |
| 5                | 2        | mexicana_m    | 1        |
| 6                | 2        | thai_ckn_l    | 1        |
| 7                | 3        | ital_supr_m   | 1        |
| 8                | 3        | prsc_argla_l  | 1        |
| 9                | 4        | ital_supr_m   | 1        |
| 10               | 5        | ital_supr_m   | 1        |

 </details>

<details>
  <summary>Table Name: Order Details</summary>
  
| order_id | date     | time     |
|----------|----------|----------|
| 1        | 1/1/2015 | 11:38:36 |
| 2        | 1/1/2015 | 11:57:40 |
| 3        | 1/1/2015 | 12:12:28 |
| 4        | 1/1/2015 | 12:16:31 |
| 5        | 1/1/2015 | 12:21:30 |
| 6        | 1/1/2015 | 12:29:36 |
| 7        | 1/1/2015 | 12:50:37 |
| 8        | 1/1/2015 | 12:51:37 |
| 9        | 1/1/2015 | 12:52:01 |
| 10       | 1/1/2015 | 13:00:15 |
| 11       | 1/1/2015 | 13:02:59 |

  </details>
  
  <details>
  <summary>Table Name: Pizzas</summary>
  
 | pizza_id      | pizza_type_id | size | price |
|---------------|---------------|------|-------|
| bbq_ckn_s     | bbq_ckn       | S    | 12.75 |
| bbq_ckn_m     | bbq_ckn       | M    | 16.75 |
| bbq_ckn_l     | bbq_ckn       | L    | 20.75 |
| cali_ckn_s    | cali_ckn      | S    | 12.75 |
| cali_ckn_m    | cali_ckn      | M    | 16.75 |
| cali_ckn_l    | cali_ckn      | L    | 20.75 |
| ckn_alfredo_s | ckn_alfredo   | S    | 12.75 |
| ckn_alfredo_m | ckn_alfredo   | M    | 16.75 |
| ckn_alfredo_l | ckn_alfredo   | L    | 20.75 |
| ckn_pesto_s   | ckn_pesto     | S    | 12.75 | 

  </details>
  
   <details>
  <summary>Table Name: Pizza Types</summary>
  
| pizza_type_id | name                         | category |
|---------------|------------------------------|----------|
| bbq_ckn       | The Barbecue Chicken Pizza   | Chicken  |
| cali_ckn      | The California Chicken Pizza | Chicken  |
| ckn_alfredo   | The Chicken Alfredo Pizza    | Chicken  |
| ckn_pesto     | The Chicken Pesto Pizza      | Chicken  |
| southw_ckn    | The Southwest Chicken Pizza  | Chicken  |
| thai_ckn      | The Thai Chicken Pizza       | Chicken  |
| big_meat      | The Big Meat Pizza           | Classic  |
| classic_dlx   | The Classic Deluxe Pizza     | Classic  |
| hawaiian      | The Hawaiian Pizza           | Classic  |
| ital_cpcllo   | The Italian Capocollo Pizza  | Classic  |

  </details>
 
  <details>
  <summary>Table Name: Revenue </summary>
  This is a claculate Table;
  
  ```SQL
  Revenue = GROUPBY(orders,orders[date],"MonthSales",SUMX(CURRENTGROUP(),SUM(pizzas[price])))
  ```
  
   </details>
 
## Relationships

 There is a One to Many relationship between;
- `order_details` and `pizzas` using `pizza_id`
- `order_details` and `orders` using `order_id`
- `pizzas` and `pizza_types` using `pizza_type_id`
-- `Revenue` and `orders` using `date`

![image](https://user-images.githubusercontent.com/10958742/212383939-f1f0fd45-f624-4b72-9b53-fca633a4d668.png)

  ## Questions 
  
1)	Are there any peak hours?
2)	How many pizzas are typically in an order? Do we have any bestsellers?
3)	How much money did we make this year? Can we indentify any seasonality in the sales?
4) Do we have any bestsellers?
5)	Are there any pizzas we should take of the menu, or any promotions we could leverage?

## Solution.

Q1) Are there any peak hours?

*There is a spike of orders from around mid day (12noon to 1pm and also in the evening)*

*Visual: `Line Graph`*


![image](https://user-images.githubusercontent.com/10958742/212387421-eddaa240-92d9-412f-831a-7f8b6aa503f5.png)


Q2) How many pizzas are typically in an order? 

*There is average of One pizza per order. This is calculated by getting the sun of all pizza ordered / Number of orders.*

*calculation with DAX:* 
```SQL
averageNumberPizzas = COUNT(order_details[pizza_id])/COUNT(order_details[order_id])
```

*Visual: `Card`

![image](https://user-images.githubusercontent.com/10958742/212387215-8aff2d2f-484c-4786-bf80-679245d576ed.png)

Q3) Do we have any bestsellers?

*The best selling pizza is The Classic Deluxe Pizza.*

*visual: `Table`*

![image](https://user-images.githubusercontent.com/10958742/212389595-f6fc1f3e-ad9b-4f2c-a8d8-5174f737fc5b.png)


Q4) How much money did we make this year? Can we indentify any seasonality in the sales?

*The higher the number of orders the high the revenue*

*Visual: `Staked Column Chart`* 

![image](https://user-images.githubusercontent.com/10958742/212387052-227a4759-16cb-4305-9b5e-17f826775e8f.png)

-Number of Orders per Month

![image](https://user-images.githubusercontent.com/10958742/212390040-6a8e358a-1ebc-464c-9204-3f8cf3f6ede3.png)

Q5) Are there any pizzas we should take of the menu, or any promotions we could leverage?

*I would suggest taking off Pizzas with less that 500 orders through the year.*

*For the ones the shop received less than 1000 orders, there should be a promotion strategy.*




