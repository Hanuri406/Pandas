# DataFrame

## Tips

### Check the type of the result (Series? DataFrame?)

```
print(type(df.iloc[0,1]))
<class 'str'>

print(type(df.iloc[0,1:2]))
<class 'pandas.core.series.Series'>

print(type(df.iloc[0:3,1:2]))
<class 'pandas.core.frame.DataFrame'>
```
### df[item] = df.loc[:,item] (item means column_index)

```
df.loc[:,['year']] = df[['year']] 
```

### df.loc[item] = df.loc[item,:] (item means row_index)

```
df.loc[0:3,:] = df.loc[0:3]
```

### list vs range

```
df.loc[0:3] (O) vs df.loc[[0:3]] (X)
df.loc[0,1,2] (O) vs df.loc[[0,1,2]] (X)
```

### set_index with inplace

```
scientists.set_index('Name',inplace=True)
scientists = scientists.set_index('Name')
```


## Basics

### 1. Import pandas

```
import pandas as df
df = pd.read_csv("gapminder.tsv",sep="\t")
```

### 2. Functions

```
df.head(5)
```
|index|country|continent|year|lifeExp|pop|gdpPercap|
|---|---|---|---|---|---|---|
|0|Afghanistan|Asia|1952|28\.801|8425333|779\.4453145|
|1|Afghanistan|Asia|1957|30\.332|9240934|820\.8530296|
|2|Afghanistan|Asia|1962|31\.997|10267083|853\.10071|
|3|Afghanistan|Asia|1967|34\.02|11537966|836\.1971382|
|4|Afghanistan|Asia|1972|36\.088|13079460|739\.9811058|

```
type(df) , df.shape
<class 'pandas.core.frame.DataFrame'> , (1704, 6)

df.columns
Index(['country', 'continent', 'year', 'lifeExp', 'pop', 'gdpPercap'], dtype='object')
```
```
df.dtypes
```
|  |  |
|---|---|
|country      | object|
|continent    | object|
|year         |  int64|
|lifeExp      |float64|
|pop          |  int64|
|gdpPercap    |float64|
|dtype: object|       |

```
df.info()
```

## Extraction

### 1. Column - df[col_index] or df[[col_index1,col_index2...]]

```
country_df = df['country']
print(type(country_df))
<class 'pandas.core.series.Series'>
```
```
country_df
```
|  |  |
|---|---|
|0    |  Afghanistan|
|1    |  Afghanistan|
|2    |  Afghanistan|
|3    |  Afghanistan|
|4    |  Afghanistan|
|     |     ...     |

Name: country, Length: 1704, dtype: object

```
subset = df[['country','year']]
subset.head()
```
|index|country|year|
|---|---|---|
|0|Afghanistan|1952|
|1|Afghanistan|1957|
|2|Afghanistan|1962|
|3|Afghanistan|1967|
|4|Afghanistan|1972|

### 2. Row - loc[row_index] or loc[[row_index1,row_index2]]

```
df.loc[[0,9,99]]
```

|index|country|continent|year|lifeExp|pop|gdpPercap|
|---|---|---|---|---|---|---|
|0|Afghanistan|Asia|1952|28\.801|8425333|779\.4453145|
|9|Afghanistan|Asia|1997|41\.763|22227415|635\.341351|
|99|Bangladesh|Asia|1967|43\.453|62821884|721\.1860862|

```
print(type(df.loc[0]))
<class 'pandas.core.series.Series'>

print(type(df.loc[[0,1]]))
<class 'pandas.core.frame.DataFrame'>
```

### 3. Row - iloc[row_number] or iloc[[row_number1,row_number2]]

```
df.loc[[0,9,99]]
```

|index|country|continent|year|lifeExp|pop|gdpPercap|
|---|---|---|---|---|---|---|
|0|Afghanistan|Asia|1952|28\.801|8425333|779\.4453145|
|9|Afghanistan|Asia|1997|41\.763|22227415|635\.341351|
|99|Bangladesh|Asia|1967|43\.453|62821884|721\.1860862|


### 4. Row & Column- loc[[row_indexs],[col_indexs]]

```
print(df.loc[[0,1,4],['country','year']])
```

|index|country|year|
|---|---|---|
|0|Afghanistan|1952|
|1|Afghanistan|1957|
|4|Afghanistan|1972|

### 5. Range - df[['year']] = df.loc[:,['year']] or df.loc[0:3,:] = df.loc[0:3]

```
print(df.loc[0:3,['year']])
```

|index|year|
|---|---|
|0|1952|
|1|1957|
|2|1962|
|3|1967|


### 6. Condition

