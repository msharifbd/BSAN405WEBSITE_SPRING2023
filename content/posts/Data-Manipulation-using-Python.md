---
title: 'Data Manipulation Using Python'
output: html_document
date: "2023-02-08"
---




```r
library(reticulate)
use_condaenv("anaconda3")
```

      

### Importing Necessary Packages (Libraries)


```python
# Importing Necessary Packages 
import pandas as pd # For Data Manipulation 
import numpy as np 
import matplotlib.pyplot as plt # For Data Visualization 
import seaborn as sns
```


```python
pd.__version__ # This is important because in old version some of the functions from Pandas do not work.
```

```
## '1.4.4'
```

### Importing the Dataset


```python
# Importing Dataset 
product = pd.read_csv("https://s3.us-west-2.amazonaws.com/public.gamelab.fun/dataset/Al-Bundy_raw-data.csv")
```

### Learning about the Metadata 


```python
# Metadata of the dataset 
product.shape
```

```
## (14967, 14)
```


```python
product.columns
```

```
## Index(['InvoiceNo', 'Date', 'Country', 'ProductID', 'Shop', 'Gender',
##        'Size (US)', 'Size (Europe)', 'Size (UK)', 'UnitPrice', 'Discount',
##        'Year', 'Month', 'SalePrice'],
##       dtype='object')
```


```python
product.count()[0] # counting the number of rows in the dataset
```

```
## 14967
```


```python
product.shape[1] # counting the number of columns 
```

```
## 14
```


```python
product.dtypes
```

```
## InvoiceNo          int64
## Date              object
## Country           object
## ProductID          int64
## Shop              object
## Gender            object
## Size (US)        float64
## Size (Europe)     object
## Size (UK)        float64
## UnitPrice          int64
## Discount         float64
## Year               int64
## Month              int64
## SalePrice        float64
## dtype: object
```


```python
product.head()
```

```
##    InvoiceNo      Date         Country  ...  Year Month SalePrice
## 0      52389  1/1/2014  United Kingdom  ...  2014     1     159.0
## 1      52390  1/1/2014   United States  ...  2014     1     159.2
## 2      52391  1/1/2014          Canada  ...  2014     1     119.2
## 3      52392  1/1/2014   United States  ...  2014     1     159.0
## 4      52393  1/1/2014  United Kingdom  ...  2014     1     159.0
## 
## [5 rows x 14 columns]
```


```python
product.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## RangeIndex: 14967 entries, 0 to 14966
## Data columns (total 14 columns):
##  #   Column         Non-Null Count  Dtype  
## ---  ------         --------------  -----  
##  0   InvoiceNo      14967 non-null  int64  
##  1   Date           14967 non-null  object 
##  2   Country        14967 non-null  object 
##  3   ProductID      14967 non-null  int64  
##  4   Shop           14967 non-null  object 
##  5   Gender         14967 non-null  object 
##  6   Size (US)      14967 non-null  float64
##  7   Size (Europe)  14967 non-null  object 
##  8   Size (UK)      14967 non-null  float64
##  9   UnitPrice      14967 non-null  int64  
##  10  Discount       14967 non-null  float64
##  11  Year           14967 non-null  int64  
##  12  Month          14967 non-null  int64  
##  13  SalePrice      14967 non-null  float64
## dtypes: float64(4), int64(5), object(5)
## memory usage: 1.6+ MB
```

### Cleaning the Dataset 


```python
# Changing the names of the columns to uppercase 
product.rename(columns = str.upper, inplace = True)
```


```python
product.columns
```

```
## Index(['INVOICENO', 'DATE', 'COUNTRY', 'PRODUCTID', 'SHOP', 'GENDER',
##        'SIZE (US)', 'SIZE (EUROPE)', 'SIZE (UK)', 'UNITPRICE', 'DISCOUNT',
##        'YEAR', 'MONTH', 'SALEPRICE'],
##       dtype='object')
```


```python
# Replacing whitespace in the names of the variables 
col_name = product.columns.str.replace(' ','_')
```


