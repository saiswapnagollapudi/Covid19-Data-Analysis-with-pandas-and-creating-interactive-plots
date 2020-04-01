
## COVID19 Exploratory Data Analysis with PANDAS and creating interactive plots with plotly

In this project a simple Data Analysis is performed on covid-19 Data.

**Data Source**: https://data.world/covid-19-data-resource-hub/covid-19-case-counts/workspace/file?filename=COVID-19+Cases.csv

**Data Dictionary**: https://data.world/covid-19-data-resource-hub/covid-19-case-counts/workspace/data-dictionary

**Step 1: Load the libraries and data**


```python
import os
import numpy as np
import pandas as pd
```


```python
data = pd.read_csv('COVID-19-Cases.csv')
data.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Case_Type</th>
      <th>Cases</th>
      <th>Difference</th>
      <th>Date</th>
      <th>Country_Region</th>
      <th>Province_State</th>
      <th>Admin2</th>
      <th>Combined_Key</th>
      <th>FIPS</th>
      <th>Lat</th>
      <th>Long</th>
      <th>Prep_Flow_Runtime</th>
      <th>Table_Names</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Deaths</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2/27/2020</td>
      <td>Bahamas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>25.0343</td>
      <td>-77.3963</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Confirmed</td>
      <td>16.0</td>
      <td>0.0</td>
      <td>2/16/2020</td>
      <td>Germany</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>51.0000</td>
      <td>9.0000</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Deaths</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1/31/2020</td>
      <td>Canada</td>
      <td>Alberta</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>53.9333</td>
      <td>-116.5765</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Deaths</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3/4/2020</td>
      <td>Australia</td>
      <td>Queensland</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-28.0167</td>
      <td>153.4000</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Confirmed</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1/25/2020</td>
      <td>Suriname</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.9193</td>
      <td>-56.0278</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
  </tbody>
</table>
</div>



pandas read_csv function is used to load the csv file into pandas dataframe.

head function displays the top 5 records in the dataframe.

From the top 5 records It can be noticed that there are many missing values in the dataset.


```python
data.shape
```




    (92070, 13)



shape function is used to display number of rows and columns in a dataframe. 

There are 92070 records and 13 fields in the dataset.


```python
data.describe()
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
      <th>Cases</th>
      <th>Difference</th>
      <th>FIPS</th>
      <th>Lat</th>
      <th>Long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>91746.000000</td>
      <td>85088.000000</td>
      <td>50336.00000</td>
      <td>91716.000000</td>
      <td>91716.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>110.480184</td>
      <td>9.627915</td>
      <td>30431.79466</td>
      <td>32.128978</td>
      <td>-47.854246</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2022.197499</td>
      <td>160.640521</td>
      <td>15212.33980</td>
      <td>17.639699</td>
      <td>72.588082</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>-668.000000</td>
      <td>1001.00000</td>
      <td>-41.454500</td>
      <td>-170.132000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>18179.00000</td>
      <td>30.057200</td>
      <td>-93.985197</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>29180.00000</td>
      <td>36.932559</td>
      <td>-82.427002</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>45087.00000</td>
      <td>41.772551</td>
      <td>1.659600</td>
    </tr>
    <tr>
      <th>max</th>
      <td>101739.000000</td>
      <td>14840.000000</td>
      <td>78000.00000</td>
      <td>71.706900</td>
      <td>178.065000</td>
    </tr>
  </tbody>
</table>
</div>



describe function displays the summary statistics of a dataframe like mean, median, quantiles, min and max values, by default it selects fields containing numeric datatype values.

Notice that minimum number of cases are zero. 75 percentile is 1 meaning 75% of records have number of cases less than 1 and maximum number of cases are 101739. 



```python
data.select_dtypes('object').describe()
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
      <th>Case_Type</th>
      <th>Date</th>
      <th>Country_Region</th>
      <th>Province_State</th>
      <th>Admin2</th>
      <th>Combined_Key</th>
      <th>Prep_Flow_Runtime</th>
      <th>Table_Names</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>92070</td>
      <td>92070</td>
      <td>92070</td>
      <td>68196</td>
      <td>50928</td>
      <td>51008</td>
      <td>92070</td>
      <td>92070</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>2</td>
      <td>69</td>
      <td>177</td>
      <td>132</td>
      <td>1845</td>
      <td>3188</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Deaths</td>
      <td>3/23/2020</td>
      <td>US</td>
      <td>Texas</td>
      <td>Unassigned</td>
      <td>Cherry, Nebraska, US</td>
      <td>3/30/2020</td>
      <td>Daily Summary</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>46035</td>
      <td>6986</td>
      <td>57708</td>
      <td>4188</td>
      <td>576</td>
      <td>16</td>
      <td>92070</td>
      <td>51120</td>
    </tr>
  </tbody>
</table>
</div>



There are 2 types of cases, 177 country regions, 132 province states,1845 Admin2(this refers to county)

Province states data is available only for the below country regions: Australia, Canada, China, Denmark, France, Netherlands, United Kingdom, United States

Admin2 and combined_key data is available only for US region.

**Missing Values**


```python
data.isnull().sum()
```




    Case_Type                0
    Cases                  324
    Difference            6982
    Date                     0
    Country_Region           0
    Province_State       23874
    Admin2               41142
    Combined_Key         41062
    FIPS                 41734
    Lat                    354
    Long                   354
    Prep_Flow_Runtime        0
    Table_Names              0
    dtype: int64



Province_State, Admin2, Combined_Key, FIPS have missing values as these data is not collected for all the country regions.


```python
print("Number of rows in the dataset ",data.shape[0]," Number of columns in data ",data.shape[1])
print(data.columns)
print("Unique case types are: ", data['Case_Type'].unique())
#There are two case types one is deaths and other is confirmed
print("Number of different regions from which data is collected ",len(data['Country_Region'].unique())
print("Data is available from ",data['Date'].min()." to ",data['Date'].max())
print("Maximum number of cases are ",max(data['Cases']))
max_record = data.loc[data['Cases'].argmax(),:]
print("Highest number of Cases are reported in ",max_record['Country_Region']" and number of cases are ",max_record['Cases']," as of ",max_record['Date'])
```
