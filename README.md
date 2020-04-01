
## COVID19 Exploratory Data Analysis with PANDAS and creating interactive plots with plotly

In this project a simple Data Analysis is performed on covid-19 Data.

**View the analysis with plots**: https://nbviewer.jupyter.org/github/swapsha/Covid19-Data-Analysis-with-pandas-and-creating-interactive-plots/blob/99023044f8ea870215dca284f223ac0ead6ca9fd/covid19_analysis.ipynb

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

**Step2: Data Summary**


```python
data.describe()
```




<div>
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
      <td>Confirmed</td>
      <td>3/23/2020</td>
      <td>US</td>
      <td>Texas</td>
      <td>Unassigned</td>
      <td>Clay, Indiana, US</td>
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


```python
print("Different case types are ",list(data['Case_Type'].unique()))
```

    Different case types are  ['Deaths', 'Confirmed']
    


```python
data['Date'] = pd.to_datetime(data['Date'])
print("Data is collected from ",min(data['Date'])," to ",max(data['Date']))
```

    Data is collected from  2020-01-22 00:00:00  to  2020-03-30 00:00:00
    


```python
print("Different Table Names from which data is collected ",list(data['Table_Names'].unique()))
```

    Different Table Names from which data is collected  ['Time Series', 'Daily Summary']
    

**Step3: Analyze Missing Values**


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



Province_State, Admin2, Combined_Key, FIPS have missing values as the data for these fields is not collected for all the country regions.

Number of cases is missing in 324 records and latitude and longitude information is missing in 354 records. Lets explore data further and see if any insights can be gained about why these data could be missing.


```python
missing_cases_data = data[data['Cases'].isnull()]
missing_cases_data.head()
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
      <th>33895</th>
      <td>Confirmed</td>
      <td>NaN</td>
      <td>44.0</td>
      <td>2020-03-23</td>
      <td>US</td>
      <td>Wisconsin</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>43.0186</td>
      <td>-92.3814</td>
      <td>3/30/2020</td>
      <td>Daily Summary</td>
    </tr>
    <tr>
      <th>33928</th>
      <td>Confirmed</td>
      <td>NaN</td>
      <td>76.0</td>
      <td>2020-03-23</td>
      <td>US</td>
      <td>Utah</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>40.1500</td>
      <td>-112.0953</td>
      <td>3/30/2020</td>
      <td>Daily Summary</td>
    </tr>
    <tr>
      <th>33984</th>
      <td>Confirmed</td>
      <td>NaN</td>
      <td>20.0</td>
      <td>2020-03-23</td>
      <td>US</td>
      <td>Kansas</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>38.5266</td>
      <td>-96.7265</td>
      <td>3/30/2020</td>
      <td>Daily Summary</td>
    </tr>
    <tr>
      <th>34049</th>
      <td>Confirmed</td>
      <td>NaN</td>
      <td>109.0</td>
      <td>2020-03-23</td>
      <td>US</td>
      <td>Tennessee</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>35.1269</td>
      <td>-89.9253</td>
      <td>3/30/2020</td>
      <td>Daily Summary</td>
    </tr>
    <tr>
      <th>34111</th>
      <td>Confirmed</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2020-03-23</td>
      <td>US</td>
      <td>Wyoming</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>42.7560</td>
      <td>-107.3025</td>
      <td>3/30/2020</td>
      <td>Daily Summary</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(missing_cases_data['Date'].unique())
print(missing_cases_data['Country_Region'].unique())
print(missing_cases_data['Table_Names'].unique())
```

    ['2020-03-23T00:00:00.000000000' '2020-03-30T00:00:00.000000000'
     '2020-03-24T00:00:00.000000000' '2020-03-27T00:00:00.000000000'
     '2020-03-25T00:00:00.000000000' '2020-03-28T00:00:00.000000000'
     '2020-03-29T00:00:00.000000000' '2020-03-26T00:00:00.000000000']
    ['US']
    ['Daily Summary']
    

The missing cases are all from US Daily Summary data from 23th March to 30th March.


```python
missing_lat_data = data[data['Lat'].isnull()]
missing_lat_data.head()
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
      <th>227</th>
      <td>Confirmed</td>
      <td>705.0</td>
      <td>0.0</td>
      <td>2020-03-01</td>
      <td>Cruise Ship</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>298</th>
      <td>Deaths</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2020-02-04</td>
      <td>Cruise Ship</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>566</th>
      <td>Confirmed</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2020-02-02</td>
      <td>Cruise Ship</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>637</th>
      <td>Confirmed</td>
      <td>691.0</td>
      <td>0.0</td>
      <td>2020-02-25</td>
      <td>Cruise Ship</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
    <tr>
      <th>1205</th>
      <td>Deaths</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>2020-02-23</td>
      <td>Cruise Ship</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3/30/2020</td>
      <td>Time Series</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(missing_lat_data['Country_Region'].unique())
```

    ['Cruise Ship' 'US']
    


