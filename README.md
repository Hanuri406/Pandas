# DataFrame

<hr>

* DataFrame / index / columns             

```
df = pd.DataFrame([[15,"A","B"],[12,"C","D"]],
      index=["1","2"],
      columns=["Age","Att","Class"])
```

|   | Age | Att | Class |
|---|-----|-----|-------|
| 1 |  15 |  A  |   B   |
| 2 |  12 |  C  |   D   |

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

* extract items      
  loc[rows,cols] / iloc[rows,cols]
```
print(df.loc[0,'Math'])
print(df.iloc[2,2])
print(df.iloc[1:2,'PT':'Music'])
print(df.iloc[:,'PT':'Music'])
mask = (df.Math > 50) // boolean indexing
print(df[mask])
```
100    
65

|   | PT | Music |
|---|----|---|
| 1 | 30   |  60 |
| 2 |  65   |  10 |

|   | Name | Math | PT | Music |
|---|-----|-----|-----|---|
| 0 |  CCC |  100  |  40   |  30 |

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
df.set_index(['Name','Math'],inplace=True)
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

|   | Math | PT |
|---|----|---|
| 1 |  50  | 30 |
| 0 |  100 | 40 |
| 2 |  30  | 65 |

