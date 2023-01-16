# Importing and formatting DOA dataset


```python
# importing libraries and intializing output parameters
import pandas as pd
import numpy as np
from passyunk.parser import PassyunkParser
pd.set_option('display.max_columns', 1500)
pd.set_option('display.max_rows', 1500)
```

    C:\Users\rupam\anaconda3\lib\site-packages\fuzzywuzzy\fuzz.py:11: UserWarning: Using slow pure-python SequenceMatcher. Install python-Levenshtein to remove this warning
      warnings.warn('Using slow pure-python SequenceMatcher. Install python-Levenshtein to remove this warning')
    C:\Users\rupam\anaconda3\lib\site-packages\passyunk\parser.py:671: UserWarning: USPS file not found.
      warnings.warn('USPS file not found.')
    C:\Users\rupam\anaconda3\lib\site-packages\passyunk\parser.py:680: UserWarning: Election file not found.
      warnings.warn('Election file not found.')
    


```python
# importing DOR dataset
# url_doa="https://opendata.arcgis.com/datasets/1c57dd1b3ff84449a4b0e3fb29d3cafd_0.csv"
# dor_data_full = pd.read_csv(url_doa)

dor_data_full = pd.read_csv('C:/Users/rupam/Downloads/DOR_Parcel.csv')
```

    C:\Users\rupam\anaconda3\lib\site-packages\IPython\core\interactiveshell.py:3444: DtypeWarning: Columns (4,22,26,28,29,30,31,32,33,34,35,36,37) have mixed types.Specify dtype option on import or set low_memory=False.
      exec(code_obj, self.user_global_ns, self.user_ns)
    


```python
dor_data_full.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 606602 entries, 0 to 606601
    Data columns (total 40 columns):
     #   Column            Non-Null Count   Dtype  
    ---  ------            --------------   -----  
     0   OBJECTID          606602 non-null  int64  
     1   RECSUB            584613 non-null  object 
     2   BASEREG           606424 non-null  object 
     3   MAPREG            606443 non-null  object 
     4   PARCEL            606255 non-null  object 
     5   RECMAP            606431 non-null  object 
     6   STCOD             604924 non-null  float64
     7   HOUSE             593252 non-null  float64
     8   SUF               3090 non-null    object 
     9   UNIT              8161 non-null    object 
     10  STEX              12844 non-null   float64
     11  STDIR             238980 non-null  object 
     12  STNAM             600754 non-null  object 
     13  STDESSUF          48782 non-null   object 
     14  ELEV_FLAG         606602 non-null  int64  
     15  TOPELEV           606602 non-null  float64
     16  BOTELEV           606602 non-null  float64
     17  CONDOFLAG         606602 non-null  int64  
     18  MATCHFLAG         577588 non-null  float64
     19  INACTDATE         590452 non-null  object 
     20  ORIG_DATE         594550 non-null  object 
     21  STATUS            606602 non-null  int64  
     22  GEOID             61 non-null      object 
     23  STDES             600228 non-null  object 
     24  ADDR_SOURCE       606301 non-null  object 
     25  ADDR_STD          593119 non-null  object 
     26  COMMENTS          10225 non-null   object 
     27  PIN               576323 non-null  float64
     28  FRAC              444 non-null     object 
     29  UNIT_TYPE         7 non-null       object 
     30  STEX_FRAC         9 non-null       object 
     31  STEX_SUF          6 non-null       object 
     32  SEPARATED_RIGHTS  425 non-null     object 
     33  MUNIMENT_TYPE     17906 non-null   object 
     34  MUNIMENT_ID       17913 non-null   object 
     35  DOR_REVIEW        26119 non-null   object 
     36  OPA_REVIEW        25682 non-null   object 
     37  PWD_REVIEW        25711 non-null   object 
     38  Shape__Area       606576 non-null  float64
     39  Shape__Length     606576 non-null  float64
    dtypes: float64(9), int64(4), object(27)
    memory usage: 185.1+ MB
    


```python
dor_data_full.head()
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
      <th>OBJECTID</th>
      <th>RECSUB</th>
      <th>BASEREG</th>
      <th>MAPREG</th>
      <th>PARCEL</th>
      <th>RECMAP</th>
      <th>STCOD</th>
      <th>HOUSE</th>
      <th>SUF</th>
      <th>UNIT</th>
      <th>STEX</th>
      <th>STDIR</th>
      <th>STNAM</th>
      <th>STDESSUF</th>
      <th>ELEV_FLAG</th>
      <th>TOPELEV</th>
      <th>BOTELEV</th>
      <th>CONDOFLAG</th>
      <th>MATCHFLAG</th>
      <th>INACTDATE</th>
      <th>ORIG_DATE</th>
      <th>STATUS</th>
      <th>GEOID</th>
      <th>STDES</th>
      <th>ADDR_SOURCE</th>
      <th>ADDR_STD</th>
      <th>COMMENTS</th>
      <th>PIN</th>
      <th>FRAC</th>
      <th>UNIT_TYPE</th>
      <th>STEX_FRAC</th>
      <th>STEX_SUF</th>
      <th>SEPARATED_RIGHTS</th>
      <th>MUNIMENT_TYPE</th>
      <th>MUNIMENT_ID</th>
      <th>DOR_REVIEW</th>
      <th>OPA_REVIEW</th>
      <th>PWD_REVIEW</th>
      <th>Shape__Area</th>
      <th>Shape__Length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td></td>
      <td>062N060035</td>
      <td>062N060035</td>
      <td>35</td>
      <td>062N06</td>
      <td>88950.0</td>
      <td>1246.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/07 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1246 N 57TH ST</td>
      <td>1246 N 57TH ST</td>
      <td>NaN</td>
      <td>1.001663e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>213.898438</td>
      <td>83.596914</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td></td>
      <td>022S080047</td>
      <td>022S080047</td>
      <td>47</td>
      <td>022S08</td>
      <td>88960.0</td>
      <td>263.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>S</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>5.0</td>
      <td>1899/12/30 14:25:14+00</td>
      <td>2003/03/17 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>263 S 57TH ST</td>
      <td>263 S 57TH ST</td>
      <td>NaN</td>
      <td>1.001664e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>203.632812</td>
      <td>76.989855</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td></td>
      <td>059N230030</td>
      <td>059N230030</td>
      <td>30</td>
      <td>059N23</td>
      <td>46380.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>JUNE</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>5.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>2</td>
      <td>NaN</td>
      <td>ST</td>
      <td>JUNE ST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>83.179688</td>
      <td>41.454694</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td></td>
      <td>018S170162</td>
      <td>018S170162</td>
      <td>162</td>
      <td>018S17</td>
      <td>88980.0</td>
      <td>129.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South</td>
      <td>58TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>129 S 58TH ST</td>
      <td>129 S 58TH ST</td>
      <td>NaN</td>
      <td>1.001665e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>198.917969</td>
      <td>77.113848</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td></td>
      <td>063N010108</td>
      <td>063N010108</td>
      <td>108</td>
      <td>063N01</td>
      <td>89030.0</td>
      <td>22.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>61ST</td>
      <td></td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>22 N 61ST ST</td>
      <td>22 N 61ST ST</td>
      <td>NaN</td>
      <td>1.001668e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>153.949219</td>
      <td>63.186956</td>
    </tr>
  </tbody>
</table>
</div>




```python
# filtering DOR data for status 1 and 3
dor_data_status = dor_data_full.loc[(dor_data_full['STATUS'] == 1) | (dor_data_full['STATUS'] == 3)]
```


```python
dor_data_status.head()
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
      <th>OBJECTID</th>
      <th>RECSUB</th>
      <th>BASEREG</th>
      <th>MAPREG</th>
      <th>PARCEL</th>
      <th>RECMAP</th>
      <th>STCOD</th>
      <th>HOUSE</th>
      <th>SUF</th>
      <th>UNIT</th>
      <th>STEX</th>
      <th>STDIR</th>
      <th>STNAM</th>
      <th>STDESSUF</th>
      <th>ELEV_FLAG</th>
      <th>TOPELEV</th>
      <th>BOTELEV</th>
      <th>CONDOFLAG</th>
      <th>MATCHFLAG</th>
      <th>INACTDATE</th>
      <th>ORIG_DATE</th>
      <th>STATUS</th>
      <th>GEOID</th>
      <th>STDES</th>
      <th>ADDR_SOURCE</th>
      <th>ADDR_STD</th>
      <th>COMMENTS</th>
      <th>PIN</th>
      <th>FRAC</th>
      <th>UNIT_TYPE</th>
      <th>STEX_FRAC</th>
      <th>STEX_SUF</th>
      <th>SEPARATED_RIGHTS</th>
      <th>MUNIMENT_TYPE</th>
      <th>MUNIMENT_ID</th>
      <th>DOR_REVIEW</th>
      <th>OPA_REVIEW</th>
      <th>PWD_REVIEW</th>
      <th>Shape__Area</th>
      <th>Shape__Length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td></td>
      <td>062N060035</td>
      <td>062N060035</td>
      <td>35</td>
      <td>062N06</td>
      <td>88950.0</td>
      <td>1246.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/07 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1246 N 57TH ST</td>
      <td>1246 N 57TH ST</td>
      <td>NaN</td>
      <td>1.001663e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>213.898438</td>
      <td>83.596914</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td></td>
      <td>022S080047</td>
      <td>022S080047</td>
      <td>47</td>
      <td>022S08</td>
      <td>88960.0</td>
      <td>263.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>S</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>5.0</td>
      <td>1899/12/30 14:25:14+00</td>
      <td>2003/03/17 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>263 S 57TH ST</td>
      <td>263 S 57TH ST</td>
      <td>NaN</td>
      <td>1.001664e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>203.632812</td>
      <td>76.989855</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td></td>
      <td>018S170162</td>
      <td>018S170162</td>
      <td>162</td>
      <td>018S17</td>
      <td>88980.0</td>
      <td>129.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South</td>
      <td>58TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>129 S 58TH ST</td>
      <td>129 S 58TH ST</td>
      <td>NaN</td>
      <td>1.001665e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>198.917969</td>
      <td>77.113848</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td></td>
      <td>063N010108</td>
      <td>063N010108</td>
      <td>108</td>
      <td>063N01</td>
      <td>89030.0</td>
      <td>22.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>61ST</td>
      <td></td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>22 N 61ST ST</td>
      <td>22 N 61ST ST</td>
      <td>NaN</td>
      <td>1.001668e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>153.949219</td>
      <td>63.186956</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td></td>
      <td>068N230217</td>
      <td>068N230217</td>
      <td>217</td>
      <td>068N23</td>
      <td>89030.0</td>
      <td>1706.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>61ST</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/07 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1706 N 61ST ST</td>
      <td>1706 N 61ST ST</td>
      <td>NaN</td>
      <td>1.001668e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>238.304688</td>
      <td>90.664746</td>
    </tr>
  </tbody>
</table>
</div>




```python
# making a deep copy of dor dataset and resetting the index
dor_data = dor_data_status.copy(deep = True)
dor_data.reset_index(inplace=True,drop=True)
```


```python
dor_data.head(5)
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
      <th>OBJECTID</th>
      <th>RECSUB</th>
      <th>BASEREG</th>
      <th>MAPREG</th>
      <th>PARCEL</th>
      <th>RECMAP</th>
      <th>STCOD</th>
      <th>HOUSE</th>
      <th>SUF</th>
      <th>UNIT</th>
      <th>STEX</th>
      <th>STDIR</th>
      <th>STNAM</th>
      <th>STDESSUF</th>
      <th>ELEV_FLAG</th>
      <th>TOPELEV</th>
      <th>BOTELEV</th>
      <th>CONDOFLAG</th>
      <th>MATCHFLAG</th>
      <th>INACTDATE</th>
      <th>ORIG_DATE</th>
      <th>STATUS</th>
      <th>GEOID</th>
      <th>STDES</th>
      <th>ADDR_SOURCE</th>
      <th>ADDR_STD</th>
      <th>COMMENTS</th>
      <th>PIN</th>
      <th>FRAC</th>
      <th>UNIT_TYPE</th>
      <th>STEX_FRAC</th>
      <th>STEX_SUF</th>
      <th>SEPARATED_RIGHTS</th>
      <th>MUNIMENT_TYPE</th>
      <th>MUNIMENT_ID</th>
      <th>DOR_REVIEW</th>
      <th>OPA_REVIEW</th>
      <th>PWD_REVIEW</th>
      <th>Shape__Area</th>
      <th>Shape__Length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td></td>
      <td>062N060035</td>
      <td>062N060035</td>
      <td>35</td>
      <td>062N06</td>
      <td>88950.0</td>
      <td>1246.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/07 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1246 N 57TH ST</td>
      <td>1246 N 57TH ST</td>
      <td>NaN</td>
      <td>1.001663e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>213.898438</td>
      <td>83.596914</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td></td>
      <td>022S080047</td>
      <td>022S080047</td>
      <td>47</td>
      <td>022S08</td>
      <td>88960.0</td>
      <td>263.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>S</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>5.0</td>
      <td>1899/12/30 14:25:14+00</td>
      <td>2003/03/17 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>263 S 57TH ST</td>
      <td>263 S 57TH ST</td>
      <td>NaN</td>
      <td>1.001664e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>203.632812</td>
      <td>76.989855</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td></td>
      <td>018S170162</td>
      <td>018S170162</td>
      <td>162</td>
      <td>018S17</td>
      <td>88980.0</td>
      <td>129.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South</td>
      <td>58TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>129 S 58TH ST</td>
      <td>129 S 58TH ST</td>
      <td>NaN</td>
      <td>1.001665e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>198.917969</td>
      <td>77.113848</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td></td>
      <td>063N010108</td>
      <td>063N010108</td>
      <td>108</td>
      <td>063N01</td>
      <td>89030.0</td>
      <td>22.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>61ST</td>
      <td></td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>22 N 61ST ST</td>
      <td>22 N 61ST ST</td>
      <td>NaN</td>
      <td>1.001668e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>153.949219</td>
      <td>63.186956</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td></td>
      <td>068N230217</td>
      <td>068N230217</td>
      <td>217</td>
      <td>068N23</td>
      <td>89030.0</td>
      <td>1706.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>61ST</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/07 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1706 N 61ST ST</td>
      <td>1706 N 61ST ST</td>
      <td>NaN</td>
      <td>1.001668e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>238.304688</td>
      <td>90.664746</td>
    </tr>
  </tbody>