```python
missing_lat_data['Country_Region'].value_counts()
```




    US             216
    Cruise Ship    138
    Name: Country_Region, dtype: int64




```python
data[(data['Country_Region'] == 'US')|(data['Country_Region'] == 'Cruise Ship')]['Country_Region'].value_counts()
```




    US             57708
    Cruise Ship      138
    Name: Country_Region, dtype: int64



As Cruise Ship is not a region it has missing latitude and longitude values. There are 138 regions in US with no latitude and longitude information. Lets explore further to understand why the data is missing.


```python
print(missing_lat_data[missing_lat_data['Country_Region'] == 'US']['Table_Names'].unique())
print(missing_lat_data[missing_lat_data['Country_Region'] == 'US']['Date'].unique())
print(missing_lat_data[missing_lat_data['Country_Region'] == 'US']['Cases'].unique())
```

    ['Daily Summary']
    ['2020-03-23T00:00:00.000000000' '2020-03-30T00:00:00.000000000'
     '2020-03-24T00:00:00.000000000' '2020-03-27T00:00:00.000000000'
     '2020-03-25T00:00:00.000000000' '2020-03-28T00:00:00.000000000'
     '2020-03-29T00:00:00.000000000' '2020-03-26T00:00:00.000000000']
    [nan]
    

The missing location information in US is during the duration 23rd March to 30th March when cases are missing.

While performing analysis we will just ignore the missing data.

**Step 4: Data Analysis and Visualization**

There are two tables from which this data is collected from John Hopkins, one is Daily Summary and other is Time Series. First we need to understand the different between either sources and then continue analysis.


```python
daily_summary_data = data[data['Table_Names'] == 'Daily Summary']
time_series_data = data[data['Table_Names'] == 'Time Series']
print(daily_summary_data.shape)
print(time_series_data.shape)
```

    (51120, 13)
    (40950, 13)
    


```python
time_series_data.isnull().sum()
```




    Case_Type                0
    Cases                    0
    Difference             606
    Date                     0
    Country_Region           0
    Province_State       23874
    Admin2               40950
    Combined_Key         40950
    FIPS                 40950
    Lat                    138
    Long                   138
    Prep_Flow_Runtime        0
    Table_Names              0
    dtype: int64




```python
daily_summary_data.isnull().sum()
```




    Case_Type               0
    Cases                 324
    Difference           6376
    Date                    0
    Country_Region          0
    Province_State          0
    Admin2                192
    Combined_Key          112
    FIPS                  784
    Lat                   216
    Long                  216
    Prep_Flow_Runtime       0
    Table_Names             0
    dtype: int64



Notice that Time Series Data doesn't have county wise cases data, Its an aggregation on State and Country. First lets analyze time series data as it is useful to analyze cases across regions.


```python
import plotly.express as px
fig = px.pie(time_series_data,names='Case_Type', title='Number of records of each type')
#fig.show()
```

There is 50% data with deaths and 50% data with confirmed cases. This is beacuse for each country, region both deaths data and confirmed cases data is collected on each day.


```python
fig = px.pie(time_series_data,names='Country_Region', title='Number of records for each region')
#fig.update_traces(textposition='inside', textinfo='percent+label')
#fig.show()
```

16.1% of records have US data, the main reason behind this is in US data is displayed for each State as well. The other best way to view number of data points for each country is to filter data by selecting country and unique dates.


```python
confirmed_df = pd.DataFrame(time_series_data[time_series_data['Case_Type'] == 'Confirmed'].groupby(['Date']).agg({'Cases':'sum'}).reset_index())
confirmed_df.head()
fig = px.line(confirmed_df, x="Date", y="Cases",title = 'Confirmed cases across time through out the world')
#fig.show()
```

From the above plot it can be noticed that number of confirmed cases increased exponentially onver time.


```python
deaths_df = pd.DataFrame(time_series_data[time_series_data['Case_Type'] == 'Deaths'].groupby(['Date']).agg({'Cases':'sum'}).reset_index())
deaths_df.head()
fig = px.line(deaths_df, x="Date", y="Cases",title = 'Total Deaths across time through out the world')
#fig.show()
```

From the above plot it can be noticed that number of confirmed cases increased exponentially onver time.