```
df[df['Age'] < df['Age'].mean()]
```
|I|Name|Born|Died|Age|Occupation|
|---|---|---|---|---|---|
|0|Rosaline|Franklin|1920-07-25|1958-04-16|37|Chemist|
|4|Rachel|Carson|1907-05-27|1964-04-14|56|Biologist|
|5|John|Snow|1813-03-15|1858-06-16|45|Physician|
|6|Alan|Turing|1912-06-23|1954-06-07|41|Computer|Scientist|

```
df.loc[[False, True, True, False, True, False, True, False]]
```
|I|Name|Born|Died|Age|Occupation|
|---|---|---|---|---|---|
|1|William|Gosset|1876-06-13|1937-10-16|61|Statistician|
|2|Florence|Nightingale|1820-05-12|1910-08-13|90|Nurse|
|4|Rachel|Carson|1907-05-27|1964-04-14|56|Biologist|
|6|Alan|Turing|1912-06-23|1954-06-07|41|Computer|Scientist|

### 7. Extraction Scalar indexer - .iat[row, col], .at[row, col] (scalar index only)

``` 
movie.iat[0,1]
movie.iat[1,1]
movie.iat[1,1:2](X)
movie.at['Jon Gunn','color']
``` 


## Manipulation 

### 1. Generation

```
scientists = pd.DataFrame({ 
    'Name': ['Rosaline Franklin', 'William Gosset'], 
    'Occupation': ['Chemist', 'Statistician'], 
    'Born': ['1920-07-25', '1876-06-13'], 
    'Died': ['1958-04-16', '1937-10-16'], 
    'Age': [37, 61]}) 
```

|  | Name             |  Occupation  |     Born  |     Died   |Age  |
|---|-----|-----|-----|---|---|
|0 |Rosaline Franklin |     Chemist  | 1920-07-25| 1958-04-16 | 37 |
|1 |   William Gosset | Statistician | 1876-06-13| 1937-10-16 | 61 |

```
scientists = pd.DataFrame( 
    data={'Occupation': ['Chemist', 'Statistician'], 
          'Born': ['1920-07-25', '1876-06-13'], 
          'Died': ['1958-04-16', '1937-10-16'],
          'Age': [37, 61]},
    index=['Rosaline Franklin', 'William Gosset'],
    columns=['Occupation', 'Born', 'Age', 'Died']) 
```

| index             |  Occupation  |     Born  |     Age | Died
|-----|-----|-----|---|---|
|Rosaline Franklin |     Chemist  | 1920-07-25| 37 | 1958-04-16 |
|   William Gosset | Statistician | 1876-06-13| 61 | 1937-10-16 |


### 2. Insert columns - data sholud be prepared for all rows

```
scientists['ID'] = ['012','013']
```

|  | Name             |  Occupation  |     Born  |     Died   |Age  | ID |
|---|-----|-----|-----|---|---|---|
|0 |Rosaline Franklin |     Chemist  | 1920-07-25| 1958-04-16 | 37 | 012 |
|1 |   William Gosset | Statistician | 1876-06-13| 1937-10-16 | 61 | 013 |


### 3. Insert rows - data sholud be prepared for all columns

```
scientists.set_index('Name',inplace=True) 
scientists.loc['Kim'] = ['Mage','1920-07-22','1958-06-12',37]
```

| index             |  Occupation  |     Born  |     Age | Died
|-----|-----|-----|---|---|
|Rosaline Franklin |     Chemist  | 1920-07-25| 37 | 1958-04-16 |
|   William Gosset | Statistician | 1876-06-13| 61 | 1937-10-16 |
| Kim|     Mage  | 1920-07-22| 37 | 1958-06-12 |

```
new_sr = 
scientists.loc['Kim1'] = sr.values.tolist()
```
### 4. Concatenation

pd.concat([series_1,series_2,...])

pd.concat([dataframe_1,dataframe_2,...])

### 5. Drop columns

```
scientists = scientists.drop(['Age'],axis=1)
```

|  | Name             |  Occupation  |     Born  |     Died   |
|---|-----|-----|-----|---|
|0 |Rosaline Franklin |     Chemist  | 1920-07-25| 1958-04-16 |
|1 |   William Gosset | Statistician | 1876-06-13| 1937-10-16 |


## Statistics

### 1. groupby

```
df.groupby('year')['lifeExp','pop'].mean()
```

|year|lifeExp|pop|
|---|---|---|
|1952|49\.05761971830986|16950402\.46478873|
|1957|51\.50740112676056|18763412\.53521127|
|1962|53\.609249014084504|20421006\.85915493|
|1967|55\.67828957746479|22658298\.478873238|
|1972|57\.647386478873244|25189979\.985915493|
...


* DataFrame format