```python
product.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## RangeIndex: 14967 entries, 0 to 14966
## Data columns (total 14 columns):
##  #   Column         Non-Null Count  Dtype  
## ---  ------         --------------  -----  
##  0   INVOICENO      14967 non-null  int64  
##  1   DATE           14967 non-null  object 
##  2   COUNTRY        14967 non-null  object 
##  3   PRODUCTID      14967 non-null  int64  
##  4   SHOP           14967 non-null  object 
##  5   GENDER         14967 non-null  object 
##  6   SIZE (US)      14967 non-null  float64
##  7   SIZE (EUROPE)  14967 non-null  object 
##  8   SIZE (UK)      14967 non-null  float64
##  9   UNITPRICE      14967 non-null  int64  
##  10  DISCOUNT       14967 non-null  float64
##  11  YEAR           14967 non-null  int64  
##  12  MONTH          14967 non-null  int64  
##  13  SALEPRICE      14967 non-null  float64
## dtypes: float64(4), int64(5), object(5)
## memory usage: 1.6+ MB
```


```python
product.columns = col_name # Changing all column names 
```


```python
product.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## RangeIndex: 14967 entries, 0 to 14966
## Data columns (total 14 columns):
##  #   Column         Non-Null Count  Dtype  
## ---  ------         --------------  -----  
##  0   INVOICENO      14967 non-null  int64  
##  1   DATE           14967 non-null  object 
##  2   COUNTRY        14967 non-null  object 
##  3   PRODUCTID      14967 non-null  int64  
##  4   SHOP           14967 non-null  object 
##  5   GENDER         14967 non-null  object 
##  6   SIZE_(US)      14967 non-null  float64
##  7   SIZE_(EUROPE)  14967 non-null  object 
##  8   SIZE_(UK)      14967 non-null  float64
##  9   UNITPRICE      14967 non-null  int64  
##  10  DISCOUNT       14967 non-null  float64
##  11  YEAR           14967 non-null  int64  
##  12  MONTH          14967 non-null  int64  
##  13  SALEPRICE      14967 non-null  float64
## dtypes: float64(4), int64(5), object(5)
## memory usage: 1.6+ MB
```


```python
product.head()
```

```
##    INVOICENO      DATE         COUNTRY  ...  YEAR MONTH SALEPRICE
## 0      52389  1/1/2014  United Kingdom  ...  2014     1     159.0
## 1      52390  1/1/2014   United States  ...  2014     1     159.2
## 2      52391  1/1/2014          Canada  ...  2014     1     119.2
## 3      52392  1/1/2014   United States  ...  2014     1     159.0
## 4      52393  1/1/2014  United Kingdom  ...  2014     1     159.0
## 
## [5 rows x 14 columns]
```


```python
product
```

```
##        INVOICENO        DATE         COUNTRY  ...  YEAR MONTH SALEPRICE
## 0          52389    1/1/2014  United Kingdom  ...  2014     1     159.0
## 1          52390    1/1/2014   United States  ...  2014     1     159.2
## 2          52391    1/1/2014          Canada  ...  2014     1     119.2
## 3          52392    1/1/2014   United States  ...  2014     1     159.0
## 4          52393    1/1/2014  United Kingdom  ...  2014     1     159.0
## ...          ...         ...             ...  ...   ...   ...       ...
## 14962      65773  12/31/2016  United Kingdom  ...  2016    12     139.0
## 14963      65774  12/31/2016   United States  ...  2016    12     149.0
## 14964      65775  12/31/2016          Canada  ...  2016    12     125.3
## 14965      65776  12/31/2016         Germany  ...  2016    12     199.0
## 14966      65777  12/31/2016         Germany  ...  2016    12     125.1
## 
## [14967 rows x 14 columns]
```

### Changing the Types of the Variables 


```python
product['DATE'] = pd.to_datetime(product['DATE']) # Changing the DATE variable from object to date 
```


