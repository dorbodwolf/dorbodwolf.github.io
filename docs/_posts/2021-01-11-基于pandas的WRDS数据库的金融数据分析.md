# AcF 351b Career Skills in Accounting and Finance
## Python for Data Analysis
### Stream Assignment Part 1

给定美国债券市场部分英美企业债券发行的信息，通过下载分析WRDS数据库的金融和账务数据，评估英国脱欧对公司债券价格的影响。

#### 💲1. Download and process bond fields data


The bond yield data are downloaded from TRACE on WRDS using WRDS web. 

The downloaded file is saved as 'e792b11838182376.csv'.

Now process the data in the file...


```python
import pandas as pd
```


```python
# check pandas version
print(pd.__version__)
```

    1.1.3



```python
# read csv as pandas dataframe
trace_on_wrds = '../data/e792b11838182376.csv'
yields = pd.read_csv(trace_on_wrds, usecols=[0, 3, 4, 5], parse_dates=[1])
```


```python
# show dataframe
yields
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>7:57:03</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:29:00</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:29:00</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:34:48</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:37:44</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1326280</th>
      <td>984121CK7</td>
      <td>2017-12-28</td>
      <td>12:08:56</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1326281</th>
      <td>984121CK7</td>
      <td>2017-12-28</td>
      <td>12:08:56</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1326282</th>
      <td>984121CK7</td>
      <td>2017-12-28</td>
      <td>12:08:57</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1326283</th>
      <td>984121CK7</td>
      <td>2017-12-29</td>
      <td>8:00:11</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1326284</th>
      <td>984121CK7</td>
      <td>2017-12-29</td>
      <td>8:00:11</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1326285 rows × 4 columns</p>
</div>




```python
# extract month and year from the date field
yields['year_month'] = yields['trd_exctn_dt'].dt.to_period('M')
yields
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>7:57:03</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>1</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:29:00</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:29:00</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>3</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:34:48</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>037833BC3</td>
      <td>2015-05-07</td>
      <td>12:37:44</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1326280</th>
      <td>984121CK7</td>
      <td>2017-12-28</td>
      <td>12:08:56</td>
      <td>NaN</td>
      <td>2017-12</td>
    </tr>
    <tr>
      <th>1326281</th>
      <td>984121CK7</td>
      <td>2017-12-28</td>
      <td>12:08:56</td>
      <td>NaN</td>
      <td>2017-12</td>
    </tr>
    <tr>
      <th>1326282</th>
      <td>984121CK7</td>
      <td>2017-12-28</td>
      <td>12:08:57</td>
      <td>NaN</td>
      <td>2017-12</td>
    </tr>
    <tr>
      <th>1326283</th>
      <td>984121CK7</td>
      <td>2017-12-29</td>
      <td>8:00:11</td>
      <td>NaN</td>
      <td>2017-12</td>
    </tr>
    <tr>
      <th>1326284</th>
      <td>984121CK7</td>
      <td>2017-12-29</td>
      <td>8:00:11</td>
      <td>NaN</td>
      <td>2017-12</td>
    </tr>
  </tbody>
</table>
<p>1326285 rows × 5 columns</p>
</div>




```python
# sort dataframe first by bond issue, then by trade date, and then by trade time in ascending order.
yields = yields.sort_values(by=['CUSIP_ID', 'trd_exctn_dt', 'trd_exctn_tm'], ascending=True)
```


```python
yields[64:80]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1198536</th>
      <td>00077TAB0</td>
      <td>2015-01-05</td>
      <td>14:27:45</td>
      <td>6.608047</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198537</th>
      <td>00077TAB0</td>
      <td>2015-01-05</td>
      <td>14:27:45</td>
      <td>6.525827</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198538</th>
      <td>00077TAB0</td>
      <td>2015-01-06</td>
      <td>10:23:34</td>
      <td>6.842175</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198539</th>
      <td>00077TAB0</td>
      <td>2015-01-06</td>
      <td>10:23:34</td>
      <td>6.786439</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198540</th>
      <td>00077TAB0</td>
      <td>2015-02-17</td>
      <td>11:24:15</td>
      <td>7.002821</td>
      <td>2015-02</td>
    </tr>
    <tr>
      <th>1198541</th>
      <td>00077TAB0</td>
      <td>2015-02-17</td>
      <td>11:24:15</td>
      <td>6.897267</td>
      <td>2015-02</td>
    </tr>
    <tr>
      <th>111651</th>
      <td>00077TAB0</td>
      <td>2015-03-31</td>
      <td>14:47:54</td>
      <td>6.758606</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111652</th>
      <td>00077TAB0</td>
      <td>2015-03-31</td>
      <td>14:59:18</td>
      <td>6.816467</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111653</th>
      <td>00077TAB0</td>
      <td>2015-03-31</td>
      <td>14:59:18</td>
      <td>6.816467</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111654</th>
      <td>00077TAB0</td>
      <td>2015-04-24</td>
      <td>12:10:55</td>
      <td>6.029157</td>
      <td>2015-04</td>
    </tr>
    <tr>
      <th>111655</th>
      <td>00077TAB0</td>
      <td>2015-04-24</td>
      <td>12:10:55</td>
      <td>6.029157</td>
      <td>2015-04</td>
    </tr>
    <tr>
      <th>111656</th>
      <td>00077TAB0</td>
      <td>2015-06-04</td>
      <td>11:17:07</td>
      <td>6.404942</td>
      <td>2015-06</td>
    </tr>
    <tr>
      <th>111657</th>
      <td>00077TAB0</td>
      <td>2015-06-10</td>
      <td>11:09:56</td>
      <td>6.492385</td>
      <td>2015-06</td>
    </tr>
    <tr>
      <th>111658</th>
      <td>00077TAB0</td>
      <td>2015-06-10</td>
      <td>11:09:56</td>
      <td>6.489400</td>
      <td>2015-06</td>
    </tr>
    <tr>
      <th>111659</th>
      <td>00077TAB0</td>
      <td>2015-06-10</td>
      <td>11:09:56</td>
      <td>6.484927</td>
      <td>2015-06</td>
    </tr>
    <tr>
      <th>111660</th>
      <td>00077TAB0</td>
      <td>2015-07-07</td>
      <td>14:35:19</td>
      <td>6.901996</td>
      <td>2015-07</td>
    </tr>
  </tbody>
</table>
</div>




```python
# for each bond issue in every trade day, we only keep the last yield that occurs in the day.
yields = yields.drop_duplicates(subset=['CUSIP_ID', 'trd_exctn_dt'], keep='last')
yields
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1198533</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198534</th>
      <td>00077TAA2</td>
      <td>2015-01-27</td>
      <td>13:37:06</td>
      <td>NaN</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198535</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111591</th>
      <td>00077TAA2</td>
      <td>2015-03-26</td>
      <td>13:50:47</td>
      <td>NaN</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111592</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>56862</th>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
    </tr>
    <tr>
      <th>56866</th>
      <td>98934KAB6</td>
      <td>2017-11-28</td>
      <td>8:08:18</td>
      <td>2.865028</td>
      <td>2017-11</td>
    </tr>
    <tr>
      <th>56877</th>
      <td>98934KAB6</td>
      <td>2017-11-30</td>
      <td>17:23:00</td>
      <td>2.971758</td>
      <td>2017-11</td>
    </tr>
    <tr>
      <th>56879</th>
      <td>98934KAB6</td>
      <td>2017-12-04</td>
      <td>9:27:55</td>
      <td>3.009462</td>
      <td>2017-12</td>
    </tr>
    <tr>
      <th>56881</th>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
    </tr>
  </tbody>
</table>
<p>149595 rows × 5 columns</p>
</div>




```python
# sort yields first by cusip, then by year_month, and then by yld_pt
yields = yields.sort_values(by=['CUSIP_ID', 'year_month', 'yld_pt'])
```