</table>
</div>




```python
# no value of HOUSE is -1 in DOR dataset
dor_data[dor_data['HOUSE'] == -1].shape
```




    (0, 40)




```python
# no value of STEX is -1 in DOR dataset
dor_data[dor_data['STEX'] == -1].shape
```




    (0, 40)




```python
# replacing nan value of HOUSE by -1 in DOR dataset

dor_data['HOUSE'] = dor_data['HOUSE'].fillna(-1).astype(int)
```


```python
# replacing -1 value of HOUSE by '' (empty string) in DOR dataset

dor_data['HOUSE'] = dor_data['HOUSE'].replace(to_replace=-1,value='')
```


```python
# Changing the datatype of HOUSE column as string in DOR dataset

dor_data['HOUSE'] = dor_data['HOUSE'].astype(str)
```


```python
# replacing nan value of STEX by -1 in DOR dataset

dor_data['STEX'] = dor_data['STEX'].fillna(-1).astype(int)
```


```python
# Changing the datatype of HOUSE column as string in DOR dataset

dor_data['STEX'] = dor_data['STEX'].astype(str) 
```


```python
# replacing -1 value of STEX by nan in DOR dataset

dor_data['STEX'] = dor_data['STEX'].replace(to_replace='-1',value= np.nan)
```


```python
# Concatenating the address fields in DOR datset
dor_data["Address_Concat_dor"] = dor_data['HOUSE'].fillna('') + ('-' + dor_data["STEX"]).fillna('') + ' '+ dor_data['STDIR'].fillna('') + ' '+ dor_data['STNAM'].fillna('') + ' ' + dor_data['STDES'].fillna('')+  (' # '+ dor_data['UNIT']).fillna('')
```


```python
# Concatenating the address fields in DOR datset
dor_data["Address_Concat_dor_v1"] = dor_data['HOUSE'].fillna('') + ('-' + dor_data["STEX"]).fillna('') + ' '+ dor_data['STDIR'].fillna('') + ' '+ dor_data['STNAM'].fillna('') + ' ' + dor_data['STDES'].fillna('')+  (' [UNIT] '+ dor_data['UNIT']).fillna('')
```


```python
dor_data.head(5)
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
      <th>OBJECTID</th>
      <th>RECSUB</th>
      <th>BASEREG</th>
      <th>MAPREG</th>
      <th>PARCEL</th>
      <th>RECMAP</th>
      <th>STCOD</th>
      <th>HOUSE</th>
      <th>SUF</th>
      <th>UNIT</th>
      <th>STEX</th>
      <th>STDIR</th>
      <th>STNAM</th>
      <th>STDESSUF</th>
      <th>ELEV_FLAG</th>
      <th>TOPELEV</th>
      <th>BOTELEV</th>
      <th>CONDOFLAG</th>
      <th>MATCHFLAG</th>
      <th>INACTDATE</th>
      <th>ORIG_DATE</th>
      <th>STATUS</th>
      <th>GEOID</th>
      <th>STDES</th>
      <th>ADDR_SOURCE</th>
      <th>ADDR_STD</th>
      <th>COMMENTS</th>
      <th>PIN</th>
      <th>FRAC</th>
      <th>UNIT_TYPE</th>
      <th>STEX_FRAC</th>
      <th>STEX_SUF</th>
      <th>SEPARATED_RIGHTS</th>
      <th>MUNIMENT_TYPE</th>
      <th>MUNIMENT_ID</th>
      <th>DOR_REVIEW</th>
      <th>OPA_REVIEW</th>
      <th>PWD_REVIEW</th>
      <th>Shape__Area</th>
      <th>Shape__Length</th>
      <th>Address_Concat_dor</th>
      <th>Address_Concat_dor_v1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td></td>
      <td>062N060035</td>
      <td>062N060035</td>
      <td>35</td>
      <td>062N06</td>
      <td>88950.0</td>
      <td>1246</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/07 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1246 N 57TH ST</td>
      <td>1246 N 57TH ST</td>
      <td>NaN</td>
      <td>1.001663e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>213.898438</td>
      <td>83.596914</td>
      <td>1246 N 57TH ST</td>
      <td>1246 N 57TH ST</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td></td>
      <td>022S080047</td>
      <td>022S080047</td>
      <td>47</td>
      <td>022S08</td>
      <td>88960.0</td>
      <td>263</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>S</td>
      <td>57TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>5.0</td>
      <td>1899/12/30 14:25:14+00</td>
      <td>2003/03/17 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>263 S 57TH ST</td>
      <td>263 S 57TH ST</td>
      <td>NaN</td>
      <td>1.001664e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>203.632812</td>
      <td>76.989855</td>
      <td>263 S 57TH ST</td>
      <td>263 S 57TH ST</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4</td>
      <td></td>
      <td>018S170162</td>
      <td>018S170162</td>
      <td>162</td>
      <td>018S17</td>
      <td>88980.0</td>
      <td>129</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>South</td>
      <td>58TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>129 S 58TH ST</td>
      <td>129 S 58TH ST</td>
      <td>NaN</td>
      <td>1.001665e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>198.917969</td>
      <td>77.113848</td>
      <td>129 South 58TH ST</td>
      <td>129 South 58TH ST</td>
    </tr>
    <tr>
      <th>3</th>
      <td>5</td>
      <td></td>
      <td>063N010108</td>
      <td>063N010108</td>
      <td>108</td>
      <td>063N01</td>
      <td>89030.0</td>
      <td>22</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>61ST</td>
      <td></td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/04 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>22 N 61ST ST</td>
      <td>22 N 61ST ST</td>
      <td>NaN</td>
      <td>1.001668e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>153.949219</td>
      <td>63.186956</td>
      <td>22 N 61ST ST</td>
      <td>22 N 61ST ST</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td></td>
      <td>068N230217</td>
      <td>068N230217</td>
      <td>217</td>
      <td>068N23</td>
      <td>89030.0</td>
      <td>1706</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N</td>
      <td>61ST</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2003/02/07 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1706 N 61ST ST</td>
      <td>1706 N 61ST ST</td>
      <td>NaN</td>
      <td>1.001668e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>238.304688</td>
      <td>90.664746</td>
      <td>1706 N 61ST ST</td>
      <td>1706 N 61ST ST</td>
    </tr>
  </tbody>
</table>
</div>




```python
dor_data.loc[dor_data['UNIT'].notna()] 
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
      <th>OBJECTID</th>
      <th>RECSUB</th>
      <th>BASEREG</th>
      <th>MAPREG</th>
      <th>PARCEL</th>
      <th>RECMAP</th>
      <th>STCOD</th>
      <th>HOUSE</th>
      <th>SUF</th>
      <th>UNIT</th>
      <th>STEX</th>
      <th>STDIR</th>
      <th>STNAM</th>
      <th>STDESSUF</th>
      <th>ELEV_FLAG</th>
      <th>TOPELEV</th>
      <th>BOTELEV</th>
      <th>CONDOFLAG</th>
      <th>MATCHFLAG</th>
      <th>INACTDATE</th>
      <th>ORIG_DATE</th>
      <th>STATUS</th>
      <th>GEOID</th>
      <th>STDES</th>
      <th>ADDR_SOURCE</th>
      <th>ADDR_STD</th>
      <th>COMMENTS</th>
      <th>PIN</th>
      <th>FRAC</th>
      <th>UNIT_TYPE</th>
      <th>STEX_FRAC</th>
      <th>STEX_SUF</th>
      <th>SEPARATED_RIGHTS</th>
      <th>MUNIMENT_TYPE</th>
      <th>MUNIMENT_ID</th>
      <th>DOR_REVIEW</th>
      <th>OPA_REVIEW</th>
      <th>PWD_REVIEW</th>
      <th>Shape__Area</th>
      <th>Shape__Length</th>
      <th>Address_Concat_dor</th>
      <th>Address_Concat_dor_v1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>56</th>
      <td>118</td>
      <td>A</td>
      <td>003S050342</td>
      <td>003S050342</td>
      <td>342</td>
      <td>003S05</td>
      <td>74300.0</td>
      <td>232</td>
      <td>NaN</td>
      <td>R</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>STAMPERS</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>2.0</td>
      <td>1899/12/30 08:35:48+00</td>
      <td>2003/03/21 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>232 STAMPERS ST # R</td>
      <td>232 STAMPERS ST # R</td>
      <td>NaN</td>
      <td>1.001021e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>39.222656</td>
      <td>25.691489</td>
      <td>232  STAMPERS ST # R</td>
      <td>232  STAMPERS ST [UNIT] R</td>
    </tr>
    <tr>
      <th>64</th>
      <td>126</td>
      <td></td>
      <td>016S110191</td>
      <td>016S110191</td>
      <td>191</td>
      <td>016S11</td>
      <td>73220.0</td>
      <td>1501</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SNYDER</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 19:00:55+00</td>
      <td>2003/05/06 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>AVE</td>
      <td>1501 SNYDER AVE # A</td>
      <td>1501 SNYDER AVE # A</td>
      <td>NaN</td>
      <td>1.001028e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>308.687500</td>
      <td>72.789093</td>
      <td>1501  SNYDER AVE # A</td>
      <td>1501  SNYDER AVE [UNIT] A</td>
    </tr>
    <tr>
      <th>67</th>
      <td>129</td>
      <td></td>
      <td>160N190159</td>
      <td>160N190159</td>
      <td>159</td>
      <td>160N19</td>
      <td>53435.0</td>
      <td>1509</td>
      <td>NaN</td>
      <td>#A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>MARCY</td>
      <td>NaN</td>
      <td>1</td>
      <td>10.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 12:43:40+00</td>
      <td>2003/06/24 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>PL</td>
      <td>1509 MARCY PL # #A</td>
      <td>1509 MARCY PL # A</td>
      <td>NaN</td>
      <td>1.001034e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1215.304688</td>
      <td>159.539483</td>
      <td>1509  MARCY PL # #A</td>
      <td>1509  MARCY PL [UNIT] #A</td>
    </tr>
    <tr>
      <th>150</th>
      <td>212</td>
      <td>NaN</td>
      <td>005S060412</td>
      <td>005S060412</td>
      <td>412</td>
      <td>005S06</td>
      <td>15460.0</td>
      <td>1720</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BAINBRIDGE</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1899/12/30 17:32:46+00</td>
      <td>2003/03/19 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1720 BAINBRIDGE ST # A</td>
      <td>1720 BAINBRIDGE ST # A</td>
      <td>NaN</td>
      <td>1.001079e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97.726562</td>
      <td>39.509506</td>
      <td>1720  BAINBRIDGE ST # A</td>
      <td>1720  BAINBRIDGE ST [UNIT] A</td>
    </tr>
    <tr>
      <th>536</th>
      <td>600</td>
      <td>A</td>
      <td>004S080306</td>
      <td>004S080306</td>
      <td>306</td>
      <td>004S08</td>
      <td>51520.0</td>
      <td>520</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>LOMBARD</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>2.0</td>
      <td>1899/12/30 08:35:48+00</td>
      <td>2003/03/21 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>520 LOMBARD ST # A</td>
      <td>520 LOMBARD ST # A</td>
      <td>NaN</td>
      <td>1.001335e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>86.175781</td>
      <td>39.172754</td>
      <td>520  LOMBARD ST # A</td>
      <td>520  LOMBARD ST [UNIT] A</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
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
      <th>574500</th>
      <td>606210</td>
      <td></td>
      <td>096N060061</td>
      <td>096N060061</td>
      <td>61</td>
      <td>096N06</td>
      <td>61860.0</td>
      <td>220</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>OSBORN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 17:12:35+00</td>
      <td>2003/03/24 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>220 OSBORN ST # A</td>
      <td>220 OSBORN ST # A</td>
      <td>NaN</td>
      <td>1.001405e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>315.203125</td>
      <td>83.286032</td>
      <td>220  OSBORN ST # A</td>
      <td>220  OSBORN ST [UNIT] A</td>
    </tr>
    <tr>
      <th>574615</th>
      <td>606325</td>
      <td></td>
      <td>054N130040</td>
      <td>054N130040</td>
      <td>40</td>
      <td>054N13</td>
      <td>71580.0</td>
      <td>800</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SEFFERT</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>2.0</td>
      <td>1899/12/30 16:10:22+00</td>
      <td>2003/05/26 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>800 SEFFERT ST</td>
      <td>800 SEFFERT ST</td>
      <td>NaN</td>
      <td>1.001476e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>620.066406</td>
      <td>142.915572</td>
      <td>800  SEFFERT ST # B</td>
      <td>800  SEFFERT ST [UNIT] B</td>
    </tr>
    <tr>
      <th>574754</th>
      <td>606464</td>
      <td>NaN</td>
      <td>156N020881</td>
      <td>156N020881</td>
      <td>881</td>
      <td>156N02</td>
      <td>83225.0</td>
      <td>15144</td>
      <td>NaN</td>
      <td>202</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>WILDFLOWER</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2010/04/23 09:29:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>WAY</td>
      <td>15144 WILDFLOWER DR # 202</td>
      <td>15144 WILDFLOWER WAY # 202</td>
      <td>NaN</td>
      <td>1.001567e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>351.722656</td>
      <td>85.330568</td>
      <td>15144  WILDFLOWER WAY # 202</td>
      <td>15144  WILDFLOWER WAY [UNIT] 202</td>
    </tr>
    <tr>
      <th>574792</th>
      <td>606502</td>
      <td>NaN</td>
      <td>012N240225</td>
      <td>012N240225</td>
      <td>225</td>
      <td>012N24</td>
      <td>87890.0</td>
      <td>1642</td>
      <td>NaN</td>
      <td>38</td>
      <td>NaN</td>
      <td>N</td>
      <td>5TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1642 N 5TH ST # 38</td>
      <td>1642 N 5TH ST # 38</td>
      <td>NaN</td>
      <td>1.001594e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>121.984375</td>
      <td>50.841005</td>
      <td>1642 N 5TH ST # 38</td>
      <td>1642 N 5TH ST [UNIT] 38</td>
    </tr>
    <tr>
      <th>574814</th>
      <td>606525</td>
      <td>B</td>
      <td>012N050456</td>
      <td>012N050456</td>
      <td>456</td>
      <td>012N05</td>
      <td>87990.0</td>
      <td>1538</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>N</td>
      <td>10TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 17:44:10+00</td>
      <td>2003/05/22 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1538 N 10TH ST # B</td>
      <td>1538 N 10TH ST # B</td>
      <td>NaN</td>
      <td>1.001610e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>253.210938</td>
      <td>85.409621</td>
      <td>1538 N 10TH ST # B</td>
      <td>1538 N 10TH ST [UNIT] B</td>
    </tr>
  </tbody>