```python
product.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## RangeIndex: 14967 entries, 0 to 14966
## Data columns (total 14 columns):
##  #   Column         Non-Null Count  Dtype         
## ---  ------         --------------  -----         
##  0   INVOICENO      14967 non-null  int64         
##  1   DATE           14967 non-null  datetime64[ns]
##  2   COUNTRY        14967 non-null  object        
##  3   PRODUCTID      14967 non-null  int64         
##  4   SHOP           14967 non-null  object        
##  5   GENDER         14967 non-null  object        
##  6   SIZE_(US)      14967 non-null  float64       
##  7   SIZE_(EUROPE)  14967 non-null  object        
##  8   SIZE_(UK)      14967 non-null  float64       
##  9   UNITPRICE      14967 non-null  int64         
##  10  DISCOUNT       14967 non-null  float64       
##  11  YEAR           14967 non-null  int64         
##  12  MONTH          14967 non-null  int64         
##  13  SALEPRICE      14967 non-null  float64       
## dtypes: datetime64[ns](1), float64(4), int64(5), object(4)
## memory usage: 1.6+ MB
```


```python
product.head()
```

```
##    INVOICENO       DATE         COUNTRY  ...  YEAR MONTH SALEPRICE
## 0      52389 2014-01-01  United Kingdom  ...  2014     1     159.0
## 1      52390 2014-01-01   United States  ...  2014     1     159.2
## 2      52391 2014-01-01          Canada  ...  2014     1     119.2
## 3      52392 2014-01-01   United States  ...  2014     1     159.0
## 4      52393 2014-01-01  United Kingdom  ...  2014     1     159.0
## 
## [5 rows x 14 columns]
```


```python
product.INVOICENO = product.INVOICENO.astype(str) # converting integer to object
```


```python
product[['MONTH', 'PRODUCTID']] = product[['MONTH', 'PRODUCTID']].astype(str) # converting integer to object
```


```python
product.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## RangeIndex: 14967 entries, 0 to 14966
## Data columns (total 14 columns):
##  #   Column         Non-Null Count  Dtype         
## ---  ------         --------------  -----         
##  0   INVOICENO      14967 non-null  object        
##  1   DATE           14967 non-null  datetime64[ns]
##  2   COUNTRY        14967 non-null  object        
##  3   PRODUCTID      14967 non-null  object        
##  4   SHOP           14967 non-null  object        
##  5   GENDER         14967 non-null  object        
##  6   SIZE_(US)      14967 non-null  float64       
##  7   SIZE_(EUROPE)  14967 non-null  object        
##  8   SIZE_(UK)      14967 non-null  float64       
##  9   UNITPRICE      14967 non-null  int64         
##  10  DISCOUNT       14967 non-null  float64       
##  11  YEAR           14967 non-null  int64         
##  12  MONTH          14967 non-null  object        
##  13  SALEPRICE      14967 non-null  float64       
## dtypes: datetime64[ns](1), float64(4), int64(2), object(7)
## memory usage: 1.6+ MB
```

### SELECT ()  Function


```python
prod2 = product[['YEAR','SALEPRICE', 'DISCOUNT', 'UNITPRICE']]
```


```python
prod2.head()
```

```
##    YEAR  SALEPRICE  DISCOUNT  UNITPRICE
## 0  2014      159.0       0.0        159
## 1  2014      159.2       0.2        199
## 2  2014      119.2       0.2        149
## 3  2014      159.0       0.0        159
## 4  2014      159.0       0.0        159
```


```python
prod3 = product[['YEAR','SALEPRICE', 'DISCOUNT', 'UNITPRICE','INVOICENO']].copy()
```


```python
prod3.head()
```

```
##    YEAR  SALEPRICE  DISCOUNT  UNITPRICE INVOICENO
## 0  2014      159.0       0.0        159     52389
## 1  2014      159.2       0.2        199     52390
## 2  2014      119.2       0.2        149     52391
## 3  2014      159.0       0.0        159     52392
## 4  2014      159.0       0.0        159     52393
```


```python
prod4 = product.filter(['YEAR','SALEPRICE', 'DISCOUNT', 'UNITPRICE','INVOICENO', 'GENDER'], axis = 1)
```


