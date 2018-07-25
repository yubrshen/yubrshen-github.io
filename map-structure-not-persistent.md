# Map structure is not a persistent value in Python!

Given the following map structure referred by variable `x`


```python
x = map(lambda x: x*x, [x for x in range(10)])

x
```




    <map at 0x7f64441b26a0>



At the first access of `x`, it produces the expected values:



```python
print(list(x))
```

    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


But the second time the same access to the same `x`, it produces empty list!


```python
print(list(x))
```

    []


This shows that the map structure is a transient structure expressing the operations of mapping. Once the represented operations are performed, then the map structure is voided.

The moral of the story is that if the values intended to be produced by a map structure will be used multiple times, those values should be computed and stored as values away from the map structure.

The following code segment illustrates the correct practice:


```python
x = map(lambda x: x*x, [x for x in range(10)])
y = list(x)
print(y)
```

    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]



```python
print(y)
```

    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]


The computed values by the map structure `x` stored in `y` is persistent.