</table>
<p>7921 rows × 42 columns</p>
</div>




```python
# test case
dor_data[['ADDR_SOURCE','ADDR_STD','Address_Concat_dor','Address_Concat_dor_v1']].loc[dor_data['BASEREG'] == '006N090316'] 
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
      <th>ADDR_SOURCE</th>
      <th>ADDR_STD</th>
      <th>Address_Concat_dor</th>
      <th>Address_Concat_dor_v1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9840</th>
      <td>924-28 NEW MARKET ST # 3</td>
      <td>924-28 NEW MARKET ST # 3</td>
      <td>924-28  NEW MARKET ST # 3</td>
      <td>924-28  NEW MARKET ST [UNIT] 3</td>
    </tr>
  </tbody>
</table>
</div>




```python
"""

from passyunk.parser import PassyunkParser
standard_dor = []
base_add_dor = []
for i in dor_data.index:
    temp = dor_data.loc[i,'Address_Concat_dor']
    p = PassyunkParser()
    parsed = p.parse(temp)
    standard_dor.append(parsed['components']['output_address'])
    base_add_dor.append(parsed['components']['base_address'])

"""
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_304/2502934968.py in <module>
          5     temp = dor_data.loc[i,'Address_Concat_dor']
          6     p = PassyunkParser()
    ----> 7     parsed = p.parse(temp)
          8     standard_dor.append(parsed['components']['output_address'])
          9     base_add_dor.append(parsed['components']['base_address'])
    

    ~\anaconda3\lib\site-packages\passyunk\parser.py in parse(self, addr_str)
        690 
        691     def parse(self, addr_str):
    --> 692         parsed_out = parse(addr_str, self.MAX_RANGE)
        693 
        694         if self.return_dict:
    

    ~\anaconda3\lib\site-packages\passyunk\parser.py in parse(item, MAX_RANGE)
        377                     address_uber.type = AddrType.address
        378                 if address.street.name == '':
    --> 379                     raise ValueError('Parsed address does not have a street name: {}'.format(item))
        380             elif address_uber.type != AddrType.block:
        381                 # if the users doesn't have the centerline file, parser will still work
    

    ValueError: Parsed address does not have a street name: 0-0 #



```python
"""

dor_data['standardized_address_dor'] = standard_dor
dor_data['base_address_dor'] = base_add_dor

"""
```




    "\n\ndor_data['standardized_address_dor'] = standard_dor\ndor_data['base_address_dor'] = base_add_dor\n\n"




```python
from passyunk.parser import PassyunkParser
standard_dor_v1 = []
base_add_dor_v1 = []
for i in dor_data.index:
    temp_v1 = dor_data.loc[i,'Address_Concat_dor_v1']
    p = PassyunkParser()
    parsed = p.parse(temp_v1)
    standard_dor_v1.append(parsed['components']['output_address'])
    base_add_dor_v1.append(parsed['components']['base_address'])
```


```python
dor_data['standardized_address_dor_v1'] = standard_dor_v1
dor_data['base_address_dor_v1'] = base_add_dor_v1
```


```python
dor_data[['Address_Concat_dor_v1','ADDR_SOURCE','standardized_address_dor_v1','ADDR_STD']].loc[dor_data['UNIT'].notna()] 
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
      <th>Address_Concat_dor_v1</th>
      <th>ADDR_SOURCE</th>
      <th>standardized_address_dor_v1</th>
      <th>ADDR_STD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>56</th>
      <td>232  STAMPERS ST [UNIT] R</td>
      <td>232 STAMPERS ST # R</td>
      <td>232 STAMPERS ST UNIT R</td>
      <td>232 STAMPERS ST # R</td>
    </tr>
    <tr>
      <th>64</th>
      <td>1501  SNYDER AVE [UNIT] A</td>
      <td>1501 SNYDER AVE # A</td>
      <td>1501 SNYDER AVE UNIT A</td>
      <td>1501 SNYDER AVE # A</td>
    </tr>
    <tr>
      <th>67</th>
      <td>1509  MARCY PL [UNIT] #A</td>
      <td>1509 MARCY PL # #A</td>
      <td>1509 MARCY PL # A</td>
      <td>1509 MARCY PL # A</td>
    </tr>
    <tr>
      <th>150</th>
      <td>1720  BAINBRIDGE ST [UNIT] A</td>
      <td>1720 BAINBRIDGE ST # A</td>
      <td>1720 BAINBRIDGE ST UNIT A</td>
      <td>1720 BAINBRIDGE ST # A</td>
    </tr>
    <tr>
      <th>536</th>
      <td>520  LOMBARD ST [UNIT] A</td>
      <td>520 LOMBARD ST # A</td>
      <td>520 LOMBARD ST UNIT A</td>
      <td>520 LOMBARD ST # A</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>574500</th>
      <td>220  OSBORN ST [UNIT] A</td>
      <td>220 OSBORN ST # A</td>
      <td>220 OSBORN ST UNIT A</td>
      <td>220 OSBORN ST # A</td>
    </tr>
    <tr>
      <th>574615</th>
      <td>800  SEFFERT ST [UNIT] B</td>
      <td>800 SEFFERT ST</td>
      <td>800 SEFFERT ST UNIT B</td>
      <td>800 SEFFERT ST</td>
    </tr>
    <tr>
      <th>574754</th>
      <td>15144  WILDFLOWER WAY [UNIT] 202</td>
      <td>15144 WILDFLOWER DR # 202</td>
      <td>15144 WILDFLOWER WAY UNIT 202</td>
      <td>15144 WILDFLOWER WAY # 202</td>
    </tr>
    <tr>
      <th>574792</th>
      <td>1642 N 5TH ST [UNIT] 38</td>
      <td>1642 N 5TH ST # 38</td>
      <td>1642 N 5TH ST UNIT 38</td>
      <td>1642 N 5TH ST # 38</td>
    </tr>
    <tr>
      <th>574814</th>
      <td>1538 N 10TH ST [UNIT] B</td>
      <td>1538 N 10TH ST # B</td>
      <td>1538 N 10TH ST UNIT B</td>
      <td>1538 N 10TH ST # B</td>
    </tr>
  </tbody>
</table>
<p>7921 rows × 4 columns</p>
</div>




```python
dor_data.loc[dor_data['UNIT'].notna()] 
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
      <th>OBJECTID</th>
      <th>RECSUB</th>
      <th>BASEREG</th>
      <th>MAPREG</th>
      <th>PARCEL</th>
      <th>RECMAP</th>
      <th>STCOD</th>
      <th>HOUSE</th>
      <th>SUF</th>
      <th>UNIT</th>
      <th>STEX</th>
      <th>STDIR</th>
      <th>STNAM</th>
      <th>STDESSUF</th>
      <th>ELEV_FLAG</th>
      <th>TOPELEV</th>
      <th>BOTELEV</th>
      <th>CONDOFLAG</th>
      <th>MATCHFLAG</th>
      <th>INACTDATE</th>
      <th>ORIG_DATE</th>
      <th>STATUS</th>
      <th>GEOID</th>
      <th>STDES</th>
      <th>ADDR_SOURCE</th>
      <th>ADDR_STD</th>
      <th>COMMENTS</th>
      <th>PIN</th>
      <th>FRAC</th>
      <th>UNIT_TYPE</th>
      <th>STEX_FRAC</th>
      <th>STEX_SUF</th>
      <th>SEPARATED_RIGHTS</th>
      <th>MUNIMENT_TYPE</th>
      <th>MUNIMENT_ID</th>
      <th>DOR_REVIEW</th>
      <th>OPA_REVIEW</th>
      <th>PWD_REVIEW</th>
      <th>Shape__Area</th>
      <th>Shape__Length</th>
      <th>Address_Concat_dor</th>
      <th>Address_Concat_dor_v1</th>
      <th>standardized_address_dor_v1</th>
      <th>base_address_dor_v1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>56</th>
      <td>118</td>
      <td>A</td>
      <td>003S050342</td>
      <td>003S050342</td>
      <td>342</td>
      <td>003S05</td>
      <td>74300.0</td>
      <td>232</td>
      <td>NaN</td>
      <td>R</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>STAMPERS</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>2.0</td>
      <td>1899/12/30 08:35:48+00</td>
      <td>2003/03/21 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>232 STAMPERS ST # R</td>
      <td>232 STAMPERS ST # R</td>
      <td>NaN</td>
      <td>1.001021e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>39.222656</td>
      <td>25.691489</td>
      <td>232  STAMPERS ST # R</td>
      <td>232  STAMPERS ST [UNIT] R</td>
      <td>232 STAMPERS ST UNIT R</td>
      <td>232 STAMPERS ST</td>
    </tr>
    <tr>
      <th>64</th>
      <td>126</td>
      <td></td>
      <td>016S110191</td>
      <td>016S110191</td>
      <td>191</td>
      <td>016S11</td>
      <td>73220.0</td>
      <td>1501</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SNYDER</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 19:00:55+00</td>
      <td>2003/05/06 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>AVE</td>
      <td>1501 SNYDER AVE # A</td>
      <td>1501 SNYDER AVE # A</td>
      <td>NaN</td>
      <td>1.001028e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>308.687500</td>
      <td>72.789093</td>
      <td>1501  SNYDER AVE # A</td>
      <td>1501  SNYDER AVE [UNIT] A</td>
      <td>1501 SNYDER AVE UNIT A</td>
      <td>1501 SNYDER AVE</td>
    </tr>
    <tr>
      <th>67</th>
      <td>129</td>
      <td></td>
      <td>160N190159</td>
      <td>160N190159</td>
      <td>159</td>
      <td>160N19</td>
      <td>53435.0</td>
      <td>1509</td>
      <td>NaN</td>
      <td>#A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>MARCY</td>
      <td>NaN</td>
      <td>1</td>
      <td>10.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 12:43:40+00</td>
      <td>2003/06/24 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>PL</td>
      <td>1509 MARCY PL # #A</td>
      <td>1509 MARCY PL # A</td>
      <td>NaN</td>
      <td>1.001034e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1215.304688</td>
      <td>159.539483</td>
      <td>1509  MARCY PL # #A</td>
      <td>1509  MARCY PL [UNIT] #A</td>
      <td>1509 MARCY PL # A</td>
      <td>1509 MARCY PL</td>
    </tr>
    <tr>
      <th>150</th>
      <td>212</td>
      <td>NaN</td>
      <td>005S060412</td>
      <td>005S060412</td>
      <td>412</td>
      <td>005S06</td>
      <td>15460.0</td>
      <td>1720</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BAINBRIDGE</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1899/12/30 17:32:46+00</td>
      <td>2003/03/19 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1720 BAINBRIDGE ST # A</td>
      <td>1720 BAINBRIDGE ST # A</td>
      <td>NaN</td>
      <td>1.001079e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>97.726562</td>
      <td>39.509506</td>
      <td>1720  BAINBRIDGE ST # A</td>
      <td>1720  BAINBRIDGE ST [UNIT] A</td>
      <td>1720 BAINBRIDGE ST UNIT A</td>
      <td>1720 BAINBRIDGE ST</td>
    </tr>
    <tr>
      <th>536</th>
      <td>600</td>
      <td>A</td>
      <td>004S080306</td>
      <td>004S080306</td>
      <td>306</td>
      <td>004S08</td>
      <td>51520.0</td>
      <td>520</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>LOMBARD</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>2.0</td>
      <td>1899/12/30 08:35:48+00</td>
      <td>2003/03/21 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>520 LOMBARD ST # A</td>
      <td>520 LOMBARD ST # A</td>
      <td>NaN</td>
      <td>1.001335e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>86.175781</td>
      <td>39.172754</td>
      <td>520  LOMBARD ST # A</td>
      <td>520  LOMBARD ST [UNIT] A</td>
      <td>520 LOMBARD ST UNIT A</td>
      <td>520 LOMBARD ST</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
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
      <th>574500</th>
      <td>606210</td>
      <td></td>
      <td>096N060061</td>
      <td>096N060061</td>
      <td>61</td>
      <td>096N06</td>
      <td>61860.0</td>
      <td>220</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>OSBORN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 17:12:35+00</td>
      <td>2003/03/24 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>220 OSBORN ST # A</td>
      <td>220 OSBORN ST # A</td>
      <td>NaN</td>
      <td>1.001405e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>315.203125</td>
      <td>83.286032</td>
      <td>220  OSBORN ST # A</td>
      <td>220  OSBORN ST [UNIT] A</td>
      <td>220 OSBORN ST UNIT A</td>
      <td>220 OSBORN ST</td>
    </tr>
    <tr>
      <th>574615</th>
      <td>606325</td>
      <td></td>
      <td>054N130040</td>
      <td>054N130040</td>
      <td>40</td>
      <td>054N13</td>
      <td>71580.0</td>
      <td>800</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SEFFERT</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>2.0</td>
      <td>1899/12/30 16:10:22+00</td>
      <td>2003/05/26 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>800 SEFFERT ST</td>
      <td>800 SEFFERT ST</td>
      <td>NaN</td>
      <td>1.001476e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>620.066406</td>
      <td>142.915572</td>
      <td>800  SEFFERT ST # B</td>
      <td>800  SEFFERT ST [UNIT] B</td>
      <td>800 SEFFERT ST UNIT B</td>
      <td>800 SEFFERT ST</td>
    </tr>
    <tr>
      <th>574754</th>
      <td>606464</td>
      <td>NaN</td>
      <td>156N020881</td>
      <td>156N020881</td>
      <td>881</td>
      <td>156N02</td>
      <td>83225.0</td>
      <td>15144</td>
      <td>NaN</td>
      <td>202</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>WILDFLOWER</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1899/12/30 00:00:00+00</td>
      <td>2010/04/23 09:29:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>WAY</td>
      <td>15144 WILDFLOWER DR # 202</td>
      <td>15144 WILDFLOWER WAY # 202</td>
      <td>NaN</td>
      <td>1.001567e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>351.722656</td>
      <td>85.330568</td>
      <td>15144  WILDFLOWER WAY # 202</td>
      <td>15144  WILDFLOWER WAY [UNIT] 202</td>
      <td>15144 WILDFLOWER WAY UNIT 202</td>
      <td>15144 WILDFLOWER WAY</td>
    </tr>
    <tr>
      <th>574792</th>
      <td>606502</td>
      <td>NaN</td>
      <td>012N240225</td>
      <td>012N240225</td>
      <td>225</td>
      <td>012N24</td>
      <td>87890.0</td>
      <td>1642</td>
      <td>NaN</td>
      <td>38</td>
      <td>NaN</td>
      <td>N</td>
      <td>5TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1642 N 5TH ST # 38</td>
      <td>1642 N 5TH ST # 38</td>
      <td>NaN</td>
      <td>1.001594e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>121.984375</td>
      <td>50.841005</td>
      <td>1642 N 5TH ST # 38</td>
      <td>1642 N 5TH ST [UNIT] 38</td>
      <td>1642 N 5TH ST UNIT 38</td>
      <td>1642 N 5TH ST</td>
    </tr>
    <tr>
      <th>574814</th>
      <td>606525</td>
      <td>B</td>
      <td>012N050456</td>
      <td>012N050456</td>
      <td>456</td>
      <td>012N05</td>
      <td>87990.0</td>
      <td>1538</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>N</td>
      <td>10TH</td>
      <td>NaN</td>
      <td>0</td>
      <td>9999.0</td>
      <td>-9999.0</td>
      <td>0</td>
      <td>1.0</td>
      <td>1899/12/30 17:44:10+00</td>
      <td>2003/05/22 00:00:00+00</td>
      <td>1</td>
      <td>NaN</td>
      <td>ST</td>
      <td>1538 N 10TH ST # B</td>
      <td>1538 N 10TH ST # B</td>
      <td>NaN</td>
      <td>1.001610e+09</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>253.210938</td>
      <td>85.409621</td>
      <td>1538 N 10TH ST # B</td>
      <td>1538 N 10TH ST [UNIT] B</td>
      <td>1538 N 10TH ST UNIT B</td>
      <td>1538 N 10TH ST</td>
    </tr>
  </tbody>
