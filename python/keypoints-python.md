

### Variables

#### Lexical Scoping



```python
## Lexical Scoping in Python

# isGreaterThanRef(x) is based on the variable name 'cur' thanks to
# Python's LEXICAL SCOPING so changing the value of 'cur' will
# be taken into account in the lambda

isGreaterThanRef = lambda x: x > cur

cur = 12
print(list(map(isGreaterThanRef, [12,13,11,10,14])))
cur = 1
print(list(map(isGreaterThanRef, [12,13,11,10,14])))
#> [False, True, False, False, True]
#> [True, True, True, True, True]
```

