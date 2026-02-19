##### ***Customer Churn Analysis – SQL Project***

***This project analyzes customer churn using SQL***





**Step 1: Create Database**

CREATE DATABASE churn\_analysis;



**Step 2: Use Database**

USE churn\_analysis;



**Step 3: Create Table**

CREATE TABLE customers (customer\_id INT PRIMARY KEY,name VARCHAR(100),age INT,gender VARCHAR(10),city VARCHAR(50),subscription\_type VARCHAR(50),monthly\_charges DECIMAL(10,2),churn\_status VARCHAR(10));



**Step 4: Inserts sample data into table**



**Step 5: View All Data**

SELECT \* FROM customers;



**Step 6: Count Total Customers**

&nbsp;select count(\*) AS total\_customers from customers;

+-----------------+

| total\_customers |

+-----------------+

|             200 |

+-----------------+

***To know: How many total customers company has.***



**Step 7: Check Churn Distribution**

&nbsp;SELECT Churn, COUNT(\*) AS total FROM customers GROUP BY Churn;

+-------+-------+

| Churn | total |

+-------+-------+

| No    |    90 |

| Yes   |   110 |

+-------+-------+

***To see: Count how many customers churned and not churned***



**Step 8: Calculate Churn Rate**

&nbsp;SELECT COUNT(\*) AS total\_customers,SUM(CASE WHEN Churn='Yes' THEN 1 ELSE 0 END) AS churned\_customers,ROUND

(SUM(CASE WHEN Churn='Yes' THEN 1 ELSE 0 END)\*100/COUNT(\*),2) AS churn\_rate\_percentage FROM customers;

+-----------------+-------------------+-----------------------+

| total\_customers | churned\_customers | churn\_rate\_percentage |

+-----------------+-------------------+-----------------------+

|             200 |               110 |                 55.00 |

+-----------------+-------------------+-----------------------+

***To calculate: What percentage of customers left?***



**Step 9: Contract-wise Churn**

&nbsp;SELECT Contract,COUNT(\*) AS total\_customers,

&nbsp;   -> SUM(CASE WHEN Churn='Yes' THEN 1 ELSE 0 END) AS churned,

&nbsp;   -> ROUND(SUM(CASE WHEN Churn='Yes' THEN 1 ELSE 0 END)\*100/COUNT(\*),2) AS churn\_rate FROM customers GROUP BY Contract

&nbsp;   -> ORDER BY churn\_rate DESC;

+----------------+-----------------+---------+------------+

| Contract       | total\_customers | churned | churn\_rate |

+----------------+-----------------+---------+------------+

| Two year       |              68 |      45 |      66.18 |

| One year       |              61 |      32 |      52.46 |

| Month-to-month |              71 |      33 |      46.48 |

+----------------+-----------------+---------+------------+

***To find: Which contract type has highest churn?***



**Step 10: Tenure Group Analysis**

&nbsp;SELECT CASE WHEN tenure <= 12 THEN '0-1 Year' WHEN tenure <= 24 THEN '1-2 Years' ELSE '2+ Years' END AS tenure\_group,

&nbsp;   -> COUNT(\*) AS total, SUM(CASE WHEN Churn='Yes' THEN 1 ELSE 0 END) AS churned,

&nbsp;   -> ROUND(SUM(CASE WHEN Churn='Yes' THEN 1 ELSE 0 END)\*100/COUNT(\*),2) AS churn\_rate FROM customers

&nbsp;   -> GROUP BY tenure\_group ORDER BY churn\_rate DESC;

+--------------+-------+---------+------------+

| tenure\_group | total | churned | churn\_rate |

+--------------+-------+---------+------------+

| 0-1 Year     |    34 |      20 |      58.82 |

| 2+ Years     |   130 |      72 |      55.38 |

| 1-2 Years    |    36 |      18 |      50.00 |

+--------------+-------+---------+------------+  

***To understand: Do new customers leave more?***



**Step 11: Monthly Charges Comparison**

&nbsp;SELECT Churn, ROUND(AVG(MonthlyCharges),2) AS avg\_monthly\_charge

&nbsp;   -> FROM customers GROUP BY Churn;

+-------+--------------------+

| Churn | avg\_monthly\_charge |

+-------+--------------------+

| No    |              73.13 |

| Yes   |              71.09 |

+-------+--------------------+

***To check: Are high paying customers leaving more?***



**Step 12: Window Function**

&nbsp;SELECT customerID, MonthlyCharges, RANK() OVER (ORDER BY MonthlyCharges DESC) AS rank\_highest FROM customers;

+------------+----------------+--------------+

| customerID | MonthlyCharges | rank\_highest |

+------------+----------------+--------------+

| CUST0193   |         119.53 |            1 |

| CUST0059   |         119.06 |            2 |

| CUST0105   |         118.45 |            3 |

| CUST0101   |         117.95 |            4 |

| CUST0072   |         117.71 |            5 |

| CUST0132   |         116.46 |            6 |

| CUST0166   |         116.42 |            7 |

| CUST0165   |         115.29 |            8 |

| CUST0189   |         114.69 |            9 |