</table>
<p>7921 rows × 44 columns</p>
</div>



# Importing and formatting DOA dataset


```python
# url_opa= "https://www.opendataphilly.org/dataset/opa-property-assessments"
# data_opa_full = pd.read_csv(url_opa)
data_opa_full = pd.read_csv('C:/Users/rupam/Downloads/opa_properties_public.csv')


```

    C:\Users\rupam\anaconda3\lib\site-packages\IPython\core\interactiveshell.py:3444: DtypeWarning: Columns (4,12,19,21,25,54,67,69) have mixed types.Specify dtype option on import or set low_memory=False.
      exec(code_obj, self.user_global_ns, self.user_ns)
    


```python
data_opa_full.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 582028 entries, 0 to 582027
    Data columns (total 80 columns):
     #   Column                         Non-Null Count   Dtype  
    ---  ------                         --------------   -----  
     0   objectid                       582028 non-null  int64  
     1   assessment_date                576312 non-null  object 
     2   basements                      324960 non-null  object 
     3   beginning_point                570582 non-null  object 
     4   book_and_page                  575786 non-null  object 
     5   building_code                  581991 non-null  object 
     6   building_code_description      581955 non-null  object 
     7   category_code                  582028 non-null  int64  
     8   category_code_description      582024 non-null  object 
     9   census_tract                   581977 non-null  float64
     10  central_air                    286677 non-null  object 
     11  cross_reference                1668 non-null    float64
     12  date_exterior_condition        3060 non-null    object 
     13  depth                          578396 non-null  float64
     14  exempt_building                582028 non-null  float64
     15  exempt_land                    582028 non-null  float64
     16  exterior_condition             502026 non-null  float64
     17  fireplaces                     499795 non-null  float64
     18  frontage                       578387 non-null  float64
     19  fuel                           28794 non-null   object 
     20  garage_spaces                  499228 non-null  float64
     21  garage_type                    13356 non-null   object 
     22  general_construction           520097 non-null  object 
     23  geographic_ward                581977 non-null  float64
     24  homestead_exemption            582028 non-null  int64  
     25  house_extension                26443 non-null   object 
     26  house_number                   582028 non-null  int64  
     27  interior_condition             501777 non-null  float64
     28  location                       582028 non-null  object 
     29  mailing_address_1              112375 non-null  object 
     30  mailing_address_2              6321 non-null    object 
     31  mailing_care_of                26218 non-null   object 
     32  mailing_city_state             578142 non-null  object 
     33  mailing_street                 575727 non-null  object 
     34  mailing_zip                    576781 non-null  object 
     35  market_value                   582028 non-null  float64
     36  market_value_date              0 non-null       float64
     37  number_of_bathrooms            500123 non-null  float64
     38  number_of_bedrooms             502176 non-null  float64
     39  number_of_rooms                11761 non-null   float64
     40  number_stories                 502274 non-null  float64
     41  off_street_open                575317 non-null  float64
     42  other_building                 1250 non-null    object 
     43  owner_1                        582028 non-null  object 
     44  owner_2                        202835 non-null  object 
     45  parcel_number                  582028 non-null  int64  
     46  parcel_shape                   579004 non-null  object 
     47  quality_grade                  526475 non-null  object 
     48  recording_date                 578934 non-null  object 
     49  registry_number                573785 non-null  object 
     50  sale_date                      580306 non-null  object 
     51  sale_price                     580284 non-null  float64
     52  separate_utilities             26650 non-null   object 
     53  sewer                          10821 non-null   object 
     54  site_type                      2839 non-null    object 
     55  state_code                     581279 non-null  object 
     56  street_code                    581988 non-null  float64
     57  street_designation             582023 non-null  object 
     58  street_direction               226974 non-null  object 
     59  street_name                    582028 non-null  object 
     60  suffix                         2903 non-null    object 
     61  taxable_building               582027 non-null  float64
     62  taxable_land                   582028 non-null  float64
     63  topography                     543032 non-null  object 
     64  total_area                     579385 non-null  float64
     65  total_livable_area             540119 non-null  float64
     66  type_heater                    292672 non-null  object 
     67  unfinished                     79 non-null      object 
     68  unit                           40067 non-null   object 
     69  utility                        197 non-null     object 
     70  view_type                      561236 non-null  object 
     71  year_built                     540117 non-null  float64
     72  year_built_estimate            411559 non-null  object 
     73  zip_code                       581979 non-null  float64
     74  zoning                         581251 non-null  object 
     75  pin                            582028 non-null  int64  
     76  building_code_new              531282 non-null  object 
     77  building_code_description_new  491044 non-null  object 
     78  lat                            581980 non-null  float64
     79  lng                            581980 non-null  float64
    dtypes: float64(28), int64(6), object(46)
    memory usage: 355.2+ MB
    


```python
# making a deep copy of opa dataset and resetting the index
data_opa = data_opa_full.copy(deep = True)
```


```python
data_opa.reset_index(inplace=True,drop=True)
```


```python
data_opa_full.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 582028 entries, 0 to 582027
    Data columns (total 80 columns):
     #   Column                         Non-Null Count   Dtype  
    ---  ------                         --------------   -----  
     0   objectid                       582028 non-null  int64  
     1   assessment_date                576312 non-null  object 
     2   basements                      324960 non-null  object 
     3   beginning_point                570582 non-null  object 
     4   book_and_page                  575786 non-null  object 
     5   building_code                  581991 non-null  object 
     6   building_code_description      581955 non-null  object 
     7   category_code                  582028 non-null  int64  
     8   category_code_description      582024 non-null  object 
     9   census_tract                   581977 non-null  float64
     10  central_air                    286677 non-null  object 
     11  cross_reference                1668 non-null    float64
     12  date_exterior_condition        3060 non-null    object 
     13  depth                          578396 non-null  float64
     14  exempt_building                582028 non-null  float64
     15  exempt_land                    582028 non-null  float64
     16  exterior_condition             502026 non-null  float64
     17  fireplaces                     499795 non-null  float64
     18  frontage                       578387 non-null  float64
     19  fuel                           28794 non-null   object 
     20  garage_spaces                  499228 non-null  float64
     21  garage_type                    13356 non-null   object 
     22  general_construction           520097 non-null  object 
     23  geographic_ward                581977 non-null  float64
     24  homestead_exemption            582028 non-null  int64  
     25  house_extension                26443 non-null   object 
     26  house_number                   582028 non-null  int64  
     27  interior_condition             501777 non-null  float64
     28  location                       582028 non-null  object 
     29  mailing_address_1              112375 non-null  object 
     30  mailing_address_2              6321 non-null    object 
     31  mailing_care_of                26218 non-null   object 
     32  mailing_city_state             578142 non-null  object 
     33  mailing_street                 575727 non-null  object 
     34  mailing_zip                    576781 non-null  object 
     35  market_value                   582028 non-null  float64
     36  market_value_date              0 non-null       float64
     37  number_of_bathrooms            500123 non-null  float64
     38  number_of_bedrooms             502176 non-null  float64
     39  number_of_rooms                11761 non-null   float64
     40  number_stories                 502274 non-null  float64
     41  off_street_open                575317 non-null  float64
     42  other_building                 1250 non-null    object 
     43  owner_1                        582028 non-null  object 
     44  owner_2                        202835 non-null  object 
     45  parcel_number                  582028 non-null  int64  
     46  parcel_shape                   579004 non-null  object 
     47  quality_grade                  526475 non-null  object 
     48  recording_date                 578934 non-null  object 
     49  registry_number                573785 non-null  object 
     50  sale_date                      580306 non-null  object 
     51  sale_price                     580284 non-null  float64
     52  separate_utilities             26650 non-null   object 
     53  sewer                          10821 non-null   object 
     54  site_type                      2839 non-null    object 
     55  state_code                     581279 non-null  object 
     56  street_code                    581988 non-null  float64
     57  street_designation             582023 non-null  object 
     58  street_direction               226974 non-null  object 
     59  street_name                    582028 non-null  object 
     60  suffix                         2903 non-null    object 
     61  taxable_building               582027 non-null  float64
     62  taxable_land                   582028 non-null  float64
     63  topography                     543032 non-null  object 
     64  total_area                     579385 non-null  float64
     65  total_livable_area             540119 non-null  float64
     66  type_heater                    292672 non-null  object 
     67  unfinished                     79 non-null      object 
     68  unit                           40067 non-null   object 
     69  utility                        197 non-null     object 
     70  view_type                      561236 non-null  object 
     71  year_built                     540117 non-null  float64
     72  year_built_estimate            411559 non-null  object 
     73  zip_code                       581979 non-null  float64
     74  zoning                         581251 non-null  object 
     75  pin                            582028 non-null  int64  
     76  building_code_new              531282 non-null  object 
     77  building_code_description_new  491044 non-null  object 
     78  lat                            581980 non-null  float64
     79  lng                            581980 non-null  float64
    dtypes: float64(28), int64(6), object(46)
    memory usage: 355.2+ MB
    