```
type(df) or type(df[['color','director_name']])
type(df['color'])

<class 'pandas.core.frame.DataFrame'>
<class 'pandas.core.series.Series'>
```
```
type(df.index) or type(df.columns)
type(df.values)

<class 'pandas.core.indexes.base.Index'>
<class 'numpy.ndarray'>
```
```
df.shape, df.size, df.ndim, len(df)
(4916, 28) 137648 2 4916
```
```
df.columns
df.columns.values

Index(['color', 'director_name', 'num_critic_for_reviews', 'duration',...])
['color', 'director_name', 'num_critic_for_reviews', 'duration',...]
```
```
print(df.dtypes)
``` 
|           |        |
|-----------|--------|
|color    |  object|
|director_name |  object|
|num_critic_for_reviews     |   float64|
|duration    | float64|
| ... |  ... |

dtype: object

<hr>

# Operations

```
print(movie.sum())
print(movie.sum(axis=1))
```

|           |        |
|-----------|--------|
|num_critic_for_reviews     |   671592.0|
|duration    | 524852.0|
| ... |  ... |

|           |        |
|-----------|--------|
|0   | 9.98e+08|
|1    | 6.09e+08|
| ... |  ... |

```
movie.nlargest(5,'movie_facebook_likes')
```

 |  | color |         director_name | ... | aspect_ratio  |movie_facebook_likes|
|--|--|--|--|--|--|
|96 | Color |     Christopher Nolan | ... |         2.35  |              349000|
|293| Color |     Quentin Tarantino | ... |         2.35  |              199000|
|10 | Color |           Zack Snyder | ... |         2.35  |              197000|
|128| Color |         George Miller | ... |         2.35  |              191000|
|178| Color | Alejandro G. Iñárritu | ... |         2.35  |              190000|


* Drop null values

```
movie['color'].dropna()
```

* Boolean extraction

```
mask = (df['Math'] > 50) // boolean indexing
print(df[mask])
```

## Filter

```
movie.filter(like='likes')
```

| |  director_facebook_likes |  movie_facebook_likes |
|---|-----|-----|
|0|                         0.0 |                 33000|
|1|                      563.0  |                     0|
|2|  ... | ... |

```
movie[movie['color'].isnull()]
```

| | color | director_facebook_likes | 
|---|-----|-----|
|4|   NaN  |          Doug Walker|
|276|    NaN |          Christopher Barnard|
|453|  NaN  |  NaN |
|...|  ... | ... |



## Etc..

### Last row

```
df.iloc[-1]
df.tail(n=1)
``` 

<hr>





<hr>

* statistics        

```
df.head(n) / df.tail(n)
df.mean() / df.median() / df.max() / df.min() / df.std() / df.corr()
df.info()                         
df.describe()                   
```

|      |       Math |       PT |    Music |
|-----|-----------|----------|---------|
| count |  3.000000  |  3.000000 |  3.000000 |
| mean  |  60.000000 | 45.000000 | 33.333333 |
| std   |  36.055513 | 18.027756 | 25.166115 |
| min   |  30.000000 | 30.000000 | 10.000000 |
| 25%   |  40.000000 | 35.000000 | 20.000000 |
| 50%   |  50.000000 | 40.000000 | 30.000000 |
| 75%   |  75.000000 | 52.500000 | 45.000000 |
| max   | 100.000000 | 65.000000 | 60.000000 |                      


<hr>

* index        

```
df.set_index(['Name','Math'],inplace=True) / df.index = ['Name','Math']
df.reindex(new_list)
df.reset_index()
df.sort_index()
df.sort_values(by='PT')
```

|   | Math | PT |
|---|----|---|
| 1 |  50  | 30 |
| 0 |  100 | 40 |
| 2 |  30  | 65 |


<hr>

* Grouping        

```
df.groupby([col])
pd.pivot_table(df, index=, columns=, values=, aggfunc=)

```


|I|Name|Born|Died|Age|Occupation|
|---|---|---|---|---|---|
|0|Rosaline|Franklin|1920-07-25|1958-04-16|37|Chemist|
|1|William|Gosset|1876-06-13|1937-10-16|61|Statistician|
|2|Florence|Nightingale|1820-05-12|1910-08-13|90|Nurse|
|3|Marie|Curie|1867-11-07|1934-07-04|66|Chemist|
|4|Rachel|Carson|1907-05-27|1964-04-14|56|Biologist|
|5|John|Snow|1813-03-15|1858-06-16|45|Physician|
|6|Alan|Turing|1912-06-23|1954-06-07|41|Computer|Scientist|
|7|Johann|Gauss|1777-04-30|1855-02-23|77|Mathematician|