| CUST0131   |         114.52 |           10 |

| CUST0003   |         113.98 |           11 |

| CUST0183   |         113.60 |           12 |

| CUST0158   |         112.62 |           13 |

| CUST0134   |         112.13 |           14 |

| CUST0160   |         111.79 |           15 |

| CUST0186   |         111.55 |           16 |

| CUST0020   |         110.36 |           17 |

| CUST0083   |         110.13 |           18 |

| CUST0145   |         109.29 |           19 |

| CUST0078   |         108.92 |           20 |

| CUST0119   |         108.75 |           21 |

| CUST0061   |         108.36 |           22 |

| CUST0048   |         108.14 |           23 |

| CUST0129   |         107.88 |           24 |

| CUST0013   |         106.40 |           25 |

| CUST0040   |         106.21 |           26 |

| CUST0187   |         106.06 |           27 |

| CUST0113   |         106.04 |           28 |

| CUST0018   |         105.27 |           29 |

| CUST0085   |         104.86 |           30 |

| CUST0002   |         104.82 |           31 |

| CUST0071   |         104.53 |           32 |

| CUST0149   |         103.89 |           33 |

| CUST0106   |         103.75 |           34 |

| CUST0084   |         103.09 |           35 |

| CUST0191   |         103.02 |           36 |

| CUST0159   |         102.27 |           37 |

| CUST0115   |         102.17 |           38 |

| CUST0064   |         102.12 |           39 |

| CUST0142   |         102.04 |           40 |

| CUST0097   |         101.60 |           41 |

| CUST0151   |         101.52 |           42 |

| CUST0198   |         101.10 |           43 |

| CUST0089   |         100.65 |           44 |

| CUST0176   |         100.57 |           45 |

| CUST0056   |         100.40 |           46 |

| CUST0001   |         100.34 |           47 |

| CUST0194   |         100.06 |           48 |

| CUST0102   |          99.73 |           49 |

| CUST0128   |          99.70 |           50 |

| CUST0164   |          99.42 |           51 |

| CUST0036   |          98.63 |           52 |

| CUST0188   |          98.25 |           53 |

| CUST0028   |          97.32 |           54 |

| CUST0185   |          97.15 |           55 |

| CUST0169   |          95.87 |           56 |

| CUST0082   |          95.60 |           57 |

| CUST0014   |          95.34 |           58 |

| CUST0004   |          94.86 |           59 |

| CUST0098   |          92.39 |           60 |

| CUST0178   |          91.47 |           61 |

| CUST0088   |          91.21 |           62 |

| CUST0161   |          90.55 |           63 |

| CUST0172   |          89.89 |           64 |

| CUST0184   |          89.53 |           65 |

| CUST0073   |          89.44 |           66 |

| CUST0110   |          88.30 |           67 |

| CUST0075   |          88.29 |           68 |

| CUST0086   |          87.82 |           69 |

| CUST0124   |          87.25 |           70 |

| CUST0087   |          85.51 |           71 |

| CUST0182   |          85.17 |           72 |

| CUST0103   |          84.96 |           73 |

| CUST0118   |          84.41 |           74 |

| CUST0042   |          83.75 |           75 |

| CUST0157   |          83.00 |           76 |

| CUST0008   |          82.69 |           77 |

| CUST0141   |          82.63 |           78 |

| CUST0005   |          82.11 |           79 |

| CUST0192   |          81.90 |           80 |

| CUST0012   |          79.92 |           81 |

| CUST0171   |          79.40 |           82 |

| CUST0162   |          79.24 |           83 |

| CUST0041   |          78.72 |           84 |

| CUST0065   |          78.16 |           85 |

| CUST0199   |          77.38 |           86 |

| CUST0035   |          77.04 |           87 |

| CUST0051   |          76.90 |           88 |

| CUST0137   |          76.40 |           89 |

| CUST0140   |          75.51 |           90 |

| CUST0146   |          75.18 |           91 |

| CUST0080   |          74.00 |           92 |

| CUST0104   |          73.84 |           93 |

| CUST0016   |          73.46 |           94 |

| CUST0069   |          73.41 |           95 |

| CUST0052   |          72.98 |           96 |

| CUST0063   |          72.88 |           97 |

| CUST0031   |          72.39 |           98 |

| CUST0090   |          72.23 |           99 |

| CUST0023   |          71.99 |          100 |

| CUST0032   |          71.75 |          101 |

| CUST0034   |          71.74 |          102 |

| CUST0044   |          71.40 |          103 |

| CUST0174   |          70.93 |          104 |

| CUST0114   |          70.92 |          105 |

| CUST0197   |          70.55 |          106 |

| CUST0173   |          70.51 |          107 |

| CUST0126   |          69.93 |          108 |

| CUST0167   |          69.55 |          109 |

| CUST0117   |          68.85 |          110 |

| CUST0196   |          68.69 |          111 |

| CUST0068   |          66.11 |          112 |

| CUST0108   |          65.93 |          113 |

| CUST0092   |          65.23 |          114 |

| CUST0139   |          64.64 |          115 |

| CUST0177   |          64.62 |          116 |