```python
data_opa.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 582028 entries, 0 to 582027
    Data columns (total 80 columns):
     #   Column                         Non-Null Count   Dtype  
    ---  ------                         --------------   -----  
     0   objectid                       582028 non-null  int64  
     1   assessment_date                576312 non-null  object 
     2   basements                      324960 non-null  object 
     3   beginning_point                570582 non-null  object 
     4   book_and_page                  575786 non-null  object 
     5   building_code                  581991 non-null  object 
     6   building_code_description      581955 non-null  object 
     7   category_code                  582028 non-null  int64  
     8   category_code_description      582024 non-null  object 
     9   census_tract                   581977 non-null  float64
     10  central_air                    286677 non-null  object 
     11  cross_reference                1668 non-null    float64
     12  date_exterior_condition        3060 non-null    object 
     13  depth                          578396 non-null  float64
     14  exempt_building                582028 non-null  float64
     15  exempt_land                    582028 non-null  float64
     16  exterior_condition             502026 non-null  float64
     17  fireplaces                     499795 non-null  float64
     18  frontage                       578387 non-null  float64
     19  fuel                           28794 non-null   object 
     20  garage_spaces                  499228 non-null  float64
     21  garage_type                    13356 non-null   object 
     22  general_construction           520097 non-null  object 
     23  geographic_ward                581977 non-null  float64
     24  homestead_exemption            582028 non-null  int64  
     25  house_extension                26443 non-null   object 
     26  house_number                   582028 non-null  int64  
     27  interior_condition             501777 non-null  float64
     28  location                       582028 non-null  object 
     29  mailing_address_1              112375 non-null  object 
     30  mailing_address_2              6321 non-null    object 
     31  mailing_care_of                26218 non-null   object 
     32  mailing_city_state             578142 non-null  object 
     33  mailing_street                 575727 non-null  object 
     34  mailing_zip                    576781 non-null  object 
     35  market_value                   582028 non-null  float64
     36  market_value_date              0 non-null       float64
     37  number_of_bathrooms            500123 non-null  float64
     38  number_of_bedrooms             502176 non-null  float64
     39  number_of_rooms                11761 non-null   float64
     40  number_stories                 502274 non-null  float64
     41  off_street_open                575317 non-null  float64
     42  other_building                 1250 non-null    object 
     43  owner_1                        582028 non-null  object 
     44  owner_2                        202835 non-null  object 
     45  parcel_number                  582028 non-null  int64  
     46  parcel_shape                   579004 non-null  object 
     47  quality_grade                  526475 non-null  object 
     48  recording_date                 578934 non-null  object 
     49  registry_number                573785 non-null  object 
     50  sale_date                      580306 non-null  object 
     51  sale_price                     580284 non-null  float64
     52  separate_utilities             26650 non-null   object 
     53  sewer                          10821 non-null   object 
     54  site_type                      2839 non-null    object 
     55  state_code                     581279 non-null  object 
     56  street_code                    581988 non-null  float64
     57  street_designation             582023 non-null  object 
     58  street_direction               226974 non-null  object 
     59  street_name                    582028 non-null  object 
     60  suffix                         2903 non-null    object 
     61  taxable_building               582027 non-null  float64
     62  taxable_land                   582028 non-null  float64
     63  topography                     543032 non-null  object 
     64  total_area                     579385 non-null  float64
     65  total_livable_area             540119 non-null  float64
     66  type_heater                    292672 non-null  object 
     67  unfinished                     79 non-null      object 
     68  unit                           40067 non-null   object 
     69  utility                        197 non-null     object 
     70  view_type                      561236 non-null  object 
     71  year_built                     540117 non-null  float64
     72  year_built_estimate            411559 non-null  object 
     73  zip_code                       581979 non-null  float64
     74  zoning                         581251 non-null  object 
     75  pin                            582028 non-null  int64  
     76  building_code_new              531282 non-null  object 
     77  building_code_description_new  491044 non-null  object 
     78  lat                            581980 non-null  float64
     79  lng                            581980 non-null  float64
    dtypes: float64(28), int64(6), object(46)
    memory usage: 355.2+ MB
    


```python
data_opa['Address_concat_opa']  = data_opa['location'] + (' # ' + data_opa['unit']).fillna('')
```


```python
data_opa['Address_concat_opa_v1']  = data_opa['location'] + (' [UNIT] ' + data_opa['unit']).fillna('')
```


```python
data_opa.loc[data_opa['unit'].notna()] 
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
      <th>objectid</th>
      <th>assessment_date</th>
      <th>basements</th>
      <th>beginning_point</th>
      <th>book_and_page</th>
      <th>building_code</th>
      <th>building_code_description</th>
      <th>category_code</th>
      <th>category_code_description</th>
      <th>census_tract</th>
      <th>central_air</th>
      <th>cross_reference</th>
      <th>date_exterior_condition</th>
      <th>depth</th>
      <th>exempt_building</th>
      <th>exempt_land</th>
      <th>exterior_condition</th>
      <th>fireplaces</th>
      <th>frontage</th>
      <th>fuel</th>
      <th>garage_spaces</th>
      <th>garage_type</th>
      <th>general_construction</th>
      <th>geographic_ward</th>
      <th>homestead_exemption</th>
      <th>house_extension</th>
      <th>house_number</th>
      <th>interior_condition</th>
      <th>location</th>
      <th>mailing_address_1</th>
      <th>mailing_address_2</th>
      <th>mailing_care_of</th>
      <th>mailing_city_state</th>
      <th>mailing_street</th>
      <th>mailing_zip</th>
      <th>market_value</th>
      <th>market_value_date</th>
      <th>number_of_bathrooms</th>
      <th>number_of_bedrooms</th>
      <th>number_of_rooms</th>
      <th>number_stories</th>
      <th>off_street_open</th>
      <th>other_building</th>
      <th>owner_1</th>
      <th>owner_2</th>
      <th>parcel_number</th>
      <th>parcel_shape</th>
      <th>quality_grade</th>
      <th>recording_date</th>
      <th>registry_number</th>
      <th>sale_date</th>
      <th>sale_price</th>
      <th>separate_utilities</th>
      <th>sewer</th>
      <th>site_type</th>
      <th>state_code</th>
      <th>street_code</th>
      <th>street_designation</th>
      <th>street_direction</th>
      <th>street_name</th>
      <th>suffix</th>
      <th>taxable_building</th>
      <th>taxable_land</th>
      <th>topography</th>
      <th>total_area</th>
      <th>total_livable_area</th>
      <th>type_heater</th>
      <th>unfinished</th>
      <th>unit</th>
      <th>utility</th>
      <th>view_type</th>
      <th>year_built</th>
      <th>year_built_estimate</th>
      <th>zip_code</th>
      <th>zoning</th>
      <th>pin</th>
      <th>building_code_new</th>
      <th>building_code_description_new</th>
      <th>lat</th>
      <th>lng</th>
      <th>Address_concat_opa</th>
      <th>Address_concat_opa_v1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>165</th>
      <td>248457141</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>325' SW WINGATE ST</td>
      <td>NaN</td>
      <td>SI</td>
      <td>VACANT LAND INDUST &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>891.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>180.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>65.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>8305</td>
      <td>NaN</td>
      <td>8305 TORRESDALE AVE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>TUX  AUGUSTINE DE FINIS E</td>
      <td>PHILADELPHIA PA</td>
      <td>3835 PEARSON AVE</td>
      <td>19114</td>
      <td>169000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1087.0</td>
      <td>NaN</td>
      <td>AUGUSTINE R DE FINIS</td>
      <td>ANTOINETTE M</td>
      <td>885971240</td>
      <td>E</td>
      <td>NaN</td>
      <td>2069-04-17 00:00:00</td>
      <td>NaN</td>
      <td>2069-04-17 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>77600.0</td>
      <td>AVE</td>
      <td>NaN</td>
      <td>TORRESDALE</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>169000.0</td>
      <td>F</td>
      <td>9389.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19136.0</td>
      <td>I2</td>
      <td>1001526386</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.017075</td>
      <td>40.039042</td>
      <td>8305 TORRESDALE AVE # A</td>
      <td>8305 TORRESDALE AVE [UNIT] A</td>
    </tr>
    <tr>
      <th>370</th>
      <td>248457394</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>636' 5/8" N HALDEMAN</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>356.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>184.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>223.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>58.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>9903</td>
      <td>NaN</td>
      <td>9903 BUSTLETON AVE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Peco Energy</td>
      <td>PHILADELPHIA PA</td>
      <td>2301 Market St</td>
      <td>19107</td>
      <td>1179500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3214.0</td>
      <td>NaN</td>
      <td>PHILA ELECTRIC CO</td>
      <td>NaN</td>
      <td>885665280</td>
      <td>C</td>
      <td>NaN</td>
      <td>2063-06-27 00:00:00</td>
      <td>NaN</td>
      <td>2063-06-27 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>20020.0</td>
      <td>AVE</td>
      <td>NaN</td>
      <td>BUSTLETON</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1179500.0</td>
      <td>F</td>
      <td>20851.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19115.0</td>
      <td>CA1</td>
      <td>1001111843</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.030120</td>
      <td>40.096488</td>
      <td>9903 BUSTLETON AVE # B</td>
      <td>9903 BUSTLETON AVE [UNIT] B</td>
    </tr>
    <tr>
      <th>462</th>
      <td>248457422</td>
      <td>2022-04-18 08:55:40</td>
      <td>NaN</td>
      <td>239'10 1/4" E PECHIN</td>
      <td>NaN</td>
      <td>B30</td>
      <td>DET W/GAR 2 STY MASONRY</td>
      <td>1</td>
      <td>SINGLE FAMILY</td>
      <td>213.0</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>85688.0</td>
      <td>15122.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>A</td>
      <td>21.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>419</td>
      <td>4.0</td>
      <td>419 GREEN LN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>419 GREEN LN</td>
      <td>19128-3305</td>
      <td>447000.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>299.0</td>
      <td>NaN</td>
      <td>MANAYUNK ART CENTER</td>
      <td>NaN</td>
      <td>212121005</td>
      <td>A</td>
      <td>B-</td>
      <td>2062-04-27 00:00:00</td>
      <td>NaN</td>
      <td>2062-04-27 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>38380.0</td>
      <td>LN</td>
      <td>NaN</td>
      <td>GREEN</td>
      <td>NaN</td>
      <td>271912.0</td>
      <td>74278.0</td>
      <td>F</td>
      <td>5050.0</td>
      <td>3560.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>1890.0</td>
      <td>Y</td>
      <td>19128.0</td>
      <td>RSA2</td>
      <td>1001252817</td>
      <td>14</td>
      <td>OLD STYLE</td>
      <td>-75.218041</td>
      <td>40.032179</td>
      <td>419 GREEN LN # A</td>
      <td>419 GREEN LN [UNIT] A</td>
    </tr>
    <tr>
      <th>527</th>
      <td>248457471</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SEC 8TH ST</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>75.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>198.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>0</td>
      <td>30.0</td>
      <td>716</td>
      <td>NaN</td>
      <td>716-30 SPRUCE ST</td>
      <td>ACCOUNTING DEPT</td>
      <td>NaN</td>
      <td>PENNSYLVANIA HOSPITAL</td>
      <td>PHILADELPHIA PA</td>
      <td>800 SPRUCE ST</td>
      <td>19107</td>
      <td>969800.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>984.0</td>
      <td>NaN</td>
      <td>THE CONTRIBUTORS TO PENNA</td>
      <td>HOSPITAL</td>
      <td>883102010</td>
      <td>A</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>73960.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>SPRUCE</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>969800.0</td>
      <td>F</td>
      <td>14687.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19106.0</td>
      <td>RM4</td>
      <td>1001495769</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.154357</td>
      <td>39.945521</td>
      <td>716-30 SPRUCE ST # B</td>
      <td>716-30 SPRUCE ST [UNIT] B</td>
    </tr>
    <tr>
      <th>528</th>
      <td>248457472</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>NEC 8TH ST</td>
      <td>NaN</td>
      <td>3</td>
      <td>AIR RIGHTS COMMERCIAL</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>0</td>
      <td>33.0</td>
      <td>727</td>
      <td>NaN</td>
      <td>727-33 DELANCEY ST</td>
      <td>ACCOUNTING DEPT</td>
      <td>NaN</td>
      <td>PENNA HOSPITAL</td>
      <td>PHILADELPHIA PA</td>
      <td>800 SPRUCE ST</td>
      <td>19107</td>
      <td>282700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>THE CONTRIBUTORS TO</td>
      <td>THE PENNA HOSP</td>
      <td>883418260</td>
      <td>E</td>
      <td>C</td>
      <td>2059-04-08 00:00:00</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>18800006.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>27980.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>DELANCEY</td>
      <td>NaN</td>
      <td>180928.0</td>
      <td>101772.0</td>
      <td>F</td>
      <td>4445.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>19106.0</td>
      <td>RM4</td>
      <td>1001174201</td>
      <td>238</td>
      <td>MEDICAL OFFICE BLDNG</td>
      <td>-75.154646</td>
      <td>39.945025</td>
      <td>727-33 DELANCEY ST # A</td>
      <td>727-33 DELANCEY ST [UNIT] A</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
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
      <th>581865</th>
      <td>249034504</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>6353000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076630</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174S/O 166</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>5082400.0</td>
      <td>1270600.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>21806.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>800</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347385</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # 800</td>
      <td>3600 MARKET ST [UNIT] 800</td>
    </tr>
    <tr>
      <th>581866</th>
      <td>249034505</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>6353000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076625</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174S/O166</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>5082400.0</td>
      <td>1270600.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>21806.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>700</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347383</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # 700</td>
      <td>3600 MARKET ST [UNIT] 700</td>
    </tr>
    <tr>
      <th>581867</th>
      <td>249034506</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>3875100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076610</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>3100080.0</td>
      <td>775020.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>13301.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>G10</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347395</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # G10</td>
      <td>3600 MARKET ST [UNIT] G10</td>
    </tr>
    <tr>
      <th>581868</th>
      <td>249034507</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>NaN</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>255700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076600</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>204560.0</td>
      <td>51140.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>2711.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B50</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347387</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # B50</td>
      <td>3600 MARKET ST [UNIT] B50</td>
    </tr>
    <tr>
      <th>581989</th>
      <td>249036451</td>
      <td>2021-10-19 09:02:58</td>
      <td>NaN</td>
      <td>2256'8"M/L SE MONT CO</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>220.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>143200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>8</td>
      <td>NaN</td>
      <td>8 RIVER RD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>NaN</td>
      <td>19152</td>
      <td>143200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CITY OF PHILA DEPT OF PUB PROP WATER DEP</td>
      <td>NaN</td>
      <td>784386602</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>150N190146</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>68780.0</td>
      <td>RD</td>
      <td>NaN</td>
      <td>RIVER</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A1</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19128.0</td>
      <td>RMX1</td>
      <td>1001676987</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.258453</td>
      <td>40.049893</td>
      <td>8 RIVER RD # A1</td>
      <td>8 RIVER RD [UNIT] A1</td>
    </tr>
  </tbody>
</table>
<p>40067 rows × 82 columns</p>
</div>




```python
from passyunk.parser import PassyunkParser
standard_opa = []
base_add_opa = []
for i in data_opa.index:
    temp_add = data_opa.loc[i,'Address_concat_opa']
    p = PassyunkParser()
    parsed = p.parse(temp_add)
    standard_opa.append(parsed['components']['output_address'])
    base_add_opa.append(parsed['components']['base_address'])

```


```python
data_opa['standardized_address_opa'] = standard_opa
data_opa['base_address_opa'] = base_add_opa
```