```python
# check results
yields[0:10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1198533</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198534</th>
      <td>00077TAA2</td>
      <td>2015-01-27</td>
      <td>13:37:06</td>
      <td>NaN</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198535</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111591</th>
      <td>00077TAA2</td>
      <td>2015-03-26</td>
      <td>13:50:47</td>
      <td>NaN</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111592</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>111593</th>
      <td>00077TAA2</td>
      <td>2015-07-21</td>
      <td>11:43:45</td>
      <td>NaN</td>
      <td>2015-07</td>
    </tr>
    <tr>
      <th>111594</th>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
    </tr>
    <tr>
      <th>111595</th>
      <td>00077TAA2</td>
      <td>2015-07-30</td>
      <td>8:12:42</td>
      <td>NaN</td>
      <td>2015-07</td>
    </tr>
    <tr>
      <th>111597</th>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
    </tr>
    <tr>
      <th>111598</th>
      <td>00077TAA2</td>
      <td>2015-09-17</td>
      <td>15:45:59</td>
      <td>NaN</td>
      <td>2015-09</td>
    </tr>
  </tbody>
</table>
</div>




```python
# group yields by cysip and year_month, then get the indices of groups
yields_g = yields.groupby(['CUSIP_ID', 'year_month']).indices
```


```python
# the indices of group items in source dataframe
list(yields_g.values())[0:10]
```




    [array([0, 1]),
     array([2, 3]),
     array([4]),
     array([5, 6, 7]),
     array([8]),
     array([9]),
     array([10, 11]),
     array([12, 13]),
     array([14]),
     array([15])]




```python
# get the median indices in source dataframe of each group as list
import numpy as np
inds_median = [(sum(x) // len(x)) for x in list(yields_g.values())]
inds_median[0:10]
```




    [0, 2, 4, 6, 8, 9, 10, 12, 14, 15]




```python
# locate the yields data of each group in the source dataframe
# 这种方式获取的中位数不是算术意义的中位数
# 对于偶数个序列，算术中位数是求中间两位的平均值，而这种方式只是返回中间两位中任意一位的值。
yields_median = yields.iloc[inds_median]
```


```python
# 这里得到的结果和FAQ中给的期望结果有些差别，但是也是OK的。
yields_median
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1198533</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1198535</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>111592</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>111594</th>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
    </tr>
    <tr>
      <th>111597</th>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>56809</th>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
    </tr>
    <tr>
      <th>56840</th>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
    </tr>
    <tr>
      <th>56855</th>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
    </tr>
    <tr>
      <th>56862</th>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
    </tr>
    <tr>
      <th>56881</th>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 5 columns</p>
</div>




```python
# read csv as pandas dataframe
# acf351b_python_data.csv
cusips_file = '../data/acf351b_python_data.csv'
cusips = pd.read_csv(cusips_file,)
cusips
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>offering_amt</th>
      <th>offering_date</th>
      <th>maturity</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.7500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAB0</td>
      <td>150000.0</td>
      <td>1993-10-13</td>
      <td>2093-10-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.1250</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>001192AA1</td>
      <td>300000.0</td>
      <td>2001-02-23</td>
      <td>2011-01-14</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.1250</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>117277.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00163XAM2</td>
      <td>175000.0</td>
      <td>2006-08-10</td>
      <td>2013-08-15</td>
      <td>CMTN</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>5.9000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>351976.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00206RBS0</td>
      <td>1250000.0</td>
      <td>2013-02-07</td>
      <td>2016-02-12</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>0.7411</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>589049.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1055</th>
      <td>961548AQ7</td>
      <td>150000.0</td>
      <td>1997-03-12</td>
      <td>2027-03-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.6500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>51090.0</td>
    </tr>
    <tr>
      <th>1056</th>
      <td>961548AS3</td>
      <td>150000.0</td>
      <td>1997-06-19</td>
      <td>2027-06-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.5000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>56219.0</td>
    </tr>
    <tr>
      <th>1057</th>
      <td>984121CK7</td>
      <td>400000.0</td>
      <td>2015-02-26</td>
      <td>2020-09-01</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.7500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>626119.0</td>
    </tr>
    <tr>
      <th>1058</th>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.0000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>989701AU1</td>
      <td>34680.0</td>
      <td>2009-06-01</td>
      <td>2014-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.6500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>498722.0</td>
    </tr>
  </tbody>
</table>
<p>1060 rows × 14 columns</p>
</div>




```python
yields_median_usa_gbr = pd.merge(yields_median, cusips, how='inner', right_on ='cusip_id', left_on='CUSIP_ID')
```


```python
yields_median_usa_gbr
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>cusip_id</th>
      <th>offering_amt</th>
      <th>offering_date</th>
      <th>maturity</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 19 columns</p>
</div>




```python

# export
part1a_median_file = '../data/export/part1a_median_file.csv'
yields_median_usa_gbr.to_csv(part1a_median_file)
```


```python

```


```python
# # get median of each month using groupby and a lambda function
# import warnings
# with warnings.catch_warnings():
#     warnings.simplefilter("ignore", category=RuntimeWarning) # ignore RuntimeWarning
#     yields['median'] = yields.groupby(['CUSIP_ID', 'year_month'])[['yld_pt']].transform(lambda x: x.median())
```


```python
# # check results of 00077TAB0
# yields[40:60]
```


```python
# yields = yields.sort_values(by=['CUSIP_ID', 'year_month', 'yld_pt'])
```


```python
# # check results of 00077TAB0
# yields[40:60]
```

#### 💲2. CRSP on WRDS and 180-day stock return volat


ref: https://support.eventstudy.com/hc/en-us/articles/212258983-CUSIP-6-8-or-9-characters-

CUSIP, which is controlled by Standard & Poor's, is officially a 9-character string. The first 6 identify the issuer, the 7th and 8th identify the issue and the 9th is a check digit that is fully determined by the first 8 characters. 

CRSP (the default data source for Eventus on WRDS and, when subscribed and installed, for Eventus for Windows and Linux) omits the check digit and uses an 8-character CUSIP field. 

Common equity issues always have an 8th character of 0. As CRSP covers only common stocks, all CUSIPs in CRSP end in 0 as the 8th character. CUSIPs from other sources that have a non-zero digit in the 8th position are not common stock CUSIPs.


```python
# link crsp permco/permno from cusip_ids
import pandas as pd
links = '../data/crsp_cusip_link.csv'
links_data = pd.read_csv(links)
links_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP</th>
      <th>PERMNO</th>
      <th>PERMCO</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>crsp_enddt</th>
      <th>link_startdt</th>
      <th>link_enddt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>84766</td>
      <td>31989</td>
      <td>20020711</td>
      <td>20110318</td>
      <td>20020102</td>
      <td>20080424</td>
      <td>20020711</td>
      <td>20080424</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>92355</td>
      <td>28711</td>
      <td>20120614</td>
      <td>20150324</td>
      <td>20071018</td>
      <td>20200722</td>
      <td>20120614</td>
      <td>20150324</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAB0</td>
      <td>84766</td>
      <td>31989</td>
      <td>20020906</td>
      <td>20110328</td>
      <td>20020102</td>
      <td>20080424</td>
      <td>20020906</td>
      <td>20080424</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAB0</td>
      <td>92355</td>
      <td>28711</td>
      <td>20120607</td>
      <td>20150217</td>
      <td>20071018</td>
      <td>20200722</td>
      <td>20120607</td>
      <td>20150217</td>
    </tr>
    <tr>
      <th>4</th>
      <td>001192AA1</td>
      <td>15553</td>
      <td>116</td>
      <td>20021206</td>
      <td>20101216</td>
      <td>20020102</td>
      <td>20090208</td>
      <td>20021206</td>
      <td>20090208</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1124</th>
      <td>961548AS3</td>
      <td>21186</td>
      <td>21913</td>
      <td>20020726</td>
      <td>20141231</td>
      <td>20020130</td>
      <td>20150701</td>
      <td>20020726</td>
      <td>20141231</td>
    </tr>
    <tr>
      <th>1125</th>
      <td>961548AS3</td>
      <td>21186</td>
      <td>21913</td>
      <td>20151112</td>
      <td>20170524</td>
      <td>20150702</td>
      <td>20200930</td>
      <td>20151112</td>
      <td>20170524</td>
    </tr>
    <tr>
      <th>1126</th>
      <td>984121CK7</td>
      <td>27983</td>
      <td>21945</td>
      <td>20150226</td>
      <td>20200828</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20150226</td>
      <td>20200828</td>
    </tr>
    <tr>
      <th>1127</th>
      <td>98934KAB6</td>
      <td>79363</td>
      <td>29908</td>
      <td>20020702</td>
      <td>20200923</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20020702</td>
      <td>20200923</td>
    </tr>
    <tr>
      <th>1128</th>
      <td>989701AU1</td>
      <td>84129</td>
      <td>5057</td>
      <td>20090731</td>
      <td>20140414</td>
      <td>19821101</td>
      <td>20200930</td>
      <td>20090731</td>
      <td>20140414</td>
    </tr>
  </tbody>
</table>
<p>1129 rows × 9 columns</p>
</div>




```python
import numpy as np
# read csv as pandas dataframe
# 下载数据从2014年6月开始。因为要计算180天rolling标准差
# crspa_dsf = '../data/880fcbe48e8d30ce.csv'
# 下载数据从2014年4月开始。因为要计算180天rolling标准差
crspa_dsf = '../data/e862f245484c3340.csv'
# read (PERMNO, date, PERMCO, CUSIP, RET)
dsf = pd.read_csv(crspa_dsf, usecols = [0, 1, 15, 48])
dsf
```

    /Users/jade_mayer/anaconda3/lib/python3.8/site-packages/IPython/core/interactiveshell.py:3146: DtypeWarning: Columns (48) have mixed types.Specify dtype option on import or set low_memory=False.
      has_raised = await self.run_ast_nodes(code_ast.body, cell_name,





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO</th>
      <th>RET</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10145</td>
      <td>2014/04/15</td>
      <td>22168</td>
      <td>0.008689</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10145</td>
      <td>2014/04/16</td>
      <td>22168</td>
      <td>0.017337</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10145</td>
      <td>2014/04/17</td>
      <td>22168</td>
      <td>-0.002144</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10145</td>
      <td>2014/04/21</td>
      <td>22168</td>
      <td>0.000859</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10145</td>
      <td>2014/04/22</td>
      <td>22168</td>
      <td>0.001717</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>140596</th>
      <td>93013</td>
      <td>2017/12/22</td>
      <td>53204</td>
      <td>0.001886</td>
    </tr>
    <tr>
      <th>140597</th>
      <td>93013</td>
      <td>2017/12/26</td>
      <td>53204</td>
      <td>-0.001345</td>
    </tr>
    <tr>
      <th>140598</th>
      <td>93013</td>
      <td>2017/12/27</td>
      <td>53204</td>
      <td>0.006642</td>
    </tr>
    <tr>
      <th>140599</th>
      <td>93013</td>
      <td>2017/12/28</td>
      <td>53204</td>
      <td>-0.007936</td>
    </tr>
    <tr>
      <th>140600</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
    </tr>
  </tbody>
</table>
<p>140601 rows × 4 columns</p>
</div>



Missing Value Codes in SAS

When looking up a holding period return (RET), or delisting return (DLRET), SAS may return a missing value code. These are indicated with a decimal point followed by a letter (e.g. ".E", ".D"). The descriptions for the missing value codes in SAS can be found on the "Variable Description" page for CRSP Stock.


```python
# missing value
# B means Off-exchange
subset = dsf.loc[dsf['RET'] == 'B'].count()
subset
```




    PERMNO    0
    date      0
    PERMCO    0
    RET       0
    dtype: int64




```python
# missing value
# C means No valid previous price
subset = dsf.loc[dsf['RET'] == 'C'].count()
subset
```




    PERMNO    3
    date      3
    PERMCO    3
    RET       3
    dtype: int64




```python
# remove missing data rows
dsf = dsf[dsf.RET != 'C']
# df = df[df.RET != 'B']
dsf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO</th>
      <th>RET</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10145</td>
      <td>2014/04/15</td>
      <td>22168</td>
      <td>0.008689</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10145</td>
      <td>2014/04/16</td>
      <td>22168</td>
      <td>0.017337</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10145</td>
      <td>2014/04/17</td>
      <td>22168</td>
      <td>-0.002144</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10145</td>
      <td>2014/04/21</td>
      <td>22168</td>
      <td>0.000859</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10145</td>
      <td>2014/04/22</td>
      <td>22168</td>
      <td>0.001717</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>140596</th>
      <td>93013</td>
      <td>2017/12/22</td>
      <td>53204</td>
      <td>0.001886</td>
    </tr>
    <tr>
      <th>140597</th>
      <td>93013</td>
      <td>2017/12/26</td>
      <td>53204</td>
      <td>-0.001345</td>
    </tr>
    <tr>
      <th>140598</th>
      <td>93013</td>
      <td>2017/12/27</td>
      <td>53204</td>
      <td>0.006642</td>
    </tr>
    <tr>
      <th>140599</th>
      <td>93013</td>
      <td>2017/12/28</td>
      <td>53204</td>
      <td>-0.007936</td>
    </tr>
    <tr>
      <th>140600</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
    </tr>
  </tbody>
</table>
<p>140598 rows × 4 columns</p>
</div>




```python
# calculate rolling standard deviation of 180-day

# dsf['rolling'] = 
rollings = dsf.groupby('PERMNO')['RET'].rolling(180).std()
# rollings_df = pd.DataFrame(data = [rollings.values] * len(rollings), columns = rollings.index)
rollings[(10145, 0)]
```




    nan




```python
dsf.index
```




    Int64Index([     0,      1,      2,      3,      4,      5,      6,      7,
                     8,      9,
                ...
                140591, 140592, 140593, 140594, 140595, 140596, 140597, 140598,
                140599, 140600],
               dtype='int64', length=140598)




```python
# join rolling data with source dataframe on (dsf.index, 'PERMNO')
dsf = dsf.merge(rollings.rename('rollings_'), on=[dsf.index, 'PERMNO'] ,left_index=True, right_index=True)
```


```python
dsf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO</th>
      <th>RET</th>
      <th>rollings_</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10145</td>
      <td>2014/04/15</td>
      <td>22168</td>
      <td>0.008689</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10145</td>
      <td>2014/04/16</td>
      <td>22168</td>
      <td>0.017337</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10145</td>
      <td>2014/04/17</td>
      <td>22168</td>
      <td>-0.002144</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10145</td>
      <td>2014/04/21</td>
      <td>22168</td>
      <td>0.000859</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10145</td>
      <td>2014/04/22</td>
      <td>22168</td>
      <td>0.001717</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>140596</th>
      <td>93013</td>
      <td>2017/12/22</td>
      <td>53204</td>
      <td>0.001886</td>
      <td>0.010455</td>
    </tr>
    <tr>
      <th>140597</th>
      <td>93013</td>
      <td>2017/12/26</td>
      <td>53204</td>
      <td>-0.001345</td>
      <td>0.010445</td>
    </tr>
    <tr>
      <th>140598</th>
      <td>93013</td>
      <td>2017/12/27</td>
      <td>53204</td>
      <td>0.006642</td>
      <td>0.010446</td>
    </tr>
    <tr>
      <th>140599</th>
      <td>93013</td>
      <td>2017/12/28</td>
      <td>53204</td>
      <td>-0.007936</td>
      <td>0.010463</td>
    </tr>
    <tr>
      <th>140600</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
    </tr>
  </tbody>
</table>
<p>140598 rows × 5 columns</p>
</div>




```python
dsf_cusip = pd.merge(dsf, links_data, on=['PERMNO'], how='inner')
```


```python
dsf_cusip
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO_x</th>
      <th>RET</th>
      <th>rollings_</th>
      <th>CUSIP</th>
      <th>PERMCO_y</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>crsp_enddt</th>
      <th>link_startdt</th>
      <th>link_enddt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10145</td>
      <td>2014/04/15</td>
      <td>22168</td>
      <td>0.008689</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10145</td>
      <td>2014/04/16</td>
      <td>22168</td>
      <td>0.017337</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10145</td>
      <td>2014/04/17</td>
      <td>22168</td>
      <td>-0.002144</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10145</td>
      <td>2014/04/21</td>
      <td>22168</td>
      <td>0.000859</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10145</td>
      <td>2014/04/22</td>
      <td>22168</td>
      <td>0.001717</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1001488</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
      <td>03523TBK3</td>
      <td>53204</td>
      <td>20110707</td>
      <td>20140623</td>
      <td>20090916</td>
      <td>20200930</td>
      <td>20110707</td>
      <td>20140623</td>
    </tr>
    <tr>
      <th>1001489</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
      <td>035240AC4</td>
      <td>53204</td>
      <td>20161220</td>
      <td>20180725</td>
      <td>20090916</td>
      <td>20200930</td>
      <td>20161220</td>
      <td>20180725</td>
    </tr>
    <tr>
      <th>1001490</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
      <td>035242AF3</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20190131</td>
      <td>20090916</td>
      <td>20200930</td>
      <td>20140122</td>
      <td>20190131</td>
    </tr>
    <tr>
      <th>1001491</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
      <td>035242AK2</td>
      <td>53204</td>
      <td>20160113</td>
      <td>20200930</td>
      <td>20090916</td>
      <td>20200930</td>
      <td>20160113</td>
      <td>20200930</td>
    </tr>
    <tr>
      <th>1001492</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>20200930</td>
      <td>20140122</td>
      <td>20170117</td>
    </tr>
  </tbody>
</table>
<p>1001493 rows × 13 columns</p>
</div>




```python
dsf_cusip.loc[dsf_cusip['PERMNO'] == 10145]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO_x</th>
      <th>RET</th>
      <th>rollings_</th>
      <th>CUSIP</th>
      <th>PERMCO_y</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>crsp_enddt</th>
      <th>link_startdt</th>
      <th>link_enddt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10145</td>
      <td>2014/04/15</td>
      <td>22168</td>
      <td>0.008689</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10145</td>
      <td>2014/04/16</td>
      <td>22168</td>
      <td>0.017337</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10145</td>
      <td>2014/04/17</td>
      <td>22168</td>
      <td>-0.002144</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10145</td>
      <td>2014/04/21</td>
      <td>22168</td>
      <td>0.000859</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10145</td>
      <td>2014/04/22</td>
      <td>22168</td>
      <td>0.001717</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>931</th>
      <td>10145</td>
      <td>2017/12/22</td>
      <td>22168</td>
      <td>-0.001496</td>
      <td>0.006667</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>932</th>
      <td>10145</td>
      <td>2017/12/26</td>
      <td>22168</td>
      <td>0.001759</td>
      <td>0.006667</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>933</th>
      <td>10145</td>
      <td>2017/12/27</td>
      <td>22168</td>
      <td>0.001236</td>
      <td>0.006667</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>934</th>
      <td>10145</td>
      <td>2017/12/28</td>
      <td>22168</td>
      <td>0.001169</td>
      <td>0.006601</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>935</th>
      <td>10145</td>
      <td>2017/12/29</td>
      <td>22168</td>
      <td>-0.004996</td>
      <td>0.006600</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
  </tbody>
</table>
<p>936 rows × 13 columns</p>
</div>




```python
# read csv as pandas dataframe
# acf351b_python_data.csv
cusips_file = '../data/acf351b_python_data.csv'
cusips = pd.read_csv(cusips_file)
cusips
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>offering_amt</th>
      <th>offering_date</th>
      <th>maturity</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.7500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAB0</td>
      <td>150000.0</td>
      <td>1993-10-13</td>
      <td>2093-10-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.1250</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>001192AA1</td>
      <td>300000.0</td>
      <td>2001-02-23</td>
      <td>2011-01-14</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.1250</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>117277.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00163XAM2</td>
      <td>175000.0</td>
      <td>2006-08-10</td>
      <td>2013-08-15</td>
      <td>CMTN</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>5.9000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>351976.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00206RBS0</td>
      <td>1250000.0</td>
      <td>2013-02-07</td>
      <td>2016-02-12</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>0.7411</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>589049.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1055</th>
      <td>961548AQ7</td>
      <td>150000.0</td>
      <td>1997-03-12</td>
      <td>2027-03-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.6500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>51090.0</td>
    </tr>
    <tr>
      <th>1056</th>
      <td>961548AS3</td>
      <td>150000.0</td>
      <td>1997-06-19</td>
      <td>2027-06-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.5000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>56219.0</td>
    </tr>
    <tr>
      <th>1057</th>
      <td>984121CK7</td>
      <td>400000.0</td>
      <td>2015-02-26</td>
      <td>2020-09-01</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.7500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>626119.0</td>
    </tr>
    <tr>
      <th>1058</th>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.0000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>989701AU1</td>
      <td>34680.0</td>
      <td>2009-06-01</td>
      <td>2014-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.6500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>498722.0</td>
    </tr>
  </tbody>
</table>
<p>1060 rows × 14 columns</p>
</div>




```python
dsf_cusip_country = pd.merge(dsf_cusip, cusips, left_on=['CUSIP'], right_on=['cusip_id'], how='inner')
```


```python
dsf_cusip_country.loc[dsf_cusip['PERMNO'] == 10145]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO_x</th>
      <th>RET</th>
      <th>rollings_</th>
      <th>CUSIP</th>
      <th>PERMCO_y</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>...</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10145</td>
      <td>2014/04/15</td>
      <td>22168</td>
      <td>0.008689</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10145</td>
      <td>2014/04/16</td>
      <td>22168</td>
      <td>0.017337</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10145</td>
      <td>2014/04/17</td>
      <td>22168</td>
      <td>-0.002144</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10145</td>
      <td>2014/04/21</td>
      <td>22168</td>
      <td>0.000859</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10145</td>
      <td>2014/04/22</td>
      <td>22168</td>
      <td>0.001717</td>
      <td>NaN</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>931</th>
      <td>10145</td>
      <td>2017/12/22</td>
      <td>22168</td>
      <td>-0.001496</td>
      <td>0.006667</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>932</th>
      <td>10145</td>
      <td>2017/12/26</td>
      <td>22168</td>
      <td>0.001759</td>
      <td>0.006667</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>933</th>
      <td>10145</td>
      <td>2017/12/27</td>
      <td>22168</td>
      <td>0.001236</td>
      <td>0.006667</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>934</th>
      <td>10145</td>
      <td>2017/12/28</td>
      <td>22168</td>
      <td>0.001169</td>
      <td>0.006601</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>935</th>
      <td>10145</td>
      <td>2017/12/29</td>
      <td>22168</td>
      <td>-0.004996</td>
      <td>0.006600</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
  </tbody>
</table>
<p>936 rows × 27 columns</p>
</div>




```python
dsf_cusip_country_nnan = dsf_cusip_country.dropna()

```


```python
dsf_cusip_country_nnan
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO_x</th>
      <th>RET</th>
      <th>rollings_</th>
      <th>CUSIP</th>
      <th>PERMCO_y</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>...</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>179</th>
      <td>10145</td>
      <td>2014/12/30</td>
      <td>22168</td>
      <td>-0.009344</td>
      <td>0.010120</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>180</th>
      <td>10145</td>
      <td>2014/12/31</td>
      <td>22168</td>
      <td>-0.007943</td>
      <td>0.010122</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>181</th>
      <td>10145</td>
      <td>2015/01/02</td>
      <td>22168</td>
      <td>0.003103</td>
      <td>0.010046</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>182</th>
      <td>10145</td>
      <td>2015/01/05</td>
      <td>22168</td>
      <td>-0.019056</td>
      <td>0.010150</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>183</th>
      <td>10145</td>
      <td>2015/01/06</td>
      <td>22168</td>
      <td>-0.002339</td>
      <td>0.010152</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1001488</th>
      <td>93013</td>
      <td>2017/12/22</td>
      <td>53204</td>
      <td>0.001886</td>
      <td>0.010455</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001489</th>
      <td>93013</td>
      <td>2017/12/26</td>
      <td>53204</td>
      <td>-0.001345</td>
      <td>0.010445</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001490</th>
      <td>93013</td>
      <td>2017/12/27</td>
      <td>53204</td>
      <td>0.006642</td>
      <td>0.010446</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001491</th>
      <td>93013</td>
      <td>2017/12/28</td>
      <td>53204</td>
      <td>-0.007936</td>
      <td>0.010463</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001492</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
  </tbody>
</table>
<p>786357 rows × 27 columns</p>
</div>




```python
dsf_cusip_country_ = dsf_cusip_country_nnan.drop_duplicates(subset=['cusip_id', 'date'], keep='last')


```


```python
dsf_cusip_country_
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PERMNO</th>
      <th>date</th>
      <th>PERMCO_x</th>
      <th>RET</th>
      <th>rollings_</th>
      <th>CUSIP</th>
      <th>PERMCO_y</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>...</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>179</th>
      <td>10145</td>
      <td>2014/12/30</td>
      <td>22168</td>
      <td>-0.009344</td>
      <td>0.010120</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>180</th>
      <td>10145</td>
      <td>2014/12/31</td>
      <td>22168</td>
      <td>-0.007943</td>
      <td>0.010122</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>181</th>
      <td>10145</td>
      <td>2015/01/02</td>
      <td>22168</td>
      <td>0.003103</td>
      <td>0.010046</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>182</th>
      <td>10145</td>
      <td>2015/01/05</td>
      <td>22168</td>
      <td>-0.019056</td>
      <td>0.010150</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>183</th>
      <td>10145</td>
      <td>2015/01/06</td>
      <td>22168</td>
      <td>-0.002339</td>
      <td>0.010152</td>
      <td>438516BK1</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1001488</th>
      <td>93013</td>
      <td>2017/12/22</td>
      <td>53204</td>
      <td>0.001886</td>
      <td>0.010455</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001489</th>
      <td>93013</td>
      <td>2017/12/26</td>
      <td>53204</td>
      <td>-0.001345</td>
      <td>0.010445</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001490</th>
      <td>93013</td>
      <td>2017/12/27</td>
      <td>53204</td>
      <td>0.006642</td>
      <td>0.010446</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001491</th>
      <td>93013</td>
      <td>2017/12/28</td>
      <td>53204</td>
      <td>-0.007936</td>
      <td>0.010463</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>1001492</th>
      <td>93013</td>
      <td>2017/12/29</td>
      <td>53204</td>
      <td>0.002696</td>
      <td>0.010431</td>
      <td>03524BAD8</td>
      <td>53204</td>
      <td>20140122</td>
      <td>20170117</td>
      <td>20090916</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
  </tbody>
</table>
<p>716846 rows × 27 columns</p>
</div>




```python
dsf_cusip_country_.to_csv('../data/export/part1b_180days_rolling_window.csv')
```

#### 💲3. PRCCQ from Compustat

ref: https://bbs.pinggu.org/thread-3588010-1-1.html

关于market leverage和book leverage的研究可以追溯到Fama和French在1992年的论文The Cross-Section of Expected Stock Returns（没错就是讲三因子模型的那篇）。

论文里关于两种leverage的定义原话是We use two leverage variables, the ratio of book assets to market equity, A/ME, and the ratio of book assets to book equity, A/BE. We interpret A/ME as a measure of market leverage, while A/BE is a measure of book leverage.

A指的是Total Assets，ME指的是Market Value of Equity，BE指的是Book Value of Equity。Market leverage和book leverage是对公司财务杠杆的两种衡量方式，我们平时一般说的financial leverage指的是book leverage。

顺带一提，论文中的结论是股票收益和market leverage成正相关，和book leverage不相关甚至轻微负相关

ref: https://www.indeed.com/career-advice/career-development/how-to-calculate-total-debt

Total debt is calculated by adding up a company's liabilities, or debts, which are categorized as short and long-term debt. Financial lenders or business leaders may look at a company's balance sheet to factor in the debt ratio to make informed decisions about future loan options. They calculate the debt ratio by taking the total debt and dividing it by the total assets.

Outstanding Debt

Debt that has not yet been repaid in full. For example, if one borrows $10,000 and has paid back $2,000, the outstanding debt is $8,000. In general, interest is calculated over the outstanding debt rather than the original amount borrowed.

ref: https://www.lawinsider.com/dictionary/book-leverage-ratio

Book Leverage Ratio means the ratio of Total Consolidated Long Term Debt to Total Assets, as shown in the applicable Financial Statements for Guarantor A for any accounting period and determined in accordance with GAAP.

ref: https://www.quora.com/What-are-the-current-liabilities-in-a-balance-sheet

Liability: Liability is something which the business owes. For example, a loan taken from a bank.

Classification of Liabilities-

Current liabilities: Current liabilities are the liabilities which the business has to pay within a year. These are short-term liabilities. For example, trade creditors. Trade Creditors are the suppliers from whom we purchase the goods on credit. Usually, the payment to trade creditors is made within one year. Other examples of current liabilities are outstanding(unpaid) salaries, tax payable, etc.

Non-Current Liabilities: Non-Current Liabilities are long term liabilities which are not repayable within one year. For example, Long term loan taken for say five years.

Contingent Liability: Contingent Liability is that kind of a liability which is non-existent as on date, but it may become an actual liability in the future. For example, if a customer has filed a suit against the company for some compensation. This can become an actual liability in the future if the firm loses the case. However, as on date, it is not a liability as the outcome is not known today.




关于CRSP / Compustat链接表的详细信息：

http://kaichen.work/?p=138


```python
gvkey_crsp_link = '../data/gvkey_crsp_link.csv'
gvkey = pd.read_csv(gvkey_crsp_link)
# gvkey = gvkey.dropna()
# gvkey_ = gvkey['gvkey']
```


```python
# gvkey_.to_csv('../gvkeys_unique.csv')
```


```python
gvkey
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GVKEY</th>
      <th>LINKPRIM</th>
      <th>LIID</th>
      <th>LINKTYPE</th>
      <th>LPERMNO</th>
      <th>LPERMCO</th>
      <th>LINKDT</th>
      <th>LINKENDDT</th>
      <th>conm</th>
      <th>tic</th>
      <th>...</th>
      <th>ipodate</th>
      <th>dldte</th>
      <th>STKO</th>
      <th>FYRC</th>
      <th>GSECTOR</th>
      <th>GGROUP</th>
      <th>GIND</th>
      <th>GSUBIND</th>
      <th>SPCINDCD</th>
      <th>SPCSECCD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>P</td>
      <td>01</td>
      <td>LC</td>
      <td>10145</td>
      <td>22168</td>
      <td>19620131</td>
      <td>E</td>
      <td>HONEYWELL INTERNATIONAL INC</td>
      <td>HON</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>20.0</td>
      <td>2010.0</td>
      <td>201050.0</td>
      <td>20105010.0</td>
      <td>355</td>
      <td>925</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1318</td>
      <td>P</td>
      <td>01</td>
      <td>LU</td>
      <td>41443</td>
      <td>20057</td>
      <td>19650118</td>
      <td>20071130</td>
      <td>ALLTEL CORP</td>
      <td>AT.2</td>
      <td>...</td>
      <td>NaN</td>
      <td>20071119.0</td>
      <td>0</td>
      <td>12</td>
      <td>50.0</td>
      <td>5010.0</td>
      <td>501020.0</td>
      <td>50102010.0</td>
      <td>715</td>
      <td>974</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1440</td>
      <td>P</td>
      <td>01</td>
      <td>LC</td>
      <td>24109</td>
      <td>20077</td>
      <td>19620131</td>
      <td>E</td>
      <td>AMERICAN ELECTRIC POWER CO</td>
      <td>AEP</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>55.0</td>
      <td>5510.0</td>
      <td>551010.0</td>
      <td>55101010.0</td>
      <td>705</td>
      <td>700</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1440</td>
      <td>C</td>
      <td>00X</td>
      <td>LC</td>
      <td>24109</td>
      <td>20077</td>
      <td>19510101</td>
      <td>19620130</td>
      <td>AMERICAN ELECTRIC POWER CO</td>
      <td>AEP</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>55.0</td>
      <td>5510.0</td>
      <td>551010.0</td>
      <td>55101010.0</td>
      <td>705</td>
      <td>700</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1447</td>
      <td>C</td>
      <td>01</td>
      <td>LU</td>
      <td>59176</td>
      <td>90</td>
      <td>19721214</td>
      <td>E</td>
      <td>AMERICAN EXPRESS CO</td>
      <td>AXP</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>40.0</td>
      <td>4020.0</td>
      <td>402020.0</td>
      <td>40202010.0</td>
      <td>850</td>
      <td>800</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>231</th>
      <td>209382</td>
      <td>P</td>
      <td>91</td>
      <td>LC</td>
      <td>89330</td>
      <td>37665</td>
      <td>20020322</td>
      <td>E</td>
      <td>VALE SA</td>
      <td>VALE</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>15.0</td>
      <td>1510.0</td>
      <td>151040.0</td>
      <td>15104050.0</td>
      <td>360</td>
      <td>970</td>
    </tr>
    <tr>
      <th>232</th>
      <td>212340</td>
      <td>P</td>
      <td>90</td>
      <td>LU</td>
      <td>85888</td>
      <td>16024</td>
      <td>19980327</td>
      <td>20190131</td>
      <td>SHIRE PLC</td>
      <td>SHPG</td>
      <td>...</td>
      <td>19960215.0</td>
      <td>20190109.0</td>
      <td>0</td>
      <td>12</td>
      <td>35.0</td>
      <td>3520.0</td>
      <td>352010.0</td>
      <td>35201010.0</td>
      <td>285</td>
      <td>905</td>
    </tr>
    <tr>
      <th>233</th>
      <td>241216</td>
      <td>P</td>
      <td>90</td>
      <td>LC</td>
      <td>88822</td>
      <td>41009</td>
      <td>20001113</td>
      <td>E</td>
      <td>SYNGENTA AG</td>
      <td>SYT</td>
      <td>...</td>
      <td>20001113.0</td>
      <td>20180110.0</td>
      <td>0</td>
      <td>12</td>
      <td>15.0</td>
      <td>1510.0</td>
      <td>151010.0</td>
      <td>15101030.0</td>
      <td>167</td>
      <td>970</td>
    </tr>
    <tr>
      <th>234</th>
      <td>241637</td>
      <td>P</td>
      <td>90</td>
      <td>LC</td>
      <td>93013</td>
      <td>53204</td>
      <td>20090916</td>
      <td>E</td>
      <td>ANHEUSER-BUSCH INBEV</td>
      <td>BUD</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>30.0</td>
      <td>3020.0</td>
      <td>302010.0</td>
      <td>30201010.0</td>
      <td>140</td>
      <td>978</td>
    </tr>
    <tr>
      <th>235</th>
      <td>252940</td>
      <td>P</td>
      <td>90</td>
      <td>LC</td>
      <td>75811</td>
      <td>22107</td>
      <td>20010402</td>
      <td>E</td>
      <td>MITSUBISHI UFJ FINANCIAL GRP</td>
      <td>MUFG</td>
      <td>...</td>
      <td>20010401.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>40.0</td>
      <td>4010.0</td>
      <td>401010.0</td>
      <td>40101010.0</td>
      <td>810</td>
      <td>800</td>
    </tr>
  </tbody>
</table>
<p>236 rows × 47 columns</p>
</div>




```python
# fundq = '../data/7cf711fc5ea7973d.csv'
fundq = '../data/309e6ea3f87e4430.csv'

# open fundq as dataframe
df = pd.read_csv(fundq)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>datafqtr</th>
      <th>atq</th>
      <th>cshoq</th>
      <th>dlttq</th>
      <th>lctq</th>
      <th>costat</th>
      <th>prccq</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>2015Q1</td>
      <td>45357.000</td>
      <td>781.707</td>
      <td>5661.000</td>
      <td>15432.0</td>
      <td>A</td>
      <td>104.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>2015Q2</td>
      <td>46412.000</td>
      <td>781.762</td>
      <td>5562.000</td>
      <td>15574.0</td>
      <td>A</td>
      <td>101.97</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>2015Q3</td>
      <td>46625.000</td>
      <td>770.691</td>
      <td>5599.000</td>
      <td>16367.0</td>
      <td>A</td>
      <td>94.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>2015Q4</td>
      <td>49316.000</td>
      <td>770.400</td>
      <td>5554.000</td>
      <td>18371.0</td>
      <td>A</td>
      <td>103.57</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>2016Q1</td>
      <td>50365.000</td>
      <td>762.115</td>
      <td>9700.000</td>
      <td>15659.0</td>
      <td>A</td>
      <td>112.05</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1851</th>
      <td>252940</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>2016Q3</td>
      <td>2586542.894</td>
      <td>13429.631</td>
      <td>219398.261</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.16</td>
    </tr>
    <tr>
      <th>1852</th>
      <td>252940</td>
      <td>2017/03/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q1</td>
      <td>2016Q4</td>
      <td>2722353.780</td>
      <td>13429.944</td>
      <td>241134.298</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.34</td>
    </tr>
    <tr>
      <th>1853</th>
      <td>252940</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>2017Q1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.75</td>
    </tr>
    <tr>
      <th>1854</th>
      <td>252940</td>
      <td>2017/09/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q3</td>
      <td>2017Q2</td>
      <td>2666912.107</td>
      <td>13289.784</td>
      <td>267516.335</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.44</td>
    </tr>
    <tr>
      <th>1855</th>
      <td>252940</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>2017Q3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>7.27</td>
    </tr>
  </tbody>
</table>
<p>1856 rows × 17 columns</p>
</div>




```python
# compute total outstanding debt
df['total_debt'] = df['dlttq'] + df['lctq']
# compute book leverage
df['book_leverage'] = df['total_debt'] / df['atq']
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>datafqtr</th>
      <th>atq</th>
      <th>cshoq</th>
      <th>dlttq</th>
      <th>lctq</th>
      <th>costat</th>
      <th>prccq</th>
      <th>total_debt</th>
      <th>book_leverage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>2015Q1</td>
      <td>45357.000</td>
      <td>781.707</td>
      <td>5661.000</td>
      <td>15432.0</td>
      <td>A</td>
      <td>104.31</td>
      <td>21093.0</td>
      <td>0.465044</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>2015Q2</td>
      <td>46412.000</td>
      <td>781.762</td>
      <td>5562.000</td>
      <td>15574.0</td>
      <td>A</td>
      <td>101.97</td>
      <td>21136.0</td>
      <td>0.455399</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>2015Q3</td>
      <td>46625.000</td>
      <td>770.691</td>
      <td>5599.000</td>
      <td>16367.0</td>
      <td>A</td>
      <td>94.69</td>
      <td>21966.0</td>
      <td>0.471121</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>2015Q4</td>
      <td>49316.000</td>
      <td>770.400</td>
      <td>5554.000</td>
      <td>18371.0</td>
      <td>A</td>
      <td>103.57</td>
      <td>23925.0</td>
      <td>0.485137</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>2016Q1</td>
      <td>50365.000</td>
      <td>762.115</td>
      <td>9700.000</td>
      <td>15659.0</td>
      <td>A</td>
      <td>112.05</td>
      <td>25359.0</td>
      <td>0.503504</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1851</th>
      <td>252940</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>2016Q3</td>
      <td>2586542.894</td>
      <td>13429.631</td>
      <td>219398.261</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.16</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1852</th>
      <td>252940</td>
      <td>2017/03/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q1</td>
      <td>2016Q4</td>
      <td>2722353.780</td>
      <td>13429.944</td>
      <td>241134.298</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.34</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1853</th>
      <td>252940</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>2017Q1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.75</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1854</th>
      <td>252940</td>
      <td>2017/09/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q3</td>
      <td>2017Q2</td>
      <td>2666912.107</td>
      <td>13289.784</td>
      <td>267516.335</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.44</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1855</th>
      <td>252940</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>2017Q3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>7.27</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1856 rows × 19 columns</p>
</div>




```python
# compute market capitalization
df['market_capitalization'] = (df['prccq'] * df['cshoq'])
# compute market leverage
df['market_leverage'] = df['total_debt'] / df['market_capitalization']
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>atq</th>
      <th>cshoq</th>
      <th>dlttq</th>
      <th>lctq</th>
      <th>costat</th>
      <th>prccq</th>
      <th>total_debt</th>
      <th>book_leverage</th>
      <th>market_capitalization</th>
      <th>market_leverage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>45357.000</td>
      <td>781.707</td>
      <td>5661.000</td>
      <td>15432.0</td>
      <td>A</td>
      <td>104.31</td>
      <td>21093.0</td>
      <td>0.465044</td>
      <td>81539.85717</td>
      <td>0.258683</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>46412.000</td>
      <td>781.762</td>
      <td>5562.000</td>
      <td>15574.0</td>
      <td>A</td>
      <td>101.97</td>
      <td>21136.0</td>
      <td>0.455399</td>
      <td>79716.27114</td>
      <td>0.265140</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>46625.000</td>
      <td>770.691</td>
      <td>5599.000</td>
      <td>16367.0</td>
      <td>A</td>
      <td>94.69</td>
      <td>21966.0</td>
      <td>0.471121</td>
      <td>72976.73079</td>
      <td>0.301000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>49316.000</td>
      <td>770.400</td>
      <td>5554.000</td>
      <td>18371.0</td>
      <td>A</td>
      <td>103.57</td>
      <td>23925.0</td>
      <td>0.485137</td>
      <td>79790.32800</td>
      <td>0.299848</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>50365.000</td>
      <td>762.115</td>
      <td>9700.000</td>
      <td>15659.0</td>
      <td>A</td>
      <td>112.05</td>
      <td>25359.0</td>
      <td>0.503504</td>
      <td>85394.98575</td>
      <td>0.296961</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1851</th>
      <td>252940</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>2586542.894</td>
      <td>13429.631</td>
      <td>219398.261</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>82726.52696</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1852</th>
      <td>252940</td>
      <td>2017/03/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q1</td>
      <td>...</td>
      <td>2722353.780</td>
      <td>13429.944</td>
      <td>241134.298</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.34</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>85145.84496</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1853</th>
      <td>252940</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.75</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1854</th>
      <td>252940</td>
      <td>2017/09/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q3</td>
      <td>...</td>
      <td>2666912.107</td>
      <td>13289.784</td>
      <td>267516.335</td>
      <td>NaN</td>
      <td>A</td>
      <td>6.44</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>85586.20896</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1855</th>
      <td>252940</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>7.27</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1856 rows × 21 columns</p>
</div>




```python
leverage = pd.merge(df, gvkey, left_on='gvkey', right_on='GVKEY')
```


```python
leverage
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>ipodate</th>
      <th>dldte</th>
      <th>STKO</th>
      <th>FYRC</th>
      <th>GSECTOR</th>
      <th>GGROUP</th>
      <th>GIND</th>
      <th>GSUBIND</th>
      <th>SPCINDCD</th>
      <th>SPCSECCD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>20.0</td>
      <td>2010.0</td>
      <td>201050.0</td>
      <td>20105010.0</td>
      <td>355</td>
      <td>925</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>20.0</td>
      <td>2010.0</td>
      <td>201050.0</td>
      <td>20105010.0</td>
      <td>355</td>
      <td>925</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>20.0</td>
      <td>2010.0</td>
      <td>201050.0</td>
      <td>20105010.0</td>
      <td>355</td>
      <td>925</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>20.0</td>
      <td>2010.0</td>
      <td>201050.0</td>
      <td>20105010.0</td>
      <td>355</td>
      <td>925</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>12</td>
      <td>20.0</td>
      <td>2010.0</td>
      <td>201050.0</td>
      <td>20105010.0</td>
      <td>355</td>
      <td>925</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2383</th>
      <td>252940</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>20010401.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>40.0</td>
      <td>4010.0</td>
      <td>401010.0</td>
      <td>40101010.0</td>
      <td>810</td>
      <td>800</td>
    </tr>
    <tr>
      <th>2384</th>
      <td>252940</td>
      <td>2017/03/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q1</td>
      <td>...</td>
      <td>20010401.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>40.0</td>
      <td>4010.0</td>
      <td>401010.0</td>
      <td>40101010.0</td>
      <td>810</td>
      <td>800</td>
    </tr>
    <tr>
      <th>2385</th>
      <td>252940</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>20010401.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>40.0</td>
      <td>4010.0</td>
      <td>401010.0</td>
      <td>40101010.0</td>
      <td>810</td>
      <td>800</td>
    </tr>
    <tr>
      <th>2386</th>
      <td>252940</td>
      <td>2017/09/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q3</td>
      <td>...</td>
      <td>20010401.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>40.0</td>
      <td>4010.0</td>
      <td>401010.0</td>
      <td>40101010.0</td>
      <td>810</td>
      <td>800</td>
    </tr>
    <tr>
      <th>2387</th>
      <td>252940</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>20010401.0</td>
      <td>NaN</td>
      <td>0</td>
      <td>3</td>
      <td>40.0</td>
      <td>4010.0</td>
      <td>401010.0</td>
      <td>40101010.0</td>
      <td>810</td>
      <td>800</td>
    </tr>
  </tbody>
</table>
<p>2388 rows × 68 columns</p>
</div>




```python
links_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP</th>
      <th>PERMNO</th>
      <th>PERMCO</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>crsp_enddt</th>
      <th>link_startdt</th>
      <th>link_enddt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>84766</td>
      <td>31989</td>
      <td>20020711</td>
      <td>20110318</td>
      <td>20020102</td>
      <td>20080424</td>
      <td>20020711</td>
      <td>20080424</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>92355</td>
      <td>28711</td>
      <td>20120614</td>
      <td>20150324</td>
      <td>20071018</td>
      <td>20200722</td>
      <td>20120614</td>
      <td>20150324</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAB0</td>
      <td>84766</td>
      <td>31989</td>
      <td>20020906</td>
      <td>20110328</td>
      <td>20020102</td>
      <td>20080424</td>
      <td>20020906</td>
      <td>20080424</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAB0</td>
      <td>92355</td>
      <td>28711</td>
      <td>20120607</td>
      <td>20150217</td>
      <td>20071018</td>
      <td>20200722</td>
      <td>20120607</td>
      <td>20150217</td>
    </tr>
    <tr>
      <th>4</th>
      <td>001192AA1</td>
      <td>15553</td>
      <td>116</td>
      <td>20021206</td>
      <td>20101216</td>
      <td>20020102</td>
      <td>20090208</td>
      <td>20021206</td>
      <td>20090208</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1124</th>
      <td>961548AS3</td>
      <td>21186</td>
      <td>21913</td>
      <td>20020726</td>
      <td>20141231</td>
      <td>20020130</td>
      <td>20150701</td>
      <td>20020726</td>
      <td>20141231</td>
    </tr>
    <tr>
      <th>1125</th>
      <td>961548AS3</td>
      <td>21186</td>
      <td>21913</td>
      <td>20151112</td>
      <td>20170524</td>
      <td>20150702</td>
      <td>20200930</td>
      <td>20151112</td>
      <td>20170524</td>
    </tr>
    <tr>
      <th>1126</th>
      <td>984121CK7</td>
      <td>27983</td>
      <td>21945</td>
      <td>20150226</td>
      <td>20200828</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20150226</td>
      <td>20200828</td>
    </tr>
    <tr>
      <th>1127</th>
      <td>98934KAB6</td>
      <td>79363</td>
      <td>29908</td>
      <td>20020702</td>
      <td>20200923</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20020702</td>
      <td>20200923</td>
    </tr>
    <tr>
      <th>1128</th>
      <td>989701AU1</td>
      <td>84129</td>
      <td>5057</td>
      <td>20090731</td>
      <td>20140414</td>
      <td>19821101</td>
      <td>20200930</td>
      <td>20090731</td>
      <td>20140414</td>
    </tr>
  </tbody>
</table>
<p>1129 rows × 9 columns</p>
</div>




```python
leverge_ = pd.merge(leverage, links_data, left_on='LPERMNO', right_on='PERMNO')
```


```python
leverge_
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>SPCSECCD</th>
      <th>CUSIP</th>
      <th>PERMNO</th>
      <th>PERMCO</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>crsp_enddt</th>
      <th>link_startdt</th>
      <th>link_enddt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>15093</th>
      <td>252940</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15094</th>
      <td>252940</td>
      <td>2017/03/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q1</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15095</th>
      <td>252940</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15096</th>
      <td>252940</td>
      <td>2017/09/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q3</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15097</th>
      <td>252940</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
  </tbody>
</table>
<p>15098 rows × 77 columns</p>
</div>




```python
leverge_unique = leverge_.drop_duplicates(subset=['CUSIP', 'datadate'], keep='last')

leverge_unique
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>SPCSECCD</th>
      <th>CUSIP</th>
      <th>PERMNO</th>
      <th>PERMCO</th>
      <th>trace_startdt</th>
      <th>trace_enddt</th>
      <th>crsp_startdt</th>
      <th>crsp_enddt</th>
      <th>link_startdt</th>
      <th>link_enddt</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>925</td>
      <td>438516BK1</td>
      <td>10145</td>
      <td>22168</td>
      <td>20161024</td>
      <td>20191024</td>
      <td>20020102</td>
      <td>20200930</td>
      <td>20161024</td>
      <td>20191024</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>15093</th>
      <td>252940</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15094</th>
      <td>252940</td>
      <td>2017/03/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q1</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15095</th>
      <td>252940</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15096</th>
      <td>252940</td>
      <td>2017/09/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q3</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
    <tr>
      <th>15097</th>
      <td>252940</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>800</td>
      <td>904851AA0</td>
      <td>75811</td>
      <td>22107</td>
      <td>20120816</td>
      <td>20131203</td>
      <td>20051003</td>
      <td>20180401</td>
      <td>20120816</td>
      <td>20131203</td>
    </tr>
  </tbody>
</table>
<p>11817 rows × 77 columns</p>
</div>




```python
# read csv as pandas dataframe
# acf351b_python_data.csv
cusips_file = '../data/acf351b_python_data.csv'
cusips = pd.read_csv(cusips_file)
cusips
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>offering_amt</th>
      <th>offering_date</th>
      <th>maturity</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.7500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAB0</td>
      <td>150000.0</td>
      <td>1993-10-13</td>
      <td>2093-10-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.1250</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>001192AA1</td>
      <td>300000.0</td>
      <td>2001-02-23</td>
      <td>2011-01-14</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.1250</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>117277.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00163XAM2</td>
      <td>175000.0</td>
      <td>2006-08-10</td>
      <td>2013-08-15</td>
      <td>CMTN</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>5.9000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>351976.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00206RBS0</td>
      <td>1250000.0</td>
      <td>2013-02-07</td>
      <td>2016-02-12</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>0.7411</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>589049.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1055</th>
      <td>961548AQ7</td>
      <td>150000.0</td>
      <td>1997-03-12</td>
      <td>2027-03-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.6500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>51090.0</td>
    </tr>
    <tr>
      <th>1056</th>
      <td>961548AS3</td>
      <td>150000.0</td>
      <td>1997-06-19</td>
      <td>2027-06-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.5000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>56219.0</td>
    </tr>
    <tr>
      <th>1057</th>
      <td>984121CK7</td>
      <td>400000.0</td>
      <td>2015-02-26</td>
      <td>2020-09-01</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.7500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>626119.0</td>
    </tr>
    <tr>
      <th>1058</th>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.0000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>989701AU1</td>
      <td>34680.0</td>
      <td>2009-06-01</td>
      <td>2014-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.6500</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>498722.0</td>
    </tr>
  </tbody>
</table>
<p>1060 rows × 14 columns</p>
</div>




```python
leverge_unique_country = pd.merge(leverge_unique, cusips, left_on='CUSIP', right_on='cusip_id')
```


```python
leverge_unique_country
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11812</th>
      <td>252940</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.25000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>176262.0</td>
    </tr>
    <tr>
      <th>11813</th>
      <td>252940</td>
      <td>2017/03/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.25000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>176262.0</td>
    </tr>
    <tr>
      <th>11814</th>
      <td>252940</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.25000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>176262.0</td>
    </tr>
    <tr>
      <th>11815</th>
      <td>252940</td>
      <td>2017/09/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q3</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.25000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>176262.0</td>
    </tr>
    <tr>
      <th>11816</th>
      <td>252940</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>5.25000</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>176262.0</td>
    </tr>
  </tbody>
</table>
<p>11817 rows × 91 columns</p>
</div>




```python
# leverge_unique_country = leverge_unique_country.dropna()
leverge_unique_country = leverge_unique_country[leverge_unique_country['market_leverage'].notna()]
leverge_unique_country
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11796</th>
      <td>241637</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11798</th>
      <td>241637</td>
      <td>2016/06/30</td>
      <td>2016</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11800</th>
      <td>241637</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11802</th>
      <td>241637</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11804</th>
      <td>241637</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
  </tbody>
</table>
<p>3205 rows × 91 columns</p>
</div>




```python
leverge_unique_country = leverge_unique_country[leverge_unique_country['book_leverage'].notna()]
leverge_unique_country
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11796</th>
      <td>241637</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11798</th>
      <td>241637</td>
      <td>2016/06/30</td>
      <td>2016</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11800</th>
      <td>241637</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11802</th>
      <td>241637</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11804</th>
      <td>241637</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
  </tbody>
</table>
<p>3205 rows × 91 columns</p>
</div>




```python
leverge_unique_country
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gvkey</th>
      <th>datadate</th>
      <th>fyearq</th>
      <th>fqtr</th>
      <th>indfmt</th>
      <th>consol</th>
      <th>popsrc</th>
      <th>datafmt</th>
      <th>curcdq</th>
      <th>datacqtr</th>
      <th>...</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1300</td>
      <td>2015/03/31</td>
      <td>2015</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1300</td>
      <td>2015/06/30</td>
      <td>2015</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1300</td>
      <td>2015/09/30</td>
      <td>2015</td>
      <td>3</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q3</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1300</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1300</td>
      <td>2016/03/31</td>
      <td>2016</td>
      <td>1</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q1</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>2.54658</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>663731.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11796</th>
      <td>241637</td>
      <td>2015/12/31</td>
      <td>2015</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2015Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11798</th>
      <td>241637</td>
      <td>2016/06/30</td>
      <td>2016</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11800</th>
      <td>241637</td>
      <td>2016/12/31</td>
      <td>2016</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2016Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11802</th>
      <td>241637</td>
      <td>2017/06/30</td>
      <td>2017</td>
      <td>2</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q2</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
    <tr>
      <th>11804</th>
      <td>241637</td>
      <td>2017/12/31</td>
      <td>2017</td>
      <td>4</td>
      <td>INDL</td>
      <td>C</td>
      <td>D</td>
      <td>STD</td>
      <td>USD</td>
      <td>2017Q4</td>
      <td>...</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>1.07567</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>605853.0</td>
    </tr>
  </tbody>
</table>
<p>3205 rows × 91 columns</p>
</div>




```python
leverge_unique_country.to_csv('../data/export/part1c_leverge.csv')
```

#### 💲4. Locate the latest credit rating


```python
# monthly yields data got in Part1(a)
yields_median_usa_gbr
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>cusip_id</th>
      <th>offering_amt</th>
      <th>offering_date</th>
      <th>maturity</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 19 columns</p>
</div>




```python
# read csv as pandas dataframe
# acf351b_python_data.csv
cusips_file = '../data/acf351b_python_data.csv'
cusips = pd.read_csv(cusips_file, usecols=[0, 13])
cusips
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAB0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>001192AA1</td>
      <td>117277.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00163XAM2</td>
      <td>351976.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00206RBS0</td>
      <td>589049.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1055</th>
      <td>961548AQ7</td>
      <td>51090.0</td>
    </tr>
    <tr>
      <th>1056</th>
      <td>961548AS3</td>
      <td>56219.0</td>
    </tr>
    <tr>
      <th>1057</th>
      <td>984121CK7</td>
      <td>626119.0</td>
    </tr>
    <tr>
      <th>1058</th>
      <td>98934KAB6</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>989701AU1</td>
      <td>498722.0</td>
    </tr>
  </tbody>
</table>
<p>1060 rows × 2 columns</p>
</div>




```python
cusips = cusips.sort_values(by=['issue_id'])
# remove cusip 40056E6B9 beacuse it lose issus_id data
cusips.dropna(inplace=True)
cusips.issue_id.astype(np.int64)
cusips
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAB0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>40</th>
      <td>030955AB4</td>
      <td>1057.0</td>
    </tr>
    <tr>
      <th>128</th>
      <td>126168AB9</td>
      <td>3024.0</td>
    </tr>
    <tr>
      <th>391</th>
      <td>386088AB4</td>
      <td>11624.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>811</th>
      <td>61769HDQ5</td>
      <td>830907.0</td>
    </tr>
    <tr>
      <th>966</th>
      <td>80283LAX1</td>
      <td>832065.0</td>
    </tr>
    <tr>
      <th>614</th>
      <td>40056FJX4</td>
      <td>832139.0</td>
    </tr>
    <tr>
      <th>615</th>
      <td>40056FKS3</td>
      <td>834537.0</td>
    </tr>
    <tr>
      <th>846</th>
      <td>674599CT0</td>
      <td>843393.0</td>
    </tr>
  </tbody>
</table>
<p>1059 rows × 2 columns</p>
</div>




```python
# read csv as pandas dataframe
# acf351b_ratings.csv
rating_file = '../data/acf351b_ratings.csv'
ratings = pd.read_csv(rating_file)
ratings
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>issue_id</th>
      <th>rating_type</th>
      <th>rating_date</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>DPR</td>
      <td>5/20/1993</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>MR</td>
      <td>5/24/2017</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>FR</td>
      <td>12/14/2018</td>
      <td>A-</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>SPR</td>
      <td>5/16/2019</td>
      <td>BB+</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>DPR</td>
      <td>10/13/1993</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3231</th>
      <td>834537</td>
      <td>FR</td>
      <td>6/25/2019</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>3232</th>
      <td>834537</td>
      <td>MR</td>
      <td>8/1/2019</td>
      <td>A3</td>
    </tr>
    <tr>
      <th>3233</th>
      <td>843393</td>
      <td>MR</td>
      <td>8/1/2019</td>
      <td>Baa3</td>
    </tr>
    <tr>
      <th>3234</th>
      <td>843393</td>
      <td>FR</td>
      <td>8/6/2019</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>3235</th>
      <td>843393</td>
      <td>SPR</td>
      <td>8/8/2019</td>
      <td>BBB</td>
    </tr>
  </tbody>
</table>
<p>3236 rows × 4 columns</p>
</div>




```python
# change dtype of rating_date from string to date
ratings['rating_date'] = pd.to_datetime(ratings['rating_date'])
ratings
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>issue_id</th>
      <th>rating_type</th>
      <th>rating_date</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5</td>
      <td>DPR</td>
      <td>1993-05-20</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>MR</td>
      <td>2017-05-24</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5</td>
      <td>FR</td>
      <td>2018-12-14</td>
      <td>A-</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td>SPR</td>
      <td>2019-05-16</td>
      <td>BB+</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>DPR</td>
      <td>1993-10-13</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3231</th>
      <td>834537</td>
      <td>FR</td>
      <td>2019-06-25</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>3232</th>
      <td>834537</td>
      <td>MR</td>
      <td>2019-08-01</td>
      <td>A3</td>
    </tr>
    <tr>
      <th>3233</th>
      <td>843393</td>
      <td>MR</td>
      <td>2019-08-01</td>
      <td>Baa3</td>
    </tr>
    <tr>
      <th>3234</th>
      <td>843393</td>
      <td>FR</td>
      <td>2019-08-06</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>3235</th>
      <td>843393</td>
      <td>SPR</td>
      <td>2019-08-08</td>
      <td>BBB</td>
    </tr>
  </tbody>
</table>
<p>3236 rows × 4 columns</p>
</div>




```python
# merge two dataframe by outer join
ratings_of_cusips = pd.merge(cusips, ratings, how='outer', on ='issue_id')
```


```python
ratings_of_cusips
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>issue_id</th>
      <th>rating_type</th>
      <th>rating_date</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>5.0</td>
      <td>DPR</td>
      <td>1993-05-20</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>5.0</td>
      <td>MR</td>
      <td>2017-05-24</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>5.0</td>
      <td>FR</td>
      <td>2018-12-14</td>
      <td>A-</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>5.0</td>
      <td>SPR</td>
      <td>2019-05-16</td>
      <td>BB+</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAB0</td>
      <td>6.0</td>
      <td>DPR</td>
      <td>1993-10-13</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3231</th>
      <td>674599CT0</td>
      <td>843393.0</td>
      <td>FR</td>
      <td>2019-08-06</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>3232</th>
      <td>674599CT0</td>
      <td>843393.0</td>
      <td>SPR</td>
      <td>2019-08-08</td>
      <td>BBB</td>
    </tr>
    <tr>
      <th>3233</th>
      <td>NaN</td>
      <td>785195.0</td>
      <td>SPR</td>
      <td>2018-10-26</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>3234</th>
      <td>NaN</td>
      <td>785195.0</td>
      <td>FR</td>
      <td>2018-10-26</td>
      <td>NR</td>
    </tr>
    <tr>
      <th>3235</th>
      <td>NaN</td>
      <td>785195.0</td>
      <td>MR</td>
      <td>2019-05-16</td>
      <td>A3</td>
    </tr>
  </tbody>
</table>
<p>3236 rows × 5 columns</p>
</div>




```python
# test
# get the cusio_id of each row
for row in yields_median_usa_gbr.iterrows():
    print(row[1]['CUSIP_ID'])
    break
```

    00077TAA2



```python
# test
# locate the ratings of yield row
for row in yields_median_usa_gbr.iterrows():
    ratings_of_row =  ratings_of_cusips.loc[ratings_of_cusips['cusip_id'] == row[1]['CUSIP_ID']]
    date_of_row = row[1]['trd_exctn_dt']
    break
print(ratings_of_row)
```

        cusip_id  issue_id rating_type rating_date rating
    0  00077TAA2       5.0         DPR  1993-05-20     NR
    1  00077TAA2       5.0          MR  2017-05-24     NR
    2  00077TAA2       5.0          FR  2018-12-14     A-
    3  00077TAA2       5.0         SPR  2019-05-16    BB+



```python
# test
# get the latest credit ratings
print(ratings_of_row['rating_date'].sort_values())
print(date_of_row)
ind = ratings_of_row['rating_date'].sort_values().searchsorted(date_of_row)
ind-1
```

    0   1993-05-20
    1   2017-05-24
    2   2018-12-14
    3   2019-05-16
    Name: rating_date, dtype: datetime64[ns]
    2015-01-26 00:00:00





    0




```python
# the monthly yield data generate in part1(a)
yields_median_usa_gbr
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>cusip_id</th>
      <th>offering_amt</th>
      <th>offering_date</th>
      <th>maturity</th>
      <th>bond_type</th>
      <th>security_level</th>
      <th>yankee</th>
      <th>country_domicile</th>
      <th>coupon</th>
      <th>asset_backed</th>
      <th>putable</th>
      <th>convertible</th>
      <th>callable</th>
      <th>issue_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>00077TAA2</td>
      <td>250000.0</td>
      <td>1993-05-20</td>
      <td>2023-05-15</td>
      <td>CDEB</td>
      <td>SUB</td>
      <td>N</td>
      <td>USA</td>
      <td>7.75</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>98934KAB6</td>
      <td>300000.0</td>
      <td>1993-11-09</td>
      <td>2023-11-15</td>
      <td>CDEB</td>
      <td>SEN</td>
      <td>N</td>
      <td>USA</td>
      <td>7.00</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>N</td>
      <td>24061.0</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 19 columns</p>
</div>




```python
from datetime import datetime
# get the latest rating level for each row in monthly yield data
ratings = []
for row in yields_median_usa_gbr.iterrows():
    # get the ratings of row from ratings_of_cusips
    ratings_of_row =  ratings_of_cusips.loc[ratings_of_cusips['cusip_id'] == row[1]['CUSIP_ID']]
    # get trd_exctn_dt of the row as "date_of_row"
    date_of_row = row[1]['trd_exctn_dt']
    # locate the latest rating
    ind_to_insert = ratings_of_row['rating_date'].sort_values().searchsorted(date_of_row)
    # get the latest rating from "ratings_of_row"
    rating_of_row = ratings_of_row.iloc[ind_to_insert - 1]['rating']
    # get the rating type of latest rating from "ratings_of_row"
    ratetype_of_row = ratings_of_row.iloc[ind_to_insert - 1]['rating_type']
    # get the rating date of latest rating from "ratings_of_row"
    ratedate_of_row = ratings_of_row.iloc[ind_to_insert - 1]['rating_date']
    # get cusip_id of the row
    cusip_of_row = row[1]['CUSIP_ID']
    # get the date of the row
    trd_exctn_dt = row[1]['trd_exctn_dt']
    # country of row
    country = row[1]['country_domicile']
    ratings.append({'cusip' : cusip_of_row , 'trd_exctn_dt': trd_exctn_dt, 'country': country, 'rating type': ratetype_of_row,
                    'rateing date': ratedate_of_row,  'rating' : rating_of_row})
```


```python
# check results
# the length of ratings list is equal to the length of monthly yield dataframe
len(ratings)
```




    11177




```python
ratings[0]
```




    {'cusip': '00077TAA2',
     'trd_exctn_dt': Timestamp('2015-01-26 00:00:00'),
     'country': 'USA',
     'rating type': 'DPR',
     'rateing date': Timestamp('1993-05-20 00:00:00'),
     'rating': 'NR'}




```python
# write results
import csv

with open('../data/export/ratings_with_country.csv', 'w') as f:  # You will need 'wb' mode in Python 2.x
    for i, d in enumerate(ratings):
        w = csv.DictWriter(f, d.keys())
        if i == 0:
            w.writeheader()
        w.writerow(d)
```

#### 5. Compute monthly credit

##### 5.1 Time to maturity

Credit spread

譯自英文-

在金融中，信用利差或淨信用利差是一種期權策略，它涉及購買一種期權和出售另一種期權，它們具有相同的等級和到期日，但執行價格不同。它的目的是賺取利潤時，這兩個選項之間的價差縮小。投資者在進入頭寸時獲得淨信用，並希望價差縮小或到期以獲取利潤。相反，投資者必須付費才能輸入債務價差。 

维基百科（英文)

What Is a Maturity Date?

The maturity date is the date on which the principal amount of a note, draft, acceptance bond or other debt instrument becomes due. On this date, which is generally printed on the certificate of the instrument in question, the principal investment is repaid to the investor, while the interest payments that were regularly paid out during the life of the bond, cease to roll in. The maturity date also refers to the termination date (due date) on which an installment loan must be paid back in full.

ref: https://www.investopedia.com/terms/m/maturitydate.asp


```python
# read csv as pandas dataframe
# acf351b_python_data.csv
cusips_file = '../data/acf351b_python_data.csv'
cusips = pd.read_csv(cusips_file, usecols=[0, 3, 7])
cusips
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAB0</td>
      <td>2093-10-15</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>001192AA1</td>
      <td>2011-01-14</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00163XAM2</td>
      <td>2013-08-15</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00206RBS0</td>
      <td>2016-02-12</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1055</th>
      <td>961548AQ7</td>
      <td>2027-03-15</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>1056</th>
      <td>961548AS3</td>
      <td>2027-06-15</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>1057</th>
      <td>984121CK7</td>
      <td>2020-09-01</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>1058</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>989701AU1</td>
      <td>2014-05-15</td>
      <td>USA</td>
    </tr>
  </tbody>
</table>
<p>1060 rows × 3 columns</p>
</div>




```python
# the bond transaction data from Part1(a)
yields_median
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>cusip_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1198533</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>1198535</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>111592</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>111594</th>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>111597</th>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>56809</th>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56840</th>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56855</th>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56862</th>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56881</th>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>98934KAB6</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 6 columns</p>
</div>




```python
yields_median['cusip_id'] = yields_median['CUSIP_ID']
yields_median
```

    <ipython-input-278-c026565aa96d>:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      yields_median['cusip_id'] = yields_median['CUSIP_ID']





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>cusip_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1198533</th>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>1198535</th>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>111592</th>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>111594</th>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>111597</th>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>00077TAA2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>56809</th>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56840</th>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56855</th>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56862</th>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>98934KAB6</td>
    </tr>
    <tr>
      <th>56881</th>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>98934KAB6</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 6 columns</p>
</div>




```python
# merge two dataframe by inner join
transactions_maturity = pd.merge(cusips, yields_median, how='inner', on ='cusip_id')
```


```python
transactions_maturity
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 8 columns</p>
</div>




```python
transactions_maturity.dtypes
```




    cusip_id                    object
    maturity                    object
    country_domicile            object
    CUSIP_ID                    object
    trd_exctn_dt        datetime64[ns]
    trd_exctn_tm                object
    yld_pt                     float64
    year_month               period[M]
    dtype: object




```python
# transform maturity to datetime
transactions_maturity['maturity'] = pd.to_datetime(transactions_maturity['maturity'])
```


```python
transactions_maturity.dtypes
```




    cusip_id                    object
    maturity            datetime64[ns]
    country_domicile            object
    CUSIP_ID                    object
    trd_exctn_dt        datetime64[ns]
    trd_exctn_tm                object
    yld_pt                     float64
    year_month               period[M]
    dtype: object




```python
# get 'time to maturity' of dt.days type
transactions_maturity['time_to_maturity'] = transactions_maturity['maturity'] - transactions_maturity['trd_exctn_dt']
# transform to int type
transactions_maturity['time_to_maturity'] = transactions_maturity['time_to_maturity'].dt.days
# transform to year
transactions_maturity['time_to_maturity'] = transactions_maturity['time_to_maturity'] / 365.25
# round to 2 decimals
transactions_maturity['time_to_maturity'] = np.around(transactions_maturity['time_to_maturity'], 2)
```


```python
transactions_maturity
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>time_to_maturity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>8.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>8.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>8.04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>7.73</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>6.21</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>6.14</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>6.06</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>5.98</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>5.91</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 9 columns</p>
</div>



##### 5.2 Zero-coupon yield

百度百科：零息债券收益率（Zero-coupon yield）


```python
transactions_maturity
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>time_to_maturity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>8.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>8.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>8.04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>7.73</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>6.21</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>6.14</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>6.06</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>5.98</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>5.91</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 9 columns</p>
</div>




```python
# read zero coupon file
zero_coupon_file = '../data/feds200628.csv'
zero_coupon = pd.read_csv(zero_coupon_file, skiprows=9, usecols=list(range(31)))
```


```python
# get the columns of the dataframe
zero_coupon.columns
```




    Index(['Unnamed: 0', 'SVENY01', 'SVENY02', 'SVENY03', 'SVENY04', 'SVENY05',
           'SVENY06', 'SVENY07', 'SVENY08', 'SVENY09', 'SVENY10', 'SVENY11',
           'SVENY12', 'SVENY13', 'SVENY14', 'SVENY15', 'SVENY16', 'SVENY17',
           'SVENY18', 'SVENY19', 'SVENY20', 'SVENY21', 'SVENY22', 'SVENY23',
           'SVENY24', 'SVENY25', 'SVENY26', 'SVENY27', 'SVENY28', 'SVENY29',
           'SVENY30'],
          dtype='object')




```python
# rename the unnamed date column
zero_coupon = zero_coupon.rename(columns={'Unnamed: 0': 'date'})
```


```python
zero_coupon.dtypes
```




    date        object
    SVENY01    float64
    SVENY02    float64
    SVENY03    float64
    SVENY04    float64
    SVENY05    float64
    SVENY06    float64
    SVENY07    float64
    SVENY08    float64
    SVENY09    float64
    SVENY10    float64
    SVENY11    float64
    SVENY12    float64
    SVENY13    float64
    SVENY14    float64
    SVENY15    float64
    SVENY16    float64
    SVENY17    float64
    SVENY18    float64
    SVENY19    float64
    SVENY20    float64
    SVENY21    float64
    SVENY22    float64
    SVENY23    float64
    SVENY24    float64
    SVENY25    float64
    SVENY26    float64
    SVENY27    float64
    SVENY28    float64
    SVENY29    float64
    SVENY30    float64
    dtype: object




```python
zero_coupon['date'] = pd.to_datetime(zero_coupon['date'])
```


```python
zero_coupon.dtypes
```




    date       datetime64[ns]
    SVENY01           float64
    SVENY02           float64
    SVENY03           float64
    SVENY04           float64
    SVENY05           float64
    SVENY06           float64
    SVENY07           float64
    SVENY08           float64
    SVENY09           float64
    SVENY10           float64
    SVENY11           float64
    SVENY12           float64
    SVENY13           float64
    SVENY14           float64
    SVENY15           float64
    SVENY16           float64
    SVENY17           float64
    SVENY18           float64
    SVENY19           float64
    SVENY20           float64
    SVENY21           float64
    SVENY22           float64
    SVENY23           float64
    SVENY24           float64
    SVENY25           float64
    SVENY26           float64
    SVENY27           float64
    SVENY28           float64
    SVENY29           float64
    SVENY30           float64
    dtype: object




```python
transactions_maturity.dtypes
```




    cusip_id                    object
    maturity            datetime64[ns]
    country_domicile            object
    CUSIP_ID                    object
    trd_exctn_dt        datetime64[ns]
    trd_exctn_tm                object
    yld_pt                     float64
    year_month               period[M]
    time_to_maturity           float64
    dtype: object




```python
# transactions_maturity['zero_coupon'] =
# loc = zero_coupon.loc[zero_coupon['date'] == transactions_maturity['trd_exctn_dt']][round(transactions_maturity['time_to_maturity'])]
# loc = zero_coupon.loc[zero_coupon['date'] == transactions_maturity['trd_exctn_dt']]
# zero_coupon['date']
# transactions_maturity['trd_exctn_dt']
```


```python
# merge two dataframe by left join
transactions_zerocoupon = pd.merge(transactions_maturity, zero_coupon, how='left', right_on ='date', left_on='trd_exctn_dt')
```


```python
# sort rows
transactions_zerocoupon.sort_values(by=['cusip_id', 'year_month'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>time_to_maturity</th>
      <th>date</th>
      <th>...</th>
      <th>SVENY21</th>
      <th>SVENY22</th>
      <th>SVENY23</th>
      <th>SVENY24</th>
      <th>SVENY25</th>
      <th>SVENY26</th>
      <th>SVENY27</th>
      <th>SVENY28</th>
      <th>SVENY29</th>
      <th>SVENY30</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>8.30</td>
      <td>2015-01-26</td>
      <td>...</td>
      <td>2.3417</td>
      <td>2.3649</td>
      <td>2.3866</td>
      <td>2.4067</td>
      <td>2.4255</td>
      <td>2.4430</td>
      <td>2.4594</td>
      <td>2.4748</td>
      <td>2.4893</td>
      <td>2.5028</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>8.14</td>
      <td>2015-03-24</td>
      <td>...</td>
      <td>2.4235</td>
      <td>2.4491</td>
      <td>2.4731</td>
      <td>2.4957</td>
      <td>2.5168</td>
      <td>2.5367</td>
      <td>2.5553</td>
      <td>2.5729</td>
      <td>2.5895</td>
      <td>2.6052</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>8.04</td>
      <td>2015-05-01</td>
      <td>...</td>
      <td>2.7832</td>
      <td>2.8154</td>
      <td>2.8459</td>
      <td>2.8746</td>
      <td>2.9018</td>
      <td>2.9276</td>
      <td>2.9520</td>
      <td>2.9751</td>
      <td>2.9970</td>
      <td>3.0179</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>7.80</td>
      <td>2015-07-27</td>
      <td>...</td>
      <td>2.8422</td>
      <td>2.8854</td>
      <td>2.9288</td>
      <td>2.9722</td>
      <td>3.0157</td>
      <td>3.0591</td>
      <td>3.1025</td>
      <td>3.1456</td>
      <td>3.1886</td>
      <td>3.2312</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>7.73</td>
      <td>2015-08-20</td>
      <td>...</td>
      <td>2.6613</td>
      <td>2.6985</td>
      <td>2.7355</td>
      <td>2.7723</td>
      <td>2.8089</td>
      <td>2.8453</td>
      <td>2.8815</td>
      <td>2.9173</td>
      <td>2.9529</td>
      <td>2.9880</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>6.21</td>
      <td>2017-08-30</td>
      <td>...</td>
      <td>2.6519</td>
      <td>2.6866</td>
      <td>2.7208</td>
      <td>2.7544</td>
      <td>2.7875</td>
      <td>2.8199</td>
      <td>2.8517</td>
      <td>2.8829</td>
      <td>2.9135</td>
      <td>2.9434</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>6.14</td>
      <td>2017-09-26</td>
      <td>...</td>
      <td>2.6849</td>
      <td>2.7176</td>
      <td>2.7500</td>
      <td>2.7821</td>
      <td>2.8139</td>
      <td>2.8452</td>
      <td>2.8762</td>
      <td>2.9066</td>
      <td>2.9366</td>
      <td>2.9661</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>6.06</td>
      <td>2017-10-24</td>
      <td>...</td>
      <td>2.8288</td>
      <td>2.8605</td>
      <td>2.8922</td>
      <td>2.9239</td>
      <td>2.9557</td>
      <td>2.9874</td>
      <td>3.0191</td>
      <td>3.0506</td>
      <td>3.0819</td>
      <td>3.1129</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>5.98</td>
      <td>2017-11-22</td>
      <td>...</td>
      <td>2.6742</td>
      <td>2.6985</td>
      <td>2.7227</td>
      <td>2.7467</td>
      <td>2.7706</td>
      <td>2.7944</td>
      <td>2.8180</td>
      <td>2.8414</td>
      <td>2.8646</td>
      <td>2.8877</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>5.91</td>
      <td>2017-12-19</td>
      <td>...</td>
      <td>2.7453</td>
      <td>2.7672</td>
      <td>2.7896</td>
      <td>2.8125</td>
      <td>2.8357</td>
      <td>2.8593</td>
      <td>2.8833</td>
      <td>2.9075</td>
      <td>2.9320</td>
      <td>2.9566</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 40 columns</p>
</div>




```python
# test format
year = f'SVENY{round(8.30):02d}'
year
```




    'SVENY08'




```python
transactions_zerocoupon['zero_coupon'] = transactions_zerocoupon[f"SVENY{round(transactions_zerocoupon['time_to_maturity']):02d}"]
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-298-066c4c5b005f> in <module>
    ----> 1 transactions_zerocoupon['zero_coupon'] = transactions_zerocoupon[f"SVENY{round(transactions_zerocoupon['time_to_maturity']):02d}"]
    

    TypeError: unsupported format string passed to Series.__format__



```python
transactions_zerocoupon.columns
```




    Index(['cusip_id', 'maturity', 'country_domicile', 'CUSIP_ID', 'trd_exctn_dt',
           'trd_exctn_tm', 'yld_pt', 'year_month', 'time_to_maturity', 'date',
           'SVENY01', 'SVENY02', 'SVENY03', 'SVENY04', 'SVENY05', 'SVENY06',
           'SVENY07', 'SVENY08', 'SVENY09', 'SVENY10', 'SVENY11', 'SVENY12',
           'SVENY13', 'SVENY14', 'SVENY15', 'SVENY16', 'SVENY17', 'SVENY18',
           'SVENY19', 'SVENY20', 'SVENY21', 'SVENY22', 'SVENY23', 'SVENY24',
           'SVENY25', 'SVENY26', 'SVENY27', 'SVENY28', 'SVENY29', 'SVENY30'],
          dtype='object')




```python
transactions_zerocoupon[transactions_zerocoupon.columns[10]]
```




    0        0.2029
    1        0.3018
    2        0.2832
    3        0.3333
    4        0.4325
              ...  
    11172    1.2249
    11173    1.3007
    11174    1.4183
    11175    1.5927
    11176    1.7084
    Name: SVENY01, Length: 11177, dtype: float64




```python
transactions_zerocoupon['time_to_maturity'].max()
```




    82.33




```python
# round to the closed year
transactions_zerocoupon['year'] = transactions_zerocoupon['time_to_maturity'].transform(lambda x : 30 if x > 29 else (x + 1 if x == 0 or not x.is_integer() else x))
```


```python
# some test samples of the above lambda function
'''

x      function(x)

0      1
0.3    1.3
0.5    1.5
1      1
1.3    2.3
2      2
5.     5
9.04   10.04
29     29
29.1   30
30     30
31     30

'''
```




    '\n\nx      function(x)\n\n0      1\n0.3    1.3\n0.5    1.5\n1      1\n1.3    2.3\n2      2\n5.     5\n9.04   10.04\n29     29\n29.1   30\n30     30\n31     30\n\n'




```python
transactions_zerocoupon['year'].min()
```




    1.0




```python
# transactions_zerocoupon['year'] = transactions_zerocoupon['year'].transform(lambda x: 1 if x < 0 else x)
```


```python

```


```python
transactions_zerocoupon
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>time_to_maturity</th>
      <th>date</th>
      <th>...</th>
      <th>SVENY22</th>
      <th>SVENY23</th>
      <th>SVENY24</th>
      <th>SVENY25</th>
      <th>SVENY26</th>
      <th>SVENY27</th>
      <th>SVENY28</th>
      <th>SVENY29</th>
      <th>SVENY30</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>8.30</td>
      <td>2015-01-26</td>
      <td>...</td>
      <td>2.3649</td>
      <td>2.3866</td>
      <td>2.4067</td>
      <td>2.4255</td>
      <td>2.4430</td>
      <td>2.4594</td>
      <td>2.4748</td>
      <td>2.4893</td>
      <td>2.5028</td>
      <td>9.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>8.14</td>
      <td>2015-03-24</td>
      <td>...</td>
      <td>2.4491</td>
      <td>2.4731</td>
      <td>2.4957</td>
      <td>2.5168</td>
      <td>2.5367</td>
      <td>2.5553</td>
      <td>2.5729</td>
      <td>2.5895</td>
      <td>2.6052</td>
      <td>9.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>8.04</td>
      <td>2015-05-01</td>
      <td>...</td>
      <td>2.8154</td>
      <td>2.8459</td>
      <td>2.8746</td>
      <td>2.9018</td>
      <td>2.9276</td>
      <td>2.9520</td>
      <td>2.9751</td>
      <td>2.9970</td>
      <td>3.0179</td>
      <td>9.04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>7.80</td>
      <td>2015-07-27</td>
      <td>...</td>
      <td>2.8854</td>
      <td>2.9288</td>
      <td>2.9722</td>
      <td>3.0157</td>
      <td>3.0591</td>
      <td>3.1025</td>
      <td>3.1456</td>
      <td>3.1886</td>
      <td>3.2312</td>
      <td>8.80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>7.73</td>
      <td>2015-08-20</td>
      <td>...</td>
      <td>2.6985</td>
      <td>2.7355</td>
      <td>2.7723</td>
      <td>2.8089</td>
      <td>2.8453</td>
      <td>2.8815</td>
      <td>2.9173</td>
      <td>2.9529</td>
      <td>2.9880</td>
      <td>8.73</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>6.21</td>
      <td>2017-08-30</td>
      <td>...</td>
      <td>2.6866</td>
      <td>2.7208</td>
      <td>2.7544</td>
      <td>2.7875</td>
      <td>2.8199</td>
      <td>2.8517</td>
      <td>2.8829</td>
      <td>2.9135</td>
      <td>2.9434</td>
      <td>7.21</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>6.14</td>
      <td>2017-09-26</td>
      <td>...</td>
      <td>2.7176</td>
      <td>2.7500</td>
      <td>2.7821</td>
      <td>2.8139</td>
      <td>2.8452</td>
      <td>2.8762</td>
      <td>2.9066</td>
      <td>2.9366</td>
      <td>2.9661</td>
      <td>7.14</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>6.06</td>
      <td>2017-10-24</td>
      <td>...</td>
      <td>2.8605</td>
      <td>2.8922</td>
      <td>2.9239</td>
      <td>2.9557</td>
      <td>2.9874</td>
      <td>3.0191</td>
      <td>3.0506</td>
      <td>3.0819</td>
      <td>3.1129</td>
      <td>7.06</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>5.98</td>
      <td>2017-11-22</td>
      <td>...</td>
      <td>2.6985</td>
      <td>2.7227</td>
      <td>2.7467</td>
      <td>2.7706</td>
      <td>2.7944</td>
      <td>2.8180</td>
      <td>2.8414</td>
      <td>2.8646</td>
      <td>2.8877</td>
      <td>6.98</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>5.91</td>
      <td>2017-12-19</td>
      <td>...</td>
      <td>2.7672</td>
      <td>2.7896</td>
      <td>2.8125</td>
      <td>2.8357</td>
      <td>2.8593</td>
      <td>2.8833</td>
      <td>2.9075</td>
      <td>2.9320</td>
      <td>2.9566</td>
      <td>6.91</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 41 columns</p>
</div>




```python
# 事先创建“zero_coupon”列，来避免“Wrong number of items passed 11177, placement implies 1”错误
transactions_zerocoupon['zero_coupon'] = 0
```


```python
# For each bond issue and trade, locate the zero-coupon yield of US treasury with the time to maturity closest to the bond issue’s.
transactions_zerocoupon['zero_coupon'] = transactions_zerocoupon[transactions_zerocoupon.columns[transactions_zerocoupon['year'].astype(int) + 8]]
```


```python
transactions_zerocoupon['year']
```




    0        9.30
    1        9.14
    2        9.04
    3        8.80
    4        8.73
             ... 
    11172    7.21
    11173    7.14
    11174    7.06
    11175    6.98
    11176    6.91
    Name: year, Length: 11177, dtype: float64



##### 5.3 Credit spreads


```python
# take the difference between the yields of the bond issue and the zero-coupon yield and the result is the credit spreads.
transactions_zerocoupon['credit_spreads'] = transactions_zerocoupon['yld_pt'] - transactions_zerocoupon['zero_coupon']
```


```python
transactions_zerocoupon
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>time_to_maturity</th>
      <th>date</th>
      <th>...</th>
      <th>SVENY24</th>
      <th>SVENY25</th>
      <th>SVENY26</th>
      <th>SVENY27</th>
      <th>SVENY28</th>
      <th>SVENY29</th>
      <th>SVENY30</th>
      <th>year</th>
      <th>zero_coupon</th>
      <th>credit_spreads</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-01-26</td>
      <td>16:01:58</td>
      <td>NaN</td>
      <td>2015-01</td>
      <td>8.30</td>
      <td>2015-01-26</td>
      <td>...</td>
      <td>2.4067</td>
      <td>2.4255</td>
      <td>2.4430</td>
      <td>2.4594</td>
      <td>2.4748</td>
      <td>2.4893</td>
      <td>2.5028</td>
      <td>9.30</td>
      <td>1.7586</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-03-24</td>
      <td>16:37:01</td>
      <td>NaN</td>
      <td>2015-03</td>
      <td>8.14</td>
      <td>2015-03-24</td>
      <td>...</td>
      <td>2.4957</td>
      <td>2.5168</td>
      <td>2.5367</td>
      <td>2.5553</td>
      <td>2.5729</td>
      <td>2.5895</td>
      <td>2.6052</td>
      <td>9.14</td>
      <td>1.7968</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-05-01</td>
      <td>11:03:37</td>
      <td>NaN</td>
      <td>2015-05</td>
      <td>8.04</td>
      <td>2015-05-01</td>
      <td>...</td>
      <td>2.8746</td>
      <td>2.9018</td>
      <td>2.9276</td>
      <td>2.9520</td>
      <td>2.9751</td>
      <td>2.9970</td>
      <td>3.0179</td>
      <td>9.04</td>
      <td>2.0255</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-07-27</td>
      <td>9:14:28</td>
      <td>NaN</td>
      <td>2015-07</td>
      <td>7.80</td>
      <td>2015-07-27</td>
      <td>...</td>
      <td>2.9722</td>
      <td>3.0157</td>
      <td>3.0591</td>
      <td>3.1025</td>
      <td>3.1456</td>
      <td>3.1886</td>
      <td>3.2312</td>
      <td>8.80</td>
      <td>2.1064</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00077TAA2</td>
      <td>2023-05-15</td>
      <td>USA</td>
      <td>00077TAA2</td>
      <td>2015-08-20</td>
      <td>12:06:06</td>
      <td>NaN</td>
      <td>2015-08</td>
      <td>7.73</td>
      <td>2015-08-20</td>
      <td>...</td>
      <td>2.7723</td>
      <td>2.8089</td>
      <td>2.8453</td>
      <td>2.8815</td>
      <td>2.9173</td>
      <td>2.9529</td>
      <td>2.9880</td>
      <td>8.73</td>
      <td>1.987</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>6.21</td>
      <td>2017-08-30</td>
      <td>...</td>
      <td>2.7544</td>
      <td>2.7875</td>
      <td>2.8199</td>
      <td>2.8517</td>
      <td>2.8829</td>
      <td>2.9135</td>
      <td>2.9434</td>
      <td>7.21</td>
      <td>2.0507</td>
      <td>0.67949</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>6.14</td>
      <td>2017-09-26</td>
      <td>...</td>
      <td>2.7821</td>
      <td>2.8139</td>
      <td>2.8452</td>
      <td>2.8762</td>
      <td>2.9066</td>
      <td>2.9366</td>
      <td>2.9661</td>
      <td>7.14</td>
      <td>2.1521</td>
      <td>0.70636</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>6.06</td>
      <td>2017-10-24</td>
      <td>...</td>
      <td>2.9239</td>
      <td>2.9557</td>
      <td>2.9874</td>
      <td>3.0191</td>
      <td>3.0506</td>
      <td>3.0819</td>
      <td>3.1129</td>
      <td>7.06</td>
      <td>2.3256</td>
      <td>0.629487</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>5.98</td>
      <td>2017-11-22</td>
      <td>...</td>
      <td>2.7467</td>
      <td>2.7706</td>
      <td>2.7944</td>
      <td>2.8180</td>
      <td>2.8414</td>
      <td>2.8646</td>
      <td>2.8877</td>
      <td>6.98</td>
      <td>2.2634</td>
      <td>0.672886</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>5.91</td>
      <td>2017-12-19</td>
      <td>...</td>
      <td>2.8125</td>
      <td>2.8357</td>
      <td>2.8593</td>
      <td>2.8833</td>
      <td>2.9075</td>
      <td>2.9320</td>
      <td>2.9566</td>
      <td>6.91</td>
      <td>2.41</td>
      <td>0.550962</td>
    </tr>
  </tbody>
</table>
<p>11177 rows × 43 columns</p>
</div>




```python
# drop掉包含nan的行
# transactions_zerocoupon = transactions_zerocoupon.dropna()
transactions_zerocoupon = transactions_zerocoupon[transactions_zerocoupon['zero_coupon'].notna()]
transactions_zerocoupon = transactions_zerocoupon[transactions_zerocoupon['yld_pt'].notna()]



```


```python
transactions_zerocoupon
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cusip_id</th>
      <th>maturity</th>
      <th>country_domicile</th>
      <th>CUSIP_ID</th>
      <th>trd_exctn_dt</th>
      <th>trd_exctn_tm</th>
      <th>yld_pt</th>
      <th>year_month</th>
      <th>time_to_maturity</th>
      <th>date</th>
      <th>...</th>
      <th>SVENY24</th>
      <th>SVENY25</th>
      <th>SVENY26</th>
      <th>SVENY27</th>
      <th>SVENY28</th>
      <th>SVENY29</th>
      <th>SVENY30</th>
      <th>year</th>
      <th>zero_coupon</th>
      <th>credit_spreads</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>21</th>
      <td>00077TAB0</td>
      <td>2093-10-15</td>
      <td>USA</td>
      <td>00077TAB0</td>
      <td>2015-01-05</td>
      <td>14:27:45</td>
      <td>6.525827</td>
      <td>2015-01</td>
      <td>78.78</td>
      <td>2015-01-05</td>
      <td>...</td>
      <td>2.5902</td>
      <td>2.6174</td>
      <td>2.6438</td>
      <td>2.6694</td>
      <td>2.6942</td>
      <td>2.7183</td>
      <td>2.7415</td>
      <td>30.00</td>
      <td>1.964</td>
      <td>4.56183</td>
    </tr>
    <tr>
      <th>22</th>
      <td>00077TAB0</td>
      <td>2093-10-15</td>
      <td>USA</td>
      <td>00077TAB0</td>
      <td>2015-02-17</td>
      <td>11:24:15</td>
      <td>6.897267</td>
      <td>2015-02</td>
      <td>78.66</td>
      <td>2015-02-17</td>
      <td>...</td>
      <td>2.7596</td>
      <td>2.7781</td>
      <td>2.7953</td>
      <td>2.8114</td>
      <td>2.8264</td>
      <td>2.8405</td>
      <td>2.8537</td>
      <td>30.00</td>
      <td>2.0779</td>
      <td>4.81937</td>
    </tr>
    <tr>
      <th>23</th>
      <td>00077TAB0</td>
      <td>2093-10-15</td>
      <td>USA</td>
      <td>00077TAB0</td>
      <td>2015-03-31</td>
      <td>14:59:18</td>
      <td>6.816467</td>
      <td>2015-03</td>
      <td>78.54</td>
      <td>2015-03-31</td>
      <td>...</td>
      <td>2.5792</td>
      <td>2.6016</td>
      <td>2.6228</td>
      <td>2.6427</td>
      <td>2.6616</td>
      <td>2.6794</td>
      <td>2.6963</td>
      <td>30.00</td>
      <td>1.8462</td>
      <td>4.97027</td>
    </tr>
    <tr>
      <th>24</th>
      <td>00077TAB0</td>
      <td>2093-10-15</td>
      <td>USA</td>
      <td>00077TAB0</td>
      <td>2015-04-24</td>
      <td>12:10:55</td>
      <td>6.029157</td>
      <td>2015-04</td>
      <td>78.48</td>
      <td>2015-04-24</td>
      <td>...</td>
      <td>2.6637</td>
      <td>2.6893</td>
      <td>2.7135</td>
      <td>2.7363</td>
      <td>2.7578</td>
      <td>2.7781</td>
      <td>2.7972</td>
      <td>30.00</td>
      <td>1.8252</td>
      <td>4.20396</td>
    </tr>
    <tr>
      <th>25</th>
      <td>00077TAB0</td>
      <td>2093-10-15</td>
      <td>USA</td>
      <td>00077TAB0</td>
      <td>2015-06-04</td>
      <td>11:17:07</td>
      <td>6.404942</td>
      <td>2015-06</td>
      <td>78.37</td>
      <td>2015-06-04</td>
      <td>...</td>
      <td>3.1048</td>
      <td>3.1394</td>
      <td>3.1731</td>
      <td>3.2059</td>
      <td>3.2379</td>
      <td>3.2689</td>
      <td>3.2991</td>
      <td>30.00</td>
      <td>2.2132</td>
      <td>4.19174</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11172</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-08-30</td>
      <td>10:53:27</td>
      <td>2.730190</td>
      <td>2017-08</td>
      <td>6.21</td>
      <td>2017-08-30</td>
      <td>...</td>
      <td>2.7544</td>
      <td>2.7875</td>
      <td>2.8199</td>
      <td>2.8517</td>
      <td>2.8829</td>
      <td>2.9135</td>
      <td>2.9434</td>
      <td>7.21</td>
      <td>2.0507</td>
      <td>0.67949</td>
    </tr>
    <tr>
      <th>11173</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-09-26</td>
      <td>13:56:25</td>
      <td>2.858460</td>
      <td>2017-09</td>
      <td>6.14</td>
      <td>2017-09-26</td>
      <td>...</td>
      <td>2.7821</td>
      <td>2.8139</td>
      <td>2.8452</td>
      <td>2.8762</td>
      <td>2.9066</td>
      <td>2.9366</td>
      <td>2.9661</td>
      <td>7.14</td>
      <td>2.1521</td>
      <td>0.70636</td>
    </tr>
    <tr>
      <th>11174</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-10-24</td>
      <td>12:57:12</td>
      <td>2.955087</td>
      <td>2017-10</td>
      <td>6.06</td>
      <td>2017-10-24</td>
      <td>...</td>
      <td>2.9239</td>
      <td>2.9557</td>
      <td>2.9874</td>
      <td>3.0191</td>
      <td>3.0506</td>
      <td>3.0819</td>
      <td>3.1129</td>
      <td>7.06</td>
      <td>2.3256</td>
      <td>0.629487</td>
    </tr>
    <tr>
      <th>11175</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-11-22</td>
      <td>9:27:49</td>
      <td>2.936286</td>
      <td>2017-11</td>
      <td>5.98</td>
      <td>2017-11-22</td>
      <td>...</td>
      <td>2.7467</td>
      <td>2.7706</td>
      <td>2.7944</td>
      <td>2.8180</td>
      <td>2.8414</td>
      <td>2.8646</td>
      <td>2.8877</td>
      <td>6.98</td>
      <td>2.2634</td>
      <td>0.672886</td>
    </tr>
    <tr>
      <th>11176</th>
      <td>98934KAB6</td>
      <td>2023-11-15</td>
      <td>USA</td>
      <td>98934KAB6</td>
      <td>2017-12-19</td>
      <td>12:22:55</td>
      <td>2.960962</td>
      <td>2017-12</td>
      <td>5.91</td>
      <td>2017-12-19</td>
      <td>...</td>
      <td>2.8125</td>
      <td>2.8357</td>
      <td>2.8593</td>
      <td>2.8833</td>
      <td>2.9075</td>
      <td>2.9320</td>
      <td>2.9566</td>
      <td>6.91</td>
      <td>2.41</td>
      <td>0.550962</td>
    </tr>
  </tbody>
</table>
<p>7548 rows × 43 columns</p>
</div>




```python
transactions_zerocoupon.to_csv('../data/export/part1e.csv')
```


```python

```
