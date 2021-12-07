# 資料庫管理 作業二
## B08705008 資管三 祝浩文
### 1.
#### (a)
The time spent running ten queries is listed below. (Unit: ms)
* 133.871
* 134.289
* 132.082
* 147.970
* 133.204
* 131.815
* 160.276
* 148.040
* 149.411
* 144.544
Average: 141.550, Std: 9.834
#### (b)
I created two indices using the following sql commands.
```sql
CREATE index sales_date ON Sales(salesdate);
CREATE index sales_memberid ON Sales(memberid);
```
The time spent running the ten queries is listed below. (Unit: ms)
* 225.181
* 201.341
* 195.728
* 199.990
* 201.458
* 202.637
* 197.486
* 189.945
* 188.864
* 189.102

Average: 199.1732, Std: 10.57552099

#### \(c\)
I created a multi-column index using the sql command below.
```sql
CREATE index sales_data_memberid ON sales(salesdate, memberid);
```
The time spent running ten queries is listed below. (Unit: ms)
* 35.785
* 24.653
* 22.308
* 23.362
* 23.550
* 23.705
* 23.511
* 21.392
* 23.932
* 23.950

Average: 24.6148, Std: 4.029615168
#### (d)
The effect of multiple single-column index and multi-column index depends on the query itself. In this case, we can see that multi-column indexing is more effective, with better speed and less deviation.

### 2.
#### (a)
![](https://i.imgur.com/ldivVpS.png)
#### (b)
Before we insert 35, the tree looks like this.
![](https://i.imgur.com/wgAo6EF.png)
We would wnat to insert 35 between 32 and 43, however there is no space left in that node. 
![](https://i.imgur.com/jxU7kxR.png)
Therefore we have to split the node. The node is split into two and 42 is copied upwards.
![](https://i.imgur.com/SsFm7Vf.png)
Now the root node is full, we would have to split it too. 68 is moved upwards to the root.
![](https://i.imgur.com/ER7MQJg.png)
#### \(c\)
Before the insertion of 9, the tree looks like this.
![](https://i.imgur.com/5JcLBhz.png)
We simply traverse down the tree to find that 9 belongs the left most node. There is still enough space in the node, no splitting is required.
![](https://i.imgur.com/ldivVpS.png)

   
### 3.
Using table from PDOGS, schema and row count is shown below.
 
 
![](https://i.imgur.com/VqTTiiU.png)
![](https://i.imgur.com/3swijMT.png)


I choose the query:
```sql
SELECT * FROM access_log WHERE account_id = 1923 LIMIT 10000;
```

Which is used when the admin account of PDOGS wants to look for the latest 10000 occurrences of the account with id 1923(which is my account).

The time spent running ten queries is listed below. (Unit: ms)
* 44.899
* 304.938
* 762.545
* 488.008
* 640.843
* 79.3811
* 114.422
* 252.437
* 260.573
* 621.269

Average: 356.93151, Std: 255.6690922


Then I created a index on the account_id.
```sql
CREATE index access_log_account_id ON access_log(account_id);
```
The time spent running ten queries is listed below. (Unit: ms)
* 2.934
* 2.986
* 2.912
* 2.949
* 3.942
* 2.862
* 2.950
* 2.892
* 3.177
* 3.099

Average: 3.0703, Std: 0.320966959

We can see that indexing made a huge difference on performance. The query is now about a 100 times faster than before, with a much smaller deviation.