```python
data_opa.head()
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
      <th>objectid</th>
      <th>assessment_date</th>
      <th>basements</th>
      <th>beginning_point</th>
      <th>book_and_page</th>
      <th>building_code</th>
      <th>building_code_description</th>
      <th>category_code</th>
      <th>category_code_description</th>
      <th>census_tract</th>
      <th>central_air</th>
      <th>cross_reference</th>
      <th>date_exterior_condition</th>
      <th>depth</th>
      <th>exempt_building</th>
      <th>exempt_land</th>
      <th>exterior_condition</th>
      <th>fireplaces</th>
      <th>frontage</th>
      <th>fuel</th>
      <th>garage_spaces</th>
      <th>garage_type</th>
      <th>general_construction</th>
      <th>geographic_ward</th>
      <th>homestead_exemption</th>
      <th>house_extension</th>
      <th>house_number</th>
      <th>interior_condition</th>
      <th>location</th>
      <th>mailing_address_1</th>
      <th>mailing_address_2</th>
      <th>mailing_care_of</th>
      <th>mailing_city_state</th>
      <th>mailing_street</th>
      <th>mailing_zip</th>
      <th>market_value</th>
      <th>market_value_date</th>
      <th>number_of_bathrooms</th>
      <th>number_of_bedrooms</th>
      <th>number_of_rooms</th>
      <th>number_stories</th>
      <th>off_street_open</th>
      <th>other_building</th>
      <th>owner_1</th>
      <th>owner_2</th>
      <th>parcel_number</th>
      <th>parcel_shape</th>
      <th>quality_grade</th>
      <th>recording_date</th>
      <th>registry_number</th>
      <th>sale_date</th>
      <th>sale_price</th>
      <th>separate_utilities</th>
      <th>sewer</th>
      <th>site_type</th>
      <th>state_code</th>
      <th>street_code</th>
      <th>street_designation</th>
      <th>street_direction</th>
      <th>street_name</th>
      <th>suffix</th>
      <th>taxable_building</th>
      <th>taxable_land</th>
      <th>topography</th>
      <th>total_area</th>
      <th>total_livable_area</th>
      <th>type_heater</th>
      <th>unfinished</th>
      <th>unit</th>
      <th>utility</th>
      <th>view_type</th>
      <th>year_built</th>
      <th>year_built_estimate</th>
      <th>zip_code</th>
      <th>zoning</th>
      <th>pin</th>
      <th>building_code_new</th>
      <th>building_code_description_new</th>
      <th>lat</th>
      <th>lng</th>
      <th>Address_concat_opa</th>
      <th>Address_concat_opa_v1</th>
      <th>standardized_address_opa</th>
      <th>base_address_opa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>248457024</td>
      <td>2022-04-27 11:50:34</td>
      <td>NaN</td>
      <td>124'9 1/2" E GERMANTN</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>175.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>87.0</td>
      <td>0.0</td>
      <td>29000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>37.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>925</td>
      <td>NaN</td>
      <td>925 W SOMERSET ST</td>
      <td>MUNICIPAL SERVICES BLDG</td>
      <td>ROOM 1030</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>1401 JOHN F KENNEDY BLVD</td>
      <td>19107</td>
      <td>29000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1356.0</td>
      <td>NaN</td>
      <td>CITY OF PHILA</td>
      <td>NaN</td>
      <td>885458000</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>73280.0</td>
      <td>ST</td>
      <td>W</td>
      <td>SOMERSET</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>1305.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19133.0</td>
      <td>CMX2</td>
      <td>1001489682</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.146849</td>
      <td>39.994767</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
    </tr>
    <tr>
      <th>1</th>
      <td>248457025</td>
      <td>2022-04-27 11:50:37</td>
      <td>NaN</td>
      <td>175' N CLIFFORD ST</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>90.0</td>
      <td>0.0</td>
      <td>79500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1755</td>
      <td>NaN</td>
      <td>1755 N 31ST ST</td>
      <td>MUNICIPAL SERVICES BLDG</td>
      <td>ROOM 1030</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>1401 JOHN F KENNEDY BLVD</td>
      <td>19107</td>
      <td>79500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1650.0</td>
      <td>NaN</td>
      <td>CITY OF PHILA</td>
      <td>NaN</td>
      <td>324196601</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>88400.0</td>
      <td>ST</td>
      <td>N</td>
      <td>31ST</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>1260.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>RSA5</td>
      <td>1001648434</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.184591</td>
      <td>39.983481</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
    </tr>
    <tr>
      <th>2</th>
      <td>248457026</td>
      <td>2022-04-27 11:50:40</td>
      <td>NaN</td>
      <td>NWC COLUMBIA AVE</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>49.0</td>
      <td>0.0</td>
      <td>44600.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1700</td>
      <td>NaN</td>
      <td>1700 N NEWKIRK ST</td>
      <td>OF PHILADELPHIA</td>
      <td>16TH FLOOR</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>PHILADELPHIA PA</td>
      <td>1234 MARKET ST</td>
      <td>19107</td>
      <td>44600.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1259.0</td>
      <td>NaN</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>OF PHILADELPHIA</td>
      <td>324158601</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>59640.0</td>
      <td>ST</td>
      <td>N</td>
      <td>NEWKIRK</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>784.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>RSA5</td>
      <td>1001388974</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.180972</td>
      <td>39.981766</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
    </tr>
    <tr>
      <th>3</th>
      <td>248457027</td>
      <td>2022-04-27 11:50:38</td>
      <td>NaN</td>
      <td>30'8" N COLUMBIA AVE</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>65.0</td>
      <td>0.0</td>
      <td>64500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1705</td>
      <td>NaN</td>
      <td>1705 N 29TH ST</td>
      <td>OF PHILADELPHIA</td>
      <td>16TH FLOOR</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>PHILADELPHIA PA</td>
      <td>1234 MARKET ST</td>
      <td>19107</td>
      <td>64500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1575.0</td>
      <td>NaN</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>OF PHILADELPHIA</td>
      <td>324176801</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>88360.0</td>
      <td>ST</td>
      <td>N</td>
      <td>29TH</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>975.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>RSA5</td>
      <td>1001646785</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.181622</td>
      <td>39.981936</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
    </tr>
    <tr>
      <th>4</th>
      <td>248457028</td>
      <td>2022-04-27 11:50:40</td>
      <td>NaN</td>
      <td>SWC MONTGOMERY ST</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>68.0</td>
      <td>0.0</td>
      <td>4900.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1766</td>
      <td>NaN</td>
      <td>1766 N 28TH ST</td>
      <td>OF PHILADELPHIA</td>
      <td>16TH FLOOR</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>PHILADELPHIA PA</td>
      <td>1234 MARKET ST</td>
      <td>19107</td>
      <td>4900.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1083.0</td>
      <td>NaN</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>OF PHILADELPHIA</td>
      <td>324150201</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>88340.0</td>
      <td>ST</td>
      <td>N</td>
      <td>28TH</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>1042.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>CMX1</td>
      <td>1001645495</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.180171</td>
      <td>39.983045</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
    </tr>
  </tbody>
</table>
</div>




```python
data_opa.loc[data_opa['unit'].notna()] 
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
      <th>objectid</th>
      <th>assessment_date</th>
      <th>basements</th>
      <th>beginning_point</th>
      <th>book_and_page</th>
      <th>building_code</th>
      <th>building_code_description</th>
      <th>category_code</th>
      <th>category_code_description</th>
      <th>census_tract</th>
      <th>central_air</th>
      <th>cross_reference</th>
      <th>date_exterior_condition</th>
      <th>depth</th>
      <th>exempt_building</th>
      <th>exempt_land</th>
      <th>exterior_condition</th>
      <th>fireplaces</th>
      <th>frontage</th>
      <th>fuel</th>
      <th>garage_spaces</th>
      <th>garage_type</th>
      <th>general_construction</th>
      <th>geographic_ward</th>
      <th>homestead_exemption</th>
      <th>house_extension</th>
      <th>house_number</th>
      <th>interior_condition</th>
      <th>location</th>
      <th>mailing_address_1</th>
      <th>mailing_address_2</th>
      <th>mailing_care_of</th>
      <th>mailing_city_state</th>
      <th>mailing_street</th>
      <th>mailing_zip</th>
      <th>market_value</th>
      <th>market_value_date</th>
      <th>number_of_bathrooms</th>
      <th>number_of_bedrooms</th>
      <th>number_of_rooms</th>
      <th>number_stories</th>
      <th>off_street_open</th>
      <th>other_building</th>
      <th>owner_1</th>
      <th>owner_2</th>
      <th>parcel_number</th>
      <th>parcel_shape</th>
      <th>quality_grade</th>
      <th>recording_date</th>
      <th>registry_number</th>
      <th>sale_date</th>
      <th>sale_price</th>
      <th>separate_utilities</th>
      <th>sewer</th>
      <th>site_type</th>
      <th>state_code</th>
      <th>street_code</th>
      <th>street_designation</th>
      <th>street_direction</th>
      <th>street_name</th>
      <th>suffix</th>
      <th>taxable_building</th>
      <th>taxable_land</th>
      <th>topography</th>
      <th>total_area</th>
      <th>total_livable_area</th>
      <th>type_heater</th>
      <th>unfinished</th>
      <th>unit</th>
      <th>utility</th>
      <th>view_type</th>
      <th>year_built</th>
      <th>year_built_estimate</th>
      <th>zip_code</th>
      <th>zoning</th>
      <th>pin</th>
      <th>building_code_new</th>
      <th>building_code_description_new</th>
      <th>lat</th>
      <th>lng</th>
      <th>Address_concat_opa</th>
      <th>Address_concat_opa_v1</th>
      <th>standardized_address_opa</th>
      <th>base_address_opa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>165</th>
      <td>248457141</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>325' SW WINGATE ST</td>
      <td>NaN</td>
      <td>SI</td>
      <td>VACANT LAND INDUST &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>891.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>180.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>65.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>8305</td>
      <td>NaN</td>
      <td>8305 TORRESDALE AVE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>TUX  AUGUSTINE DE FINIS E</td>
      <td>PHILADELPHIA PA</td>
      <td>3835 PEARSON AVE</td>
      <td>19114</td>
      <td>169000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1087.0</td>
      <td>NaN</td>
      <td>AUGUSTINE R DE FINIS</td>
      <td>ANTOINETTE M</td>
      <td>885971240</td>
      <td>E</td>
      <td>NaN</td>
      <td>2069-04-17 00:00:00</td>
      <td>NaN</td>
      <td>2069-04-17 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>77600.0</td>
      <td>AVE</td>
      <td>NaN</td>
      <td>TORRESDALE</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>169000.0</td>
      <td>F</td>
      <td>9389.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19136.0</td>
      <td>I2</td>
      <td>1001526386</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.017075</td>
      <td>40.039042</td>
      <td>8305 TORRESDALE AVE # A</td>
      <td>8305 TORRESDALE AVE [UNIT] A</td>
      <td>8305 TORRESDALE AVE # A</td>
      <td>8305 TORRESDALE AVE</td>
    </tr>
    <tr>
      <th>370</th>
      <td>248457394</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>636' 5/8" N HALDEMAN</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>356.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>184.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>223.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>58.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>9903</td>
      <td>NaN</td>
      <td>9903 BUSTLETON AVE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Peco Energy</td>
      <td>PHILADELPHIA PA</td>
      <td>2301 Market St</td>
      <td>19107</td>
      <td>1179500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3214.0</td>
      <td>NaN</td>
      <td>PHILA ELECTRIC CO</td>
      <td>NaN</td>
      <td>885665280</td>
      <td>C</td>
      <td>NaN</td>
      <td>2063-06-27 00:00:00</td>
      <td>NaN</td>
      <td>2063-06-27 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>20020.0</td>
      <td>AVE</td>
      <td>NaN</td>
      <td>BUSTLETON</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1179500.0</td>
      <td>F</td>
      <td>20851.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19115.0</td>
      <td>CA1</td>
      <td>1001111843</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.030120</td>
      <td>40.096488</td>
      <td>9903 BUSTLETON AVE # B</td>
      <td>9903 BUSTLETON AVE [UNIT] B</td>
      <td>9903 BUSTLETON AVE # B</td>
      <td>9903 BUSTLETON AVE</td>
    </tr>
    <tr>
      <th>462</th>
      <td>248457422</td>
      <td>2022-04-18 08:55:40</td>
      <td>NaN</td>
      <td>239'10 1/4" E PECHIN</td>
      <td>NaN</td>
      <td>B30</td>
      <td>DET W/GAR 2 STY MASONRY</td>
      <td>1</td>
      <td>SINGLE FAMILY</td>
      <td>213.0</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>85688.0</td>
      <td>15122.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>A</td>
      <td>21.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>419</td>
      <td>4.0</td>
      <td>419 GREEN LN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>419 GREEN LN</td>
      <td>19128-3305</td>
      <td>447000.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>299.0</td>
      <td>NaN</td>
      <td>MANAYUNK ART CENTER</td>
      <td>NaN</td>
      <td>212121005</td>
      <td>A</td>
      <td>B-</td>
      <td>2062-04-27 00:00:00</td>
      <td>NaN</td>
      <td>2062-04-27 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>38380.0</td>
      <td>LN</td>
      <td>NaN</td>
      <td>GREEN</td>
      <td>NaN</td>
      <td>271912.0</td>
      <td>74278.0</td>
      <td>F</td>
      <td>5050.0</td>
      <td>3560.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>1890.0</td>
      <td>Y</td>
      <td>19128.0</td>
      <td>RSA2</td>
      <td>1001252817</td>
      <td>14</td>
      <td>OLD STYLE</td>
      <td>-75.218041</td>
      <td>40.032179</td>
      <td>419 GREEN LN # A</td>
      <td>419 GREEN LN [UNIT] A</td>
      <td>419 GREEN LN # A</td>
      <td>419 GREEN LN</td>
    </tr>
    <tr>
      <th>527</th>
      <td>248457471</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SEC 8TH ST</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>75.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>198.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>0</td>
      <td>30.0</td>
      <td>716</td>
      <td>NaN</td>
      <td>716-30 SPRUCE ST</td>
      <td>ACCOUNTING DEPT</td>
      <td>NaN</td>
      <td>PENNSYLVANIA HOSPITAL</td>
      <td>PHILADELPHIA PA</td>
      <td>800 SPRUCE ST</td>
      <td>19107</td>
      <td>969800.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>984.0</td>
      <td>NaN</td>
      <td>THE CONTRIBUTORS TO PENNA</td>
      <td>HOSPITAL</td>
      <td>883102010</td>
      <td>A</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>73960.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>SPRUCE</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>969800.0</td>
      <td>F</td>
      <td>14687.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19106.0</td>
      <td>RM4</td>
      <td>1001495769</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.154357</td>
      <td>39.945521</td>
      <td>716-30 SPRUCE ST # B</td>
      <td>716-30 SPRUCE ST [UNIT] B</td>
      <td>716-30 SPRUCE ST # B</td>
      <td>716-30 SPRUCE ST</td>
    </tr>
    <tr>
      <th>528</th>
      <td>248457472</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>NEC 8TH ST</td>
      <td>NaN</td>
      <td>3</td>
      <td>AIR RIGHTS COMMERCIAL</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>0</td>
      <td>33.0</td>
      <td>727</td>
      <td>NaN</td>
      <td>727-33 DELANCEY ST</td>
      <td>ACCOUNTING DEPT</td>
      <td>NaN</td>
      <td>PENNA HOSPITAL</td>
      <td>PHILADELPHIA PA</td>
      <td>800 SPRUCE ST</td>
      <td>19107</td>
      <td>282700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>THE CONTRIBUTORS TO</td>
      <td>THE PENNA HOSP</td>
      <td>883418260</td>
      <td>E</td>
      <td>C</td>
      <td>2059-04-08 00:00:00</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>18800006.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>27980.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>DELANCEY</td>
      <td>NaN</td>
      <td>180928.0</td>
      <td>101772.0</td>
      <td>F</td>
      <td>4445.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>19106.0</td>
      <td>RM4</td>
      <td>1001174201</td>
      <td>238</td>
      <td>MEDICAL OFFICE BLDNG</td>
      <td>-75.154646</td>
      <td>39.945025</td>
      <td>727-33 DELANCEY ST # A</td>
      <td>727-33 DELANCEY ST [UNIT] A</td>
      <td>727-33 DELANCEY ST # A</td>
      <td>727-33 DELANCEY ST</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
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
      <th>581865</th>
      <td>249034504</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>6353000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076630</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174S/O 166</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>5082400.0</td>
      <td>1270600.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>21806.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>800</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347385</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # 800</td>
      <td>3600 MARKET ST [UNIT] 800</td>
      <td>3600 MARKET ST # 800</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581866</th>
      <td>249034505</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>6353000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076625</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174S/O166</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>5082400.0</td>
      <td>1270600.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>21806.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>700</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347383</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # 700</td>
      <td>3600 MARKET ST [UNIT] 700</td>
      <td>3600 MARKET ST # 700</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581867</th>
      <td>249034506</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>3875100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076610</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>3100080.0</td>
      <td>775020.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>13301.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>G10</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347395</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # G10</td>
      <td>3600 MARKET ST [UNIT] G10</td>
      <td>3600 MARKET ST # G10</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581868</th>
      <td>249034507</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>NaN</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>255700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076600</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>204560.0</td>
      <td>51140.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>2711.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B50</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347387</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # B50</td>
      <td>3600 MARKET ST [UNIT] B50</td>
      <td>3600 MARKET ST # B50</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581989</th>
      <td>249036451</td>
      <td>2021-10-19 09:02:58</td>
      <td>NaN</td>
      <td>2256'8"M/L SE MONT CO</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>220.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>143200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>8</td>
      <td>NaN</td>
      <td>8 RIVER RD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>NaN</td>
      <td>19152</td>
      <td>143200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CITY OF PHILA DEPT OF PUB PROP WATER DEP</td>
      <td>NaN</td>
      <td>784386602</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>150N190146</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>68780.0</td>
      <td>RD</td>
      <td>NaN</td>
      <td>RIVER</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A1</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19128.0</td>
      <td>RMX1</td>
      <td>1001676987</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.258453</td>
      <td>40.049893</td>
      <td>8 RIVER RD # A1</td>
      <td>8 RIVER RD [UNIT] A1</td>
      <td>8 RIVER RD # A1</td>
      <td>8 RIVER RD</td>
    </tr>
  </tbody>
