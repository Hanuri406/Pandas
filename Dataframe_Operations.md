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
newbie = pd.Series(['CS','1966-06-23','1946-02-01',20])
scientists.loc['Newbie'] = newbie.values.tolist()
```

## 4. Concatenation

### df1 
|A  |B  |C  |D  |
|---|---|---|---|
|a0 |b0 |c0 |d0 |
|a1 |b1 |c1 |d1 |

### df2 
|A  |B  |C  |D  |
|---|---|---|---|
|a2 |b2 |c2 |d2 |
|a3 |b3 |c3 |d3 |

## Dataframe + Dataframe
```
df = pd.concat([df1,df2])
```

### df
|A  |B  |C  |D  |
|---|---|---|---|
|a0 |b0 |c0 |d0 |
|a1 |b1 |c1 |d1 |
|a2 |b2 |c2 |d2 |
|a3 |b3 |c3 |d3 |

## Dataframe + Series

```
new_row_series = pd.Series(['n1', 'n2', 'n3', 'n4'])
df = pd.concat([df,new_row_series])
```

|FIELD1|A  |B  |C  |D  |0  |
|------|---|---|---|---|---|
|0     |a0 |b0 |c0 |d0 |NaN|
|1     |a1 |b1 |c1 |d1 |NaN|
|2     |a2 |b2 |c2 |d2 |NaN|
|3     |a3 |b3 |c3 |d3 |NaN|
|0     |NaN|NaN|NaN|NaN|n1 |
|1     |NaN|NaN|NaN|NaN|n2 |
|2     |NaN|NaN|NaN|NaN|n3 |
|3     |NaN|NaN|NaN|NaN|n4 |


pd.concat([dataframe_1,dataframe_2,...])

### 5. Drop columns

```
scientists = scientists.drop(['Age'],axis=1)
```

|  | Name             |  Occupation  |     Born  |     Died   |
|---|-----|-----|-----|---|
|0 |Rosaline Franklin |     Chemist  | 1920-07-25| 1958-04-16 |
|1 |   William Gosset | Statistician | 1876-06-13| 1937-10-16 |