```python
prod4.head()
```

```
##    YEAR  SALEPRICE  DISCOUNT  UNITPRICE INVOICENO  GENDER
## 0  2014      159.0       0.0        159     52389    Male
## 1  2014      159.2       0.2        199     52390    Male
## 2  2014      119.2       0.2        149     52391    Male
## 3  2014      159.0       0.0        159     52392  Female
## 4  2014      159.0       0.0        159     52393  Female
```


```python
# Dropping columns 
product.drop(['SIZE_(EUROPE)', 'SIZE_(UK)'], axis = 1, inplace = True)
```


```python
product.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## RangeIndex: 14967 entries, 0 to 14966
## Data columns (total 12 columns):
##  #   Column     Non-Null Count  Dtype         
## ---  ------     --------------  -----         
##  0   INVOICENO  14967 non-null  object        
##  1   DATE       14967 non-null  datetime64[ns]
##  2   COUNTRY    14967 non-null  object        
##  3   PRODUCTID  14967 non-null  object        
##  4   SHOP       14967 non-null  object        
##  5   GENDER     14967 non-null  object        
##  6   SIZE_(US)  14967 non-null  float64       
##  7   UNITPRICE  14967 non-null  int64         
##  8   DISCOUNT   14967 non-null  float64       
##  9   YEAR       14967 non-null  int64         
##  10  MONTH      14967 non-null  object        
##  11  SALEPRICE  14967 non-null  float64       
## dtypes: datetime64[ns](1), float64(3), int64(2), object(6)
## memory usage: 1.4+ MB
```

### COUNT () Function


```python
product.COUNTRY.value_counts() # Sorting in Descending Order 
```

```
## United States     5886
## Germany           4392
## Canada            2952
## United Kingdom    1737
## Name: COUNTRY, dtype: int64
```


```python
product.YEAR.value_counts().sort_values() # Sorting in Ascending Order 
```

```
## 2014    2753
## 2015    4848
## 2016    7366
## Name: YEAR, dtype: int64
```

### FILTER () Function 


```python
US = product.loc[product['COUNTRY'] == 'United States'] # Using loc function 
```


```python
US.head()
```

```
##    INVOICENO       DATE        COUNTRY  ...  YEAR MONTH SALEPRICE
## 1      52390 2014-01-01  United States  ...  2014     1     159.2
## 3      52392 2014-01-01  United States  ...  2014     1     159.0
## 5      52394 2014-01-01  United States  ...  2014     1     159.0
## 8      52397 2014-01-02  United States  ...  2014     1     139.0
## 10     52399 2014-01-02  United States  ...  2014     1     129.0
## 
## [5 rows x 12 columns]
```


```python
US2 = product[product['COUNTRY'] == 'United States'] # Alternative way to filter 
```


```python
US2.head()
```

```
##    INVOICENO       DATE        COUNTRY  ...  YEAR MONTH SALEPRICE
## 1      52390 2014-01-01  United States  ...  2014     1     159.2
## 3      52392 2014-01-01  United States  ...  2014     1     159.0
## 5      52394 2014-01-01  United States  ...  2014     1     159.0
## 8      52397 2014-01-02  United States  ...  2014     1     139.0
## 10     52399 2014-01-02  United States  ...  2014     1     129.0
## 
## [5 rows x 12 columns]
```


```python
US_GERMANY = product.query("COUNTRY == ['Germany', 'United States']") # Using query function 
```


```python
US_GERMANY.head()
```

```
##   INVOICENO       DATE        COUNTRY  ...  YEAR MONTH SALEPRICE
## 1     52390 2014-01-01  United States  ...  2014     1     159.2
## 3     52392 2014-01-01  United States  ...  2014     1     159.0
## 5     52394 2014-01-01  United States  ...  2014     1     159.0
## 6     52395 2014-01-02        Germany  ...  2014     1     179.0
## 8     52397 2014-01-02  United States  ...  2014     1     139.0
## 
## [5 rows x 12 columns]
```


```python
Male = product[product['GENDER']=="Male"]
```