| CUST0179   |          64.11 |          117 |

| CUST0136   |          63.97 |          118 |

| CUST0143   |          63.87 |          119 |

| CUST0030   |          63.21 |          120 |

| CUST0190   |          62.60 |          121 |

| CUST0127   |          62.58 |          122 |

| CUST0094   |          62.01 |          123 |

| CUST0125   |          61.66 |          124 |

| CUST0025   |          61.42 |          125 |

| CUST0181   |          61.16 |          126 |

| CUST0017   |          60.90 |          127 |

| CUST0054   |          60.00 |          128 |

| CUST0148   |          59.68 |          129 |

| CUST0135   |          58.39 |          130 |

| CUST0067   |          58.02 |          131 |

| CUST0168   |          57.26 |          132 |

| CUST0015   |          56.99 |          133 |

| CUST0039   |          56.72 |          134 |

| CUST0045   |          56.51 |          135 |

| CUST0021   |          56.27 |          136 |

| CUST0019   |          55.99 |          137 |

| CUST0027   |          55.42 |          138 |

| CUST0066   |          54.66 |          139 |

| CUST0076   |          54.27 |          140 |

| CUST0156   |          53.72 |          141 |

| CUST0091   |          53.61 |          142 |

| CUST0100   |          53.21 |          143 |

| CUST0010   |          52.56 |          144 |

| CUST0070   |          52.18 |          145 |

| CUST0133   |          52.17 |          146 |

| CUST0200   |          51.89 |          147 |

| CUST0195   |          51.13 |          148 |

| CUST0147   |          50.79 |          149 |

| CUST0093   |          50.07 |          150 |

| CUST0096   |          50.03 |          151 |

| CUST0121   |          50.01 |          152 |

| CUST0144   |          48.94 |          153 |

| CUST0074   |          48.48 |          154 |

| CUST0033   |          47.13 |          155 |

| CUST0095   |          47.04 |          156 |

| CUST0170   |          46.84 |          157 |

| CUST0060   |          44.53 |          158 |

| CUST0049   |          44.42 |          159 |

| CUST0155   |          43.59 |          160 |

| CUST0043   |          43.55 |          161 |

| CUST0029   |          43.49 |          162 |

| CUST0107   |          43.35 |          163 |

| CUST0122   |          43.34 |          164 |

| CUST0112   |          43.23 |          165 |

| CUST0109   |          42.78 |          166 |

| CUST0011   |          42.08 |          167 |

| CUST0038   |          41.45 |          168 |

| CUST0047   |          40.56 |          169 |

| CUST0153   |          39.03 |          170 |

| CUST0024   |          38.67 |          171 |

| CUST0099   |          37.03 |          172 |

| CUST0007   |          36.57 |          173 |

| CUST0116   |          36.23 |          174 |

| CUST0180   |          35.26 |          175 |

| CUST0175   |          34.08 |          176 |

| CUST0009   |          33.03 |          177 |

| CUST0026   |          32.61 |          178 |

| CUST0152   |          32.20 |          179 |

| CUST0046   |          30.64 |          180 |

| CUST0062   |          30.24 |          181 |

| CUST0154   |          30.14 |          182 |

| CUST0058   |          29.95 |          183 |

| CUST0081   |          29.76 |          184 |

| CUST0057   |          29.64 |          185 |

| CUST0120   |          28.65 |          186 |

| CUST0150   |          28.26 |          187 |

| CUST0053   |          27.91 |          188 |

| CUST0077   |          27.38 |          189 |

| CUST0079   |          26.60 |          190 |

| CUST0050   |          26.32 |          191 |

| CUST0123   |          25.80 |          192 |

| CUST0111   |          24.82 |          193 |

| CUST0130   |          24.33 |          194 |

| CUST0138   |          21.69 |          195 |

| CUST0037   |          21.29 |          196 |

| CUST0163   |          21.23 |          197 |

| CUST0055   |          20.43 |          198 |

| CUST0006   |          20.39 |          199 |

| CUST0022   |          20.08 |          200 |

+------------+----------------+--------------+

***To Check: Identify top revenue customers***



**Step 13: Identify High Risk Customers**

&nbsp;SELECT \*FROM customers WHERE Contract = 'Month-to-month'AND tenure < 12 AND MonthlyCharges > 80 AND Churn = 'Yes';

+------------+--------+---------------+--------+----------------+--------------+----------------+------------------+-------+

| customerID | gender | SeniorCitizen | tenure | MonthlyCharges | TotalCharges | Contract       | PaymentMethod    | Churn |

+------------+--------+---------------+--------+----------------+--------------+----------------+------------------+-------+

| CUST0013   | Female |             0 |      1 |         106.40 |       106.40 | Month-to-month | Mailed check     | Yes   |

| CUST0164   | Female |             0 |      2 |          99.42 |       198.84 | Month-to-month | Mailed check     | Yes   |

| CUST0182   | Male   |             1 |      5 |          85.17 |       425.85 | Month-to-month | Electronic check | Yes   |

+------------+--------+---------------+--------+----------------+--------------+----------------+------------------+-------+

***To identify: High-risk churn pattern***







