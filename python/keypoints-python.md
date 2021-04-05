[toc]



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



#### Static variables in functions/methods

```python
def myfoo(x):
    myfoo.t = x
    if myfoo.t > 1000:
        myfoo.z = x * x
    else:
        myfoo.z = -getattr(myfoo,"z", 1)
    return myfoo.t + myfoo.z


print(myfoo(1200))
print(f"myfoo::   t: {myfoo.t},  z: {myfoo.z}")
print(myfoo(10))
print(f"myfoo::   t: {myfoo.t},  z: {myfoo.z}")
print(myfoo(15))
print(f"myfoo::   t: {myfoo.t},  z: {myfoo.z}")
print(myfoo(1500))
print(f"myfoo::   t: {myfoo.t},  z: {myfoo.z}")
print(myfoo(10))
print(f"myfoo::   t: {myfoo.t},  z: {myfoo.z}")

getattr(myfoo,"z", None)
getattr(myfoo,"r","jjj")
```



