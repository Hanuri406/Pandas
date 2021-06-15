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

* loc[rows,cols] / iloc[rows,cols]
```
print(df.loc[0,'Math'])
print(df.iloc[2,2])
print(df.iloc[1:2,'PT':'Music'])
```
100    
65

|   | PT | Music |
|---|----|---|
| 1 | 30   |  60 |
| 2 |  65   |  10 |

<hr>

* []         

```
df = pd.DataFrame(exam_data)
df.set_index('Name',inplace=True)
??print(df[['Math','PT'],['CCC','DDD']])
```

|   | Math | PT |
|---|----|---|
| Name  |  |  |
| CCC | 100  | 40 |
| DDD | 50  |  30 |



