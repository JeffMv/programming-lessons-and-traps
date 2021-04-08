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



#### Scopes

```python
def bar():
    ab = 12
    def baz():
        nonlocal ab
        previous = ab
        ab = -222
        return ab, previous
    print(ab)
    print(baz())
    print(ab)

bar()
#> 12
#> (-222, 12)
#> -222
```





#### Static variables in functions/methods

There are no proper static variables for functions and methods in Python. But the feature can be partially emulated, so see the warnings and notes.

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

**NOTE**: unlike *docstrings*, these "static" members are only available AFTER the function has been called since this is just a basic expression.
Hence:

```python
def myfoo(x):
    # ...

getattr(myfoo, "t")  # raises an exception, because 'myfoo.t = x' has not been executed
```

Also note that these variables can be modified outside of the function/method, so be wary of it. Example:

```python
def myfoo(x):
    # ...

myfoo("test")
print(getattr(myfoo, "t"))  # prints "test"
myfoo.t = "hello"
print(getattr(myfoo, "t"))  # prints "hello"
```

*The case of objects and classes*

```python
## When dealing with objects, classes and methods, you have to discern several different things

class Foo():
    def bar(self):
        # ...

afoo = Foo()

# these are not the same
Foo.bar.baz  #< ...
afoo.bar.baz  #< ...
```
