# DataFrame

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

# Extraction - Columns

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


# Extraction - iloc[rows,columns] or iloc[rows]

```
df.iloc[[0,1]] ( = df.iloc[[0,1],:] = df.iloc[range(2),:] )
df.iloc[:,range(2)]
df.iloc[[0,1],[0,1]]
``` 
|   | country | continent | year | ... |
|---|-----|-----|-----|---|
| 0 |  Afghanistan |  Asia  |  1952   |  ... |
| 1 |  Afghanistan |  Asia  |  1959   |  ... |

|   | country | continent | 
|---|-----|-----|
| 0 |  Afghanistan |  Asia  |
| 1 |  Afghanistan |  Asia  |
|...| ... | ... |

|   | country | continent | 
|---|-----|-----|
| 0 |  Afghanistan |  Asia  |
| 1 |  Afghanistan |  Asia  |


```
df.iloc[0,1]
Asia
``` 

* Last row

```
df.iloc[-1]
df.tail(n=1)
df.iloc[df.shape[0]-1]
``` 


<hr>

# Extraction - loc[rows,columns] or loc[rows]

```
df.loc[:,['country','continent','year']] ( = df.loc[:,'country':'year'])
df.loc['Scott Smith':'Daniel Hsia','color']
``` 
|   | country | continent | year |
|---|-----|-----|-----|
| 0 |  Afghanistan |  Asia  |  1952   |
| 1 |  Afghanistan |  Asia  |  1959   |
| 2 |  Afghanistan |  Asia  |  1962   |
|...| ... | ... | ... |


# Extraction - index

df[item]

If item is a string or a string list, df.loc[:,item]

Elseif item is slice df.loc[item,:]

```
movie[['color','duration']] (=movie.loc[:,['color','duration']])
movie['Adam Carolla':'Adam Green'] (=movie.loc['Adam Carolla':'Adam Green',:])
```


# Extraction Scalar indexer - .iat[row, col], .at[row, col] (scalar index only)

``` 
movie.iat[0,1]
movie.iat[1,1]
movie.iat[1,1:2](X)
movie.at['Jon Gunn','color']
``` 

<hr>

# DataFrame generation             

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


```
print(df.info())

<class 'pandas.core.frame.DataFrame'>
Index: 2 entries, X to Y
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype 
---  ------  --------------  ----- 
 0   Age     2 non-null      int64 
 1   Att     2 non-null      object
 2   Class   2 non-null      object
dtypes: int64(1), object(2)
memory usage: 64.0+ bytes
None
```



* Group by







<hr>

* DataFrame / dictionary                 

```
exam_data = {'Name' : ["CCC","DDD","EEE"],
             'Math' : [100,50,30],
             'PT' : [40,30,65],
             'Music' : [30,60,10]}
df = pd.DataFrame(exam_data)
```

|   | Name | Math | PT | Music |
|---|-----|-----|-----|---|
| 0 |  CCC |  100  |  40   |  30 |
| 1 |  DDD |  50  |   30   |  60 |
| 2 |  EEE |  30  |   65   |  10 |

<hr>





<hr>

* insert items      
  columns -> ['col']
```
df['English'] = [30,50,60]
df.loc[6] = ["FFF",30,50,60]
```

|   | Name | Math | PT | Music | English |
|---|-----|-----|-----|---|----|
| 0 |  CCC |  100  |  40   |  30 | 30 |
| 1 |  DDD |  50  |   30   |  60 | 50 |
| 2 |  EEE |  30  |   65   |  10 | 60 |

|   | Name | Math | PT | Music |
|---|-----|-----|-----|---|
| 0 |  CCC |  100  |  40   |  30 |
| 1 |  DDD |  50  |   30   |  60 |
| 2 |  EEE |  30  |   65   |  10 |
| 6 |  FFF |  30  |   50   |  60 |

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