</table>
<p>40067 rows × 84 columns</p>
</div>




```python
from passyunk.parser import PassyunkParser
standard_opa_v1 = []
base_add_opa_v1 = []
for i in data_opa.index:
    temp_add_v1 = data_opa.loc[i,'Address_concat_opa_v1']
    p = PassyunkParser()
    parsed = p.parse(temp_add_v1)
    standard_opa_v1.append(parsed['components']['output_address'])
    base_add_opa_v1.append(parsed['components']['base_address'])

```


```python
data_opa['standardized_address_opa_v1'] = standard_opa_v1
data_opa['base_address_opa_v1'] = base_add_opa_v1
```


```python
data_opa.loc[data_opa['unit'].notna()] 
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
      <th>objectid</th>
      <th>assessment_date</th>
      <th>basements</th>
      <th>beginning_point</th>
      <th>book_and_page</th>
      <th>building_code</th>
      <th>building_code_description</th>
      <th>category_code</th>
      <th>category_code_description</th>
      <th>census_tract</th>
      <th>central_air</th>
      <th>cross_reference</th>
      <th>date_exterior_condition</th>
      <th>depth</th>
      <th>exempt_building</th>
      <th>exempt_land</th>
      <th>exterior_condition</th>
      <th>fireplaces</th>
      <th>frontage</th>
      <th>fuel</th>
      <th>garage_spaces</th>
      <th>garage_type</th>
      <th>general_construction</th>
      <th>geographic_ward</th>
      <th>homestead_exemption</th>
      <th>house_extension</th>
      <th>house_number</th>
      <th>interior_condition</th>
      <th>location</th>
      <th>mailing_address_1</th>
      <th>mailing_address_2</th>
      <th>mailing_care_of</th>
      <th>mailing_city_state</th>
      <th>mailing_street</th>
      <th>mailing_zip</th>
      <th>market_value</th>
      <th>market_value_date</th>
      <th>number_of_bathrooms</th>
      <th>number_of_bedrooms</th>
      <th>number_of_rooms</th>
      <th>number_stories</th>
      <th>off_street_open</th>
      <th>other_building</th>
      <th>owner_1</th>
      <th>owner_2</th>
      <th>parcel_number</th>
      <th>parcel_shape</th>
      <th>quality_grade</th>
      <th>recording_date</th>
      <th>registry_number</th>
      <th>sale_date</th>
      <th>sale_price</th>
      <th>separate_utilities</th>
      <th>sewer</th>
      <th>site_type</th>
      <th>state_code</th>
      <th>street_code</th>
      <th>street_designation</th>
      <th>street_direction</th>
      <th>street_name</th>
      <th>suffix</th>
      <th>taxable_building</th>
      <th>taxable_land</th>
      <th>topography</th>
      <th>total_area</th>
      <th>total_livable_area</th>
      <th>type_heater</th>
      <th>unfinished</th>
      <th>unit</th>
      <th>utility</th>
      <th>view_type</th>
      <th>year_built</th>
      <th>year_built_estimate</th>
      <th>zip_code</th>
      <th>zoning</th>
      <th>pin</th>
      <th>building_code_new</th>
      <th>building_code_description_new</th>
      <th>lat</th>
      <th>lng</th>
      <th>Address_concat_opa</th>
      <th>Address_concat_opa_v1</th>
      <th>standardized_address_opa</th>
      <th>base_address_opa</th>
      <th>standardized_address_opa_v1</th>
      <th>base_address_opa_v1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>165</th>
      <td>248457141</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>325' SW WINGATE ST</td>
      <td>NaN</td>
      <td>SI</td>
      <td>VACANT LAND INDUST &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>891.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>180.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>65.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>8305</td>
      <td>NaN</td>
      <td>8305 TORRESDALE AVE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>TUX  AUGUSTINE DE FINIS E</td>
      <td>PHILADELPHIA PA</td>
      <td>3835 PEARSON AVE</td>
      <td>19114</td>
      <td>169000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1087.0</td>
      <td>NaN</td>
      <td>AUGUSTINE R DE FINIS</td>
      <td>ANTOINETTE M</td>
      <td>885971240</td>
      <td>E</td>
      <td>NaN</td>
      <td>2069-04-17 00:00:00</td>
      <td>NaN</td>
      <td>2069-04-17 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>77600.0</td>
      <td>AVE</td>
      <td>NaN</td>
      <td>TORRESDALE</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>169000.0</td>
      <td>F</td>
      <td>9389.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19136.0</td>
      <td>I2</td>
      <td>1001526386</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.017075</td>
      <td>40.039042</td>
      <td>8305 TORRESDALE AVE # A</td>
      <td>8305 TORRESDALE AVE [UNIT] A</td>
      <td>8305 TORRESDALE AVE # A</td>
      <td>8305 TORRESDALE AVE</td>
      <td>8305 TORRESDALE AVE UNIT A</td>
      <td>8305 TORRESDALE AVE</td>
    </tr>
    <tr>
      <th>370</th>
      <td>248457394</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>636' 5/8" N HALDEMAN</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>356.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>184.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>223.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>58.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>9903</td>
      <td>NaN</td>
      <td>9903 BUSTLETON AVE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Peco Energy</td>
      <td>PHILADELPHIA PA</td>
      <td>2301 Market St</td>
      <td>19107</td>
      <td>1179500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3214.0</td>
      <td>NaN</td>
      <td>PHILA ELECTRIC CO</td>
      <td>NaN</td>
      <td>885665280</td>
      <td>C</td>
      <td>NaN</td>
      <td>2063-06-27 00:00:00</td>
      <td>NaN</td>
      <td>2063-06-27 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>20020.0</td>
      <td>AVE</td>
      <td>NaN</td>
      <td>BUSTLETON</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>1179500.0</td>
      <td>F</td>
      <td>20851.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19115.0</td>
      <td>CA1</td>
      <td>1001111843</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.030120</td>
      <td>40.096488</td>
      <td>9903 BUSTLETON AVE # B</td>
      <td>9903 BUSTLETON AVE [UNIT] B</td>
      <td>9903 BUSTLETON AVE # B</td>
      <td>9903 BUSTLETON AVE</td>
      <td>9903 BUSTLETON AVE UNIT B</td>
      <td>9903 BUSTLETON AVE</td>
    </tr>
    <tr>
      <th>462</th>
      <td>248457422</td>
      <td>2022-04-18 08:55:40</td>
      <td>NaN</td>
      <td>239'10 1/4" E PECHIN</td>
      <td>NaN</td>
      <td>B30</td>
      <td>DET W/GAR 2 STY MASONRY</td>
      <td>1</td>
      <td>SINGLE FAMILY</td>
      <td>213.0</td>
      <td>N</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>160.0</td>
      <td>85688.0</td>
      <td>15122.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>A</td>
      <td>21.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>419</td>
      <td>4.0</td>
      <td>419 GREEN LN</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>419 GREEN LN</td>
      <td>19128-3305</td>
      <td>447000.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>299.0</td>
      <td>NaN</td>
      <td>MANAYUNK ART CENTER</td>
      <td>NaN</td>
      <td>212121005</td>
      <td>A</td>
      <td>B-</td>
      <td>2062-04-27 00:00:00</td>
      <td>NaN</td>
      <td>2062-04-27 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>38380.0</td>
      <td>LN</td>
      <td>NaN</td>
      <td>GREEN</td>
      <td>NaN</td>
      <td>271912.0</td>
      <td>74278.0</td>
      <td>F</td>
      <td>5050.0</td>
      <td>3560.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>1890.0</td>
      <td>Y</td>
      <td>19128.0</td>
      <td>RSA2</td>
      <td>1001252817</td>
      <td>14</td>
      <td>OLD STYLE</td>
      <td>-75.218041</td>
      <td>40.032179</td>
      <td>419 GREEN LN # A</td>
      <td>419 GREEN LN [UNIT] A</td>
      <td>419 GREEN LN # A</td>
      <td>419 GREEN LN</td>
      <td>419 GREEN LN UNIT A</td>
      <td>419 GREEN LN</td>
    </tr>
    <tr>
      <th>527</th>
      <td>248457471</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SEC 8TH ST</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>75.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>198.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>0</td>
      <td>30.0</td>
      <td>716</td>
      <td>NaN</td>
      <td>716-30 SPRUCE ST</td>
      <td>ACCOUNTING DEPT</td>
      <td>NaN</td>
      <td>PENNSYLVANIA HOSPITAL</td>
      <td>PHILADELPHIA PA</td>
      <td>800 SPRUCE ST</td>
      <td>19107</td>
      <td>969800.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>984.0</td>
      <td>NaN</td>
      <td>THE CONTRIBUTORS TO PENNA</td>
      <td>HOSPITAL</td>
      <td>883102010</td>
      <td>A</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>73960.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>SPRUCE</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>969800.0</td>
      <td>F</td>
      <td>14687.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19106.0</td>
      <td>RM4</td>
      <td>1001495769</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.154357</td>
      <td>39.945521</td>
      <td>716-30 SPRUCE ST # B</td>
      <td>716-30 SPRUCE ST [UNIT] B</td>
      <td>716-30 SPRUCE ST # B</td>
      <td>716-30 SPRUCE ST</td>
      <td>716-30 SPRUCE ST UNIT B</td>
      <td>716-30 SPRUCE ST</td>
    </tr>
    <tr>
      <th>528</th>
      <td>248457472</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>NEC 8TH ST</td>
      <td>NaN</td>
      <td>3</td>
      <td>AIR RIGHTS COMMERCIAL</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>45.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>0</td>
      <td>33.0</td>
      <td>727</td>
      <td>NaN</td>
      <td>727-33 DELANCEY ST</td>
      <td>ACCOUNTING DEPT</td>
      <td>NaN</td>
      <td>PENNA HOSPITAL</td>
      <td>PHILADELPHIA PA</td>
      <td>800 SPRUCE ST</td>
      <td>19107</td>
      <td>282700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>THE CONTRIBUTORS TO</td>
      <td>THE PENNA HOSP</td>
      <td>883418260</td>
      <td>E</td>
      <td>C</td>
      <td>2059-04-08 00:00:00</td>
      <td>NaN</td>
      <td>2059-04-08 00:00:00</td>
      <td>18800006.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>27980.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>DELANCEY</td>
      <td>NaN</td>
      <td>180928.0</td>
      <td>101772.0</td>
      <td>F</td>
      <td>4445.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>NaN</td>
      <td>I</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>19106.0</td>
      <td>RM4</td>
      <td>1001174201</td>
      <td>238</td>
      <td>MEDICAL OFFICE BLDNG</td>
      <td>-75.154646</td>
      <td>39.945025</td>
      <td>727-33 DELANCEY ST # A</td>
      <td>727-33 DELANCEY ST [UNIT] A</td>
      <td>727-33 DELANCEY ST # A</td>
      <td>727-33 DELANCEY ST</td>
      <td>727-33 DELANCEY ST UNIT A</td>
      <td>727-33 DELANCEY ST</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
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
      <th>581865</th>
      <td>249034504</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>6353000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076630</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174S/O 166</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>5082400.0</td>
      <td>1270600.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>21806.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>800</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347385</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # 800</td>
      <td>3600 MARKET ST [UNIT] 800</td>
      <td>3600 MARKET ST # 800</td>
      <td>3600 MARKET ST</td>
      <td>3600 MARKET ST UNIT 800</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581866</th>
      <td>249034505</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>6353000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076625</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174S/O166</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>5082400.0</td>
      <td>1270600.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>21806.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>700</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347383</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # 700</td>
      <td>3600 MARKET ST [UNIT] 700</td>
      <td>3600 MARKET ST # 700</td>
      <td>3600 MARKET ST</td>
      <td>3600 MARKET ST UNIT 700</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581867</th>
      <td>249034506</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>1234567.0</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>3875100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076610</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>3100080.0</td>
      <td>775020.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>13301.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>G10</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347395</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # G10</td>
      <td>3600 MARKET ST [UNIT] G10</td>
      <td>3600 MARKET ST # G10</td>
      <td>3600 MARKET ST</td>
      <td>3600 MARKET ST UNIT G10</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581868</th>
      <td>249034507</td>
      <td>2021-07-16 18:15:31</td>
      <td>NaN</td>
      <td>SWC 36TH + MARKET</td>
      <td>NaN</td>
      <td>6J0</td>
      <td>COM CONDO 9 STY MASONRY</td>
      <td>4</td>
      <td>COMMERCIAL</td>
      <td>369.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>128.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>27.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>3600</td>
      <td>NaN</td>
      <td>3600 MARKET ST</td>
      <td>SUITE 800</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>3711 MARKET ST</td>
      <td>19104</td>
      <td>255700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1119.0</td>
      <td>NaN</td>
      <td>UNIVERSITY CITY</td>
      <td>SCIENCE CENTER</td>
      <td>883076600</td>
      <td>A</td>
      <td>B+</td>
      <td>1943-01-01 00:00:00</td>
      <td>17S7 174</td>
      <td>1943-01-01 00:00:00</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>53560.0</td>
      <td>ST</td>
      <td>NaN</td>
      <td>MARKET</td>
      <td>NaN</td>
      <td>204560.0</td>
      <td>51140.0</td>
      <td>NaN</td>
      <td>33495.0</td>
      <td>2711.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B50</td>
      <td>NaN</td>
      <td>I</td>
      <td>1988.0</td>
      <td>NaN</td>
      <td>19104.0</td>
      <td>CMX4</td>
      <td>1001347387</td>
      <td>244</td>
      <td>OFFICE CONDO</td>
      <td>-75.194632</td>
      <td>39.955776</td>
      <td>3600 MARKET ST # B50</td>
      <td>3600 MARKET ST [UNIT] B50</td>
      <td>3600 MARKET ST # B50</td>
      <td>3600 MARKET ST</td>
      <td>3600 MARKET ST UNIT B50</td>
      <td>3600 MARKET ST</td>
    </tr>
    <tr>
      <th>581989</th>
      <td>249036451</td>
      <td>2021-10-19 09:02:58</td>
      <td>NaN</td>
      <td>2256'8"M/L SE MONT CO</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>220.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>143200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>21.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>8</td>
      <td>NaN</td>
      <td>8 RIVER RD</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>NaN</td>
      <td>19152</td>
      <td>143200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CITY OF PHILA DEPT OF PUB PROP WATER DEP</td>
      <td>NaN</td>
      <td>784386602</td>
      <td>A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>150N190146</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>68780.0</td>
      <td>RD</td>
      <td>NaN</td>
      <td>RIVER</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A1</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19128.0</td>
      <td>RMX1</td>
      <td>1001676987</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.258453</td>
      <td>40.049893</td>
      <td>8 RIVER RD # A1</td>
      <td>8 RIVER RD [UNIT] A1</td>
      <td>8 RIVER RD # A1</td>
      <td>8 RIVER RD</td>
      <td>8 RIVER RD UNIT A1</td>
      <td>8 RIVER RD</td>
    </tr>
  </tbody>
</table>
<p>40067 rows × 86 columns</p>
</div>




```python
data_opa.head()
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
      <th>objectid</th>
      <th>assessment_date</th>
      <th>basements</th>
      <th>beginning_point</th>
      <th>book_and_page</th>
      <th>building_code</th>
      <th>building_code_description</th>
      <th>category_code</th>
      <th>category_code_description</th>
      <th>census_tract</th>
      <th>central_air</th>
      <th>cross_reference</th>
      <th>date_exterior_condition</th>
      <th>depth</th>
      <th>exempt_building</th>
      <th>exempt_land</th>
      <th>exterior_condition</th>
      <th>fireplaces</th>
      <th>frontage</th>
      <th>fuel</th>
      <th>garage_spaces</th>
      <th>garage_type</th>
      <th>general_construction</th>
      <th>geographic_ward</th>
      <th>homestead_exemption</th>
      <th>house_extension</th>
      <th>house_number</th>
      <th>interior_condition</th>
      <th>location</th>
      <th>mailing_address_1</th>
      <th>mailing_address_2</th>
      <th>mailing_care_of</th>
      <th>mailing_city_state</th>
      <th>mailing_street</th>
      <th>mailing_zip</th>
      <th>market_value</th>
      <th>market_value_date</th>
      <th>number_of_bathrooms</th>
      <th>number_of_bedrooms</th>
      <th>number_of_rooms</th>
      <th>number_stories</th>
      <th>off_street_open</th>
      <th>other_building</th>
      <th>owner_1</th>
      <th>owner_2</th>
      <th>parcel_number</th>
      <th>parcel_shape</th>
      <th>quality_grade</th>
      <th>recording_date</th>
      <th>registry_number</th>
      <th>sale_date</th>
      <th>sale_price</th>
      <th>separate_utilities</th>
      <th>sewer</th>
      <th>site_type</th>
      <th>state_code</th>
      <th>street_code</th>
      <th>street_designation</th>
      <th>street_direction</th>
      <th>street_name</th>
      <th>suffix</th>
      <th>taxable_building</th>
      <th>taxable_land</th>
      <th>topography</th>
      <th>total_area</th>
      <th>total_livable_area</th>
      <th>type_heater</th>
      <th>unfinished</th>
      <th>unit</th>
      <th>utility</th>
      <th>view_type</th>
      <th>year_built</th>
      <th>year_built_estimate</th>
      <th>zip_code</th>
      <th>zoning</th>
      <th>pin</th>
      <th>building_code_new</th>
      <th>building_code_description_new</th>
      <th>lat</th>
      <th>lng</th>
      <th>Address_concat_opa</th>
      <th>Address_concat_opa_v1</th>
      <th>standardized_address_opa</th>
      <th>base_address_opa</th>
      <th>standardized_address_opa_v1</th>
      <th>base_address_opa_v1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>248457024</td>
      <td>2022-04-27 11:50:34</td>
      <td>NaN</td>
      <td>124'9 1/2" E GERMANTN</td>
      <td>NaN</td>
      <td>SC</td>
      <td>VACANT LAND COMMER &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>175.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>87.0</td>
      <td>0.0</td>
      <td>29000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>37.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>925</td>
      <td>NaN</td>
      <td>925 W SOMERSET ST</td>
      <td>MUNICIPAL SERVICES BLDG</td>
      <td>ROOM 1030</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>1401 JOHN F KENNEDY BLVD</td>
      <td>19107</td>
      <td>29000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1356.0</td>
      <td>NaN</td>
      <td>CITY OF PHILA</td>
      <td>NaN</td>
      <td>885458000</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>73280.0</td>
      <td>ST</td>
      <td>W</td>
      <td>SOMERSET</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>1305.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19133.0</td>
      <td>CMX2</td>
      <td>1001489682</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.146849</td>
      <td>39.994767</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
      <td>925 W SOMERSET ST</td>
    </tr>
    <tr>
      <th>1</th>
      <td>248457025</td>
      <td>2022-04-27 11:50:37</td>
      <td>NaN</td>
      <td>175' N CLIFFORD ST</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>90.0</td>
      <td>0.0</td>
      <td>79500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>14.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1755</td>
      <td>NaN</td>
      <td>1755 N 31ST ST</td>
      <td>MUNICIPAL SERVICES BLDG</td>
      <td>ROOM 1030</td>
      <td>NaN</td>
      <td>PHILADELPHIA PA</td>
      <td>1401 JOHN F KENNEDY BLVD</td>
      <td>19107</td>
      <td>79500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1650.0</td>
      <td>NaN</td>
      <td>CITY OF PHILA</td>
      <td>NaN</td>
      <td>324196601</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>NaN</td>
      <td>2070-10-05 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>88400.0</td>
      <td>ST</td>
      <td>N</td>
      <td>31ST</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>1260.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>RSA5</td>
      <td>1001648434</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.184591</td>
      <td>39.983481</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
      <td>1755 N 31ST ST</td>
    </tr>
    <tr>
      <th>2</th>
      <td>248457026</td>
      <td>2022-04-27 11:50:40</td>
      <td>NaN</td>
      <td>NWC COLUMBIA AVE</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>49.0</td>
      <td>0.0</td>
      <td>44600.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>16.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1700</td>
      <td>NaN</td>
      <td>1700 N NEWKIRK ST</td>
      <td>OF PHILADELPHIA</td>
      <td>16TH FLOOR</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>PHILADELPHIA PA</td>
      <td>1234 MARKET ST</td>
      <td>19107</td>
      <td>44600.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1259.0</td>
      <td>NaN</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>OF PHILADELPHIA</td>
      <td>324158601</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>59640.0</td>
      <td>ST</td>
      <td>N</td>
      <td>NEWKIRK</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>784.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>RSA5</td>
      <td>1001388974</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.180972</td>
      <td>39.981766</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
      <td>1700 N NEWKIRK ST</td>
    </tr>
    <tr>
      <th>3</th>
      <td>248457027</td>
      <td>2022-04-27 11:50:38</td>
      <td>NaN</td>
      <td>30'8" N COLUMBIA AVE</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>65.0</td>
      <td>0.0</td>
      <td>64500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1705</td>
      <td>NaN</td>
      <td>1705 N 29TH ST</td>
      <td>OF PHILADELPHIA</td>
      <td>16TH FLOOR</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>PHILADELPHIA PA</td>
      <td>1234 MARKET ST</td>
      <td>19107</td>
      <td>64500.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1575.0</td>
      <td>NaN</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>OF PHILADELPHIA</td>
      <td>324176801</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>88360.0</td>
      <td>ST</td>
      <td>N</td>
      <td>29TH</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>975.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>RSA5</td>
      <td>1001646785</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.181622</td>
      <td>39.981936</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
      <td>1705 N 29TH ST</td>
    </tr>
    <tr>
      <th>4</th>
      <td>248457028</td>
      <td>2022-04-27 11:50:40</td>
      <td>NaN</td>
      <td>SWC MONTGOMERY ST</td>
      <td>NaN</td>
      <td>SR</td>
      <td>VACANT LAND RESIDE &lt; ACRE</td>
      <td>6</td>
      <td>VACANT LAND</td>
      <td>149.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>68.0</td>
      <td>0.0</td>
      <td>4900.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0</td>
      <td>NaN</td>
      <td>1766</td>
      <td>NaN</td>
      <td>1766 N 28TH ST</td>
      <td>OF PHILADELPHIA</td>
      <td>16TH FLOOR</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>PHILADELPHIA PA</td>
      <td>1234 MARKET ST</td>
      <td>19107</td>
      <td>4900.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1083.0</td>
      <td>NaN</td>
      <td>REDEVELOPMENT AUTHORITY</td>
      <td>OF PHILADELPHIA</td>
      <td>324150201</td>
      <td>E</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>NaN</td>
      <td>2070-09-30 00:00:00</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>PA</td>
      <td>88340.0</td>
      <td>ST</td>
      <td>N</td>
      <td>28TH</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>F</td>
      <td>1042.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>I</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>19121.0</td>
      <td>CMX1</td>
      <td>1001645495</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-75.180171</td>
      <td>39.983045</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
      <td>1766 N 28TH ST</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

