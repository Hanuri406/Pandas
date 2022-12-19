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

```
df.iloc[2,2:] = np.NaN
```
