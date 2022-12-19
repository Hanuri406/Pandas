# Missing Data 

## isnull()

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

## Count

```
print(np.count_nonzero(df.isnull())
```

## fillna

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |NaN |NaN |NaN |
|3     |4 |5 |6 |7 |

### fillna(value)

```
print(df.fillna(0))
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |0 |0 |0 |
|3     |4 |5 |6 |7 |

### fillna(method='ffill' or 'bfill')

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

### interpolate()

```
print(df.interpolate())
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|2     |3 |4 |5 |6 |
|3     |4 |5 |6 |7 |


### dropna()

```
print(df.dropna())
```

||A  |B  |C  |D  |
|------|---|---|---|---|
|0     |1 |2 |3 |4 |
|1     |2 |3 |4 |5 |
|3     |4 |5 |6 |7 |

### skipna option

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