```python
Male.head()
```

```
##   INVOICENO       DATE         COUNTRY  ...  YEAR MONTH SALEPRICE
## 0     52389 2014-01-01  United Kingdom  ...  2014     1     159.0
## 1     52390 2014-01-01   United States  ...  2014     1     159.2
## 2     52391 2014-01-01          Canada  ...  2014     1     119.2
## 5     52394 2014-01-01   United States  ...  2014     1     159.0
## 7     52396 2014-01-02          Canada  ...  2014     1     169.0
## 
## [5 rows x 12 columns]
```

### MUTATE () Function 


```python
Male.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## Int64Index: 8919 entries, 0 to 14964
## Data columns (total 12 columns):
##  #   Column     Non-Null Count  Dtype         
## ---  ------     --------------  -----         
##  0   INVOICENO  8919 non-null   object        
##  1   DATE       8919 non-null   datetime64[ns]
##  2   COUNTRY    8919 non-null   object        
##  3   PRODUCTID  8919 non-null   object        
##  4   SHOP       8919 non-null   object        
##  5   GENDER     8919 non-null   object        
##  6   SIZE_(US)  8919 non-null   float64       
##  7   UNITPRICE  8919 non-null   int64         
##  8   DISCOUNT   8919 non-null   float64       
##  9   YEAR       8919 non-null   int64         
##  10  MONTH      8919 non-null   object        
##  11  SALEPRICE  8919 non-null   float64       
## dtypes: datetime64[ns](1), float64(3), int64(2), object(6)
## memory usage: 905.8+ KB
```


```python
dayofweek = Male['DATE'].dt.day_name()
```


```python
Male = Male.assign(DAYOFWEEK = dayofweek) # We use assign function 
```


```python
Male.head()
```

```
##   INVOICENO       DATE         COUNTRY  ... MONTH SALEPRICE  DAYOFWEEK
## 0     52389 2014-01-01  United Kingdom  ...     1     159.0  Wednesday
## 1     52390 2014-01-01   United States  ...     1     159.2  Wednesday
## 2     52391 2014-01-01          Canada  ...     1     119.2  Wednesday
## 5     52394 2014-01-01   United States  ...     1     159.0  Wednesday
## 7     52396 2014-01-02          Canada  ...     1     169.0   Thursday
## 
## [5 rows x 13 columns]
```


```python
Male.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## Int64Index: 8919 entries, 0 to 14964
## Data columns (total 13 columns):
##  #   Column     Non-Null Count  Dtype         
## ---  ------     --------------  -----         
##  0   INVOICENO  8919 non-null   object        
##  1   DATE       8919 non-null   datetime64[ns]
##  2   COUNTRY    8919 non-null   object        
##  3   PRODUCTID  8919 non-null   object        
##  4   SHOP       8919 non-null   object        
##  5   GENDER     8919 non-null   object        
##  6   SIZE_(US)  8919 non-null   float64       
##  7   UNITPRICE  8919 non-null   int64         
##  8   DISCOUNT   8919 non-null   float64       
##  9   YEAR       8919 non-null   int64         
##  10  MONTH      8919 non-null   object        
##  11  SALEPRICE  8919 non-null   float64       
##  12  DAYOFWEEK  8919 non-null   object        
## dtypes: datetime64[ns](1), float64(3), int64(2), object(7)
## memory usage: 975.5+ KB
```


```python
Male.DAYOFWEEK.value_counts()
```

```
## Wednesday    1307
## Monday       1289
## Sunday       1282
## Tuesday      1270
## Thursday     1267
## Friday       1263
## Saturday     1241
## Name: DAYOFWEEK, dtype: int64
```


```python
product['ACTUALPRICE'] = product['SALEPRICE']*1-product['DISCOUNT']
```


```python
product.info()
```