# Assignment


```python
# Q1 :-

match_by_pin = pd.merge(dor_data,data_opa,left_on='PIN',right_on='pin')
print('Percent of record match by PIN = ',round((match_by_pin.shape[0]/data_opa.shape[0])*100,2))
```

    Percent of record match by PIN =  90.35
    


```python
#Q2 Part a :-

match_by_concat = pd.merge(dor_data,data_opa,left_on='Address_Concat_dor',right_on='Address_concat_opa')
print('Percent of record match by Concatenated address = ',round(((match_by_concat.shape[0]/data_opa.shape[0])*100),2))

match_by_concat_v1 = pd.merge(dor_data,data_opa,left_on='Address_Concat_dor_v1',right_on='Address_concat_opa_v1')
print('Percent of record match by Concatenated address = ',round(((match_by_concat_v1.shape[0]/data_opa.shape[0])*100),2))
```

    Percent of record match by Concatenated address =  35.3
    Percent of record match by Concatenated address =  35.3
    


```python
#Q2 Part b :-


# match_by_std = pd.merge(dor_data,data_opa,left_on='standardized_address_dor',right_on='standardized_address_opa')
# print('Percent of record match by standarized address = ',round(((match_by_std.shape[0]/data_opa.shape[0])*100),2))



match_by_std_v1 = pd.merge(dor_data,data_opa,left_on='standardized_address_dor_v1',right_on='standardized_address_opa_v1')
print('Percent of record match by standarized address = ',round(((match_by_std_v1.shape[0]/data_opa.shape[0])*100),2))
```

    Percent of record match by standarized address =  90.39
    


```python
# Q2 part 3

# match_by_base = pd.merge(dor_data,data_opa,left_on='base_address_dor',right_on='base_address_opa')
# print('Percent of record match by base address = ',round(((match_by_base.shape[0]/data_opa.shape[0])*100),2))

match_by_base_v1 = pd.merge(dor_data,data_opa,left_on='base_address_dor_v1',right_on='base_address_opa_v1')
print('Percent of record match by base address = ',round(((match_by_base_v1.shape[0]/data_opa.shape[0])*100),2))

```

    Percent of record match by base address =  104.64
    


```python
# Q3

match_by_condos = pd.merge(dor_data,data_opa, how = 'right', left_on='PIN',right_on='pin',suffixes=('_x', '_y'))
match_by_condos = match_by_condos[pd.isna(match_by_condos['OBJECTID'])]
match_by_condos = pd.DataFrame(match_by_condos.groupby(['location'])['objectid'].count())
match_by_condos = match_by_condos[match_by_condos['objectid']>1]
print('Condos not alligned with DOR = ',match_by_condos.shape[0])
```

    Condos not alligned with DOR =  2592
    


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```