```python
confirmed_df = pd.DataFrame(time_series_data[time_series_data['Case_Type'] == 'Confirmed'].groupby(['Date','Country_Region']).agg({'Cases':'sum'}).reset_index())
#fig = px.bar(confirmed_df.groupby(['Country_Region']).agg({'Cases':'sum'}).reset_index().sort_values(by = 'Cases',ascending = False), x = 'Country_Region', y = 'Cases',title = 'Total Number of Cases per region')
fig = px.bar(confirmed_df[confirmed_df['Date'] == '2020-03-22'].sort_values(by = 'Cases',ascending = False), x = 'Country_Region', y = 'Cases',title = 'Total Number of Cases per region as of March 22nd')
#fig.show()
```

As of March 22nd, Total number of cases are highest in China followed by Italy, US, Spain,Germany,Iran, France


```python
confirmed_df = pd.DataFrame(time_series_data[time_series_data['Case_Type'] == 'Confirmed'].groupby(['Date','Country_Region']).agg({'Cases':'sum'}).reset_index())
#fig = px.bar(confirmed_df.groupby(['Country_Region']).agg({'Cases':'sum'}).reset_index().sort_values(by = 'Cases',ascending = False), x = 'Country_Region', y = 'Cases',title = 'Total Number of Cases per region')
fig = px.bar(confirmed_df[confirmed_df['Date'] == '2020-03-30'].sort_values(by = 'Cases',ascending = False), x = 'Country_Region', y = 'Cases',title = 'Total Number of Cases per region as of March 30th')
#fig.show()
```

As of March 30th, Total number of cases are highest in Italy followed by Spain,China, Germany,France,Iran. Also notice in one week number of cases in Italy increased alot.


```python
fig = px.line(confirmed_df, x="Date", y="Cases",color = 'Country_Region',title = 'Time series plot of Confirmed cases across regions')
#fig.show()
```

From the above plot notice that confirmed cases in China increased rapidly in feb compared to other regions this is due to the fact that virus first started spreading in china, later with time number of confirmed cases increased slowly as the government in China has taken enough precautions to keep the situation under control. Where as in other parts of the world number of cases drastically started increasing in the second week of March. As of March 30 Italy has highest number of Cases.


```python
deaths_df = pd.DataFrame(time_series_data[time_series_data['Case_Type'] == 'Deaths'].groupby(['Date','Country_Region']).agg({'Cases':'sum'}).reset_index())
deaths_df[deaths_df['Country_Region'] == 'US'].tail()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Country_Region</th>
      <th>Cases</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10077</th>
      <td>2020-03-18</td>
      <td>US</td>
      <td>118.0</td>
    </tr>
    <tr>
      <th>10254</th>
      <td>2020-03-19</td>
      <td>US</td>
      <td>200.0</td>
    </tr>
    <tr>
      <th>10431</th>
      <td>2020-03-20</td>
      <td>US</td>
      <td>244.0</td>
    </tr>
    <tr>
      <th>10608</th>
      <td>2020-03-21</td>
      <td>US</td>
      <td>307.0</td>
    </tr>
    <tr>
      <th>10785</th>
      <td>2020-03-22</td>
      <td>US</td>
      <td>416.0</td>
    </tr>
  </tbody>
</table>
</div>



As US Data is not available from 23rd March to 30th March lets look at total deaths plot across region as on 22nd March.


```python
fig = px.bar(deaths_df[deaths_df['Date'] == '2020-03-22'].sort_values(by = 'Cases',ascending = False), x = 'Country_Region', y = 'Cases',title = 'Total Number of Deaths per region as of 22nd March')
#fig.show()
```

As of March 22, 2020 highest number of deaths are recorded in Italy around 5k, followed by China, Spain, Iran, France and US


```python
fig = px.bar(deaths_df[deaths_df['Date'] == '2020-03-30'].sort_values(by = 'Cases',ascending = False), x = 'Country_Region', y = 'Cases',title = 'Total Number of Deaths per region as on 30th March')
#fig.show()
```

As of March 30, 2020 highest number of deaths are recorded in Italy around 11.5k, followed by Spain, China, France, Iran. This plot doesnt show US data as data is missing.


```python
fig = px.line(deaths_df, x="Date", y="Cases",color = 'Country_Region',title = 'Time series plot of Deaths across regions')
#fig.show()
```

From the above plot notice that death cases in China increased rapidly in feb compared to other regions this is due to the fact that virus first started spreading in china, later with time number of confirmed cases increased slowly as the government in China has taken enough precautions to keep the situation under control. Where as in other parts of the world number of cases drastically started increasing in the second week of March. As of March 30 Italy has highest number of deaths recorded.