```
## <class 'pandas.core.frame.DataFrame'>
## RangeIndex: 14967 entries, 0 to 14966
## Data columns (total 13 columns):
##  #   Column       Non-Null Count  Dtype         
## ---  ------       --------------  -----         
##  0   INVOICENO    14967 non-null  object        
##  1   DATE         14967 non-null  datetime64[ns]
##  2   COUNTRY      14967 non-null  object        
##  3   PRODUCTID    14967 non-null  object        
##  4   SHOP         14967 non-null  object        
##  5   GENDER       14967 non-null  object        
##  6   SIZE_(US)    14967 non-null  float64       
##  7   UNITPRICE    14967 non-null  int64         
##  8   DISCOUNT     14967 non-null  float64       
##  9   YEAR         14967 non-null  int64         
##  10  MONTH        14967 non-null  object        
##  11  SALEPRICE    14967 non-null  float64       
##  12  ACTUALPRICE  14967 non-null  float64       
## dtypes: datetime64[ns](1), float64(4), int64(2), object(6)
## memory usage: 1.5+ MB
```

### GROUP BY & SUMMARIZE () Functions 


```python
product.groupby('COUNTRY') ['SALEPRICE'].mean() # Split - Appy - Combine Techniques
```

```
## COUNTRY
## Canada            144.228963
## Germany           143.574658
## United Kingdom    145.505872
## United States     143.727421
## Name: SALEPRICE, dtype: float64
```


```python
product[["COUNTRY", 'SALEPRICE']].groupby('COUNTRY').mean() # Alternative way
```

```
##                  SALEPRICE
## COUNTRY                   
## Canada          144.228963
## Germany         143.574658
## United Kingdom  145.505872
## United States   143.727421
```


```python
product.groupby('COUNTRY') ['SALEPRICE'].mean().sort_values(ascending = True)
```

```
## COUNTRY
## Germany           143.574658
## United States     143.727421
## Canada            144.228963
## United Kingdom    145.505872
## Name: SALEPRICE, dtype: float64
```


```python
product.groupby('COUNTRY') ['SALEPRICE'].mean().sort_values()
```

```
## COUNTRY
## Germany           143.574658
## United States     143.727421
## Canada            144.228963
## United Kingdom    145.505872
## Name: SALEPRICE, dtype: float64
```


```python
product.groupby('COUNTRY') ['SALEPRICE'].mean().sort_values(ascending = False)
```

```
## COUNTRY
## United Kingdom    145.505872
## Canada            144.228963
## United States     143.727421
## Germany           143.574658
## Name: SALEPRICE, dtype: float64
```

### RESHAPING Dataset 


```python
pd.__version__
```

```
## '1.4.4'
```


```python
product[['PRODUCTID','GENDER']].value_counts()
```

```
## PRODUCTID  GENDER
## 2192       Male      135
## 2190       Male      132
## 2206       Male      123
## 2183       Male      123
## 2226       Male      123
##                     ... 
## 2166       Female     39
## 2176       Female     39
## 2235       Female     36
## 2162       Female     33
## 2164       Female     33
## Length: 192, dtype: int64
```


```python
reshape = product[['PRODUCTID','GENDER']].value_counts().reset_index(name = 'COUNTS').pivot(index = 'PRODUCTID', columns = 'GENDER', values = "COUNTS")
```


```python
reshape
```

```
## GENDER     Female  Male
## PRODUCTID              
## 2147           66    99
## 2148           63    84
## 2149           72    90
## 2150           63    87
## 2151           60    96
## ...           ...   ...
## 2238           75    96
## 2239          102    87
## 2240           45    96
## 2241           69   102
## 2242           66    78
## 
## [96 rows x 2 columns]
```


```python
reshape['TOTALSALES'] = reshape['Female'] + reshape ['Male']
```


```python
reshape.sort_values('TOTALSALES', ascending = False)
```

```
## GENDER     Female  Male  TOTALSALES
## PRODUCTID                          
## 2190           75   132         207
## 2213           90   114         204
## 2226           81   123         204
## 2192           66   135         201
## 2158           78   120         198
## ...           ...   ...         ...
## 2155           42    78         120
## 2194           51    66         117
## 2229           48    66         114
## 2162           33    72         105
## 2164           33    66          99
## 
## [96 rows x 3 columns]
```













