# Series

```
print(pd.Series(['banana', 42]))
```

|index | values         |
|--|---------|
|0 |   banana|
|1 |       42|

dtype: object

```
pd.Series(['Wes McKinney', 'Creator of Pandas'], index=['Person', 'Who'])
```

|index | values         |
|--|---------|
|Person |   Wes McKinney|
|Who |      Creator of Pandas|

dtype: object

```
print(series.index) or print(series.keys())

Index(['Person', 'Who'], dtype='object')
```
```
print(series.values)

['Wes McKinney' 'Creator of Pandas']
```

# Series methods

|method | description         |
|--|---------|
|append |  |
|describe  | 요약 통계량 |
|drop_duplicate  | |
|equals  | |
|isin  | |
|min/max/median/mean/std  | |
|replace  | |
|sample  | 임의의 값을 반환|
|sort_values  | |
|to_frame  | |


|index | values         |
|--|---------|
|A |  50|
|B  | 60|
|C  | 70|
|D  | 80|
|E  | 50|
|F  | 60|
|G  | 70|

```
print(df.mean(), df.max(), df.min(), df.std(), df.median())

62.857142857142854 80 50 11.126972805283735 60.0
```

```
print(df.drop_duplicates())
```

|index | values         |
|--|---------|
|A |  50|
|B  | 60|
|C  | 70|
|D  | 80|

# Series Boolean extraction

```
print(ages) / print(ages > ages.mean()) / print(ages[ages > ages.mean()])
```
|index | values |  |index | values  |   |index | values |
|--|---------|----|--|---------|---|--|---------|
|0 |  37 |   |0 |  False |   |1 |  61 |
|1 |  61|    |1 |  True|     |2 |  90| 
|2 |  90|    |2 |  True|     |3 |  66| 
|3 |  66|    |3 |  True|     |7 |  77| 
|4 |  56|    |4 |  False|    | |  |    
|5 |  45|    |5 |  False|    | |  |    
|6 |  41|    |6 |  False|    | |  |    
|7 |  77|    |7 |  True|     | |  |    

# Series Operation

```
print(ages + ages) / print(ages + 100) / print(ages + pd.Series([1,2],index=[3,4]))
```
|index | values |  |index | values  |   |index | values |
|--|---------|----|--|---------|---|--|---------|
|0 |  74 |   |0 |  137 |   |0 |  NaN |
|1 |  122|    |1 |  161|   |1 |  NaN| 
|2 |  180|    |2 |  190|   |2 |  NaN| 
|3 |  132|    |3 |  166|   |3 |  67.0| 
|4 |  112|    |4 |  156|   |4 |  58.0|    
|5 |  90|    |5 |  145|    |5 |  NaN|    
|6 |  82|    |6 |  141|    |6 |  NaN|    
|7 |  154|    |7 |  177|   |7 |  NaN|    

# DataFrame & Series

|          index        | Occupation  |   Born    |   Died     | Age |
|----|----|----|----|----|
|Rosaline Franklin |     Chemist | 1920-07-25| 1958-04-16 | 37|
|William Gosset    | Statistician| 1876-06-13| 1937-10-16 | 61|

```
print(scientists.loc['William Gosset'])
```

|index | values         |
|--|---------|
|Occupation |  Statistician|
|Born       |    1876-06-13|
|Died       |    1937-10-16|
|Age        |            61|

```
print(scientists['Age'])
```

|index | values         |
|--|---------|
|Rosaline Franklin |   37|
|William Gosset    |   61|

Name: Age, dtype: int64

