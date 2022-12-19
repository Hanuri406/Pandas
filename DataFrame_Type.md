# Missing Data 

## 1. isnull()

There is a special method to check NaN.
NaN is neither True nor False.
```
print(NaN == True)
False
print(NaN == False)
False

print(pd.isnull(NaN))
True
```

## 2. count

```
print(np.count_nonzero(df.isnull())
```

## 3. fillna

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |NaN |NaN |NaN |
|3     |4 |5 |6 |7 |

### 3-1. fillna(value)

```
print(df.fillna(0))
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |0 |0 |0 |
|3     |4 |5 |6 |7 |

### 3-2. fillna(method='ffill' or 'bfill')

```
print(df.fillna(method='ffill'))
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |3 |4 |5 |
|3     |4 |5 |6 |7 |

```
print(df.fillna(method='ffill'))
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |5 |6 |7 |
|3     |4 |5 |6 |7 |

### 3-3. interpolate()

```
print(df.interpolate())
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |4 |5 |6 |
|3     |4 |5 |6 |7 |


## 4. dropna()

```
print(df.dropna())
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|3     |4 |5 |6 |7 |

## 5. skipna option

```
print(df.sum(skipna=False))

A 10
B NaN
C NaN
D NaN
```

```
print(df.sum(skipna=True)) or print(df.sum())

A 10
B 10
C 13
D 16
```


