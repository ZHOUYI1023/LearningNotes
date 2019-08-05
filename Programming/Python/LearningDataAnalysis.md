# Numpy
## Create Array
```python{} 
>>> import numpy as np
>>> a = np.arange(15).reshape(3, 5)
>>> b = np.array([6, 7, 8])
>>> c = np.array( [[1,2], [3,4]], dtype = complex )
>>> d = np.zeros( (3,4) )
>>> e = np.ones( (2,3,4), dtype = np.int16 )
>>> f = np.empty( (2,3) )
>>> g = np.eye(5) 
>>> h = np.arange( 0, 2, 0.3 ) 
>>> i = np.linspace( 0, 2*np.pi, 100 )
```
## Arithmetic Operations
```python
>>> a < 5
>>> A = np.array( [[1,1],
...             [0,1]] )
>>> B = np.array( [[2,0],
...             [3,4]] )
>>> A * B                       # elementwise product
array([[2, 0],
       [0, 4]])
>>> A @ B                       # matrix product
array([[5, 4],
       [3, 4]])
>>> A.dot(B)                    # another matrix product
array([[5, 4],
       [3, 4]])

>>> a = np.random.random((2,3))
>>> a.sum()
>>> a.min()
>>> a.max()
# In Numpy dimensions are called axes. The number of axes is rank.
>>> b = np.arange(12).reshape(3,4)
>>> b.sum(axis=0)                            # sum of each column
>>> b.min(axis=1)                            # min of each row
>>> b.cumsum(axis=1)                         # cumulative sum along each row
```
* `x[1,2,...]` is equivalent to `x[1,2,:,:,:]`,
* `x[...,3]` to `x[:,:,:,:,3]` and
* `x[4,...,5,:]` to `x[4,:,:,5,:]`.

## Shape Operation
When fewer indices are provided than the number of axes, the missing indices are considered complete slices:
```python
>>> b[-1]     # the last row. Equivalent to b[-1,:]
array([40, 41, 42, 43])
```

Iterating over multidimensional arrays is done with respect to the first axis:
```python
>>> for row in b:
...     print(row)
...
```
However, if one wants to perform an operation on each element in the array, one can use the flat attribute which is an iterator over all the elements of the array:
```python
>>> for element in b.flat:
...     print(element)
...
```
```python
>>> a.ravel()  # returns the array, flattened
>>> a.reshape(6,2)  # returns the array with a modified shape
>>> a.reshape(3,-1) # # -1 means "whatever is needed"
>>> a.T  # returns the array, transposed
```
The reshape function returns its argument with a modified shape, whereas the ndarray.resize method modifies the array itself
```python
>>> a.resize((2,6))
```

 hstack and vstack 
```python
>>> a = np.floor(10*np.random.random((2,2)))
>>> a
array([[ 8.,  8.],
       [ 0.,  0.]])
>>> b = np.floor(10*np.random.random((2,2)))
>>> b
array([[ 1.,  8.],
       [ 0.,  4.]])
>>> np.vstack((a,b))
array([[ 8.,  8.],
       [ 0.,  0.],
       [ 1.,  8.],
       [ 0.,  4.]])
>>> np.hstack((a,b))
array([[ 8.,  8.,  1.,  8.],
       [ 0.,  0.,  0.,  4.]])
```

## Copy
No Copy At All
```python
>>> a = np.arange(12)
>>> b = a # no new object is created
>>> b is a # a and b are two names for the same ndarray object
True
```
Shallow Copy (by view)
```
>>> c = a.view()
>>> c is a
False
>>> c.base is a                        # c is a view of the data owned by a
True
>>>
>>> c.shape = 2,6                      # a's shape doesn't change
>>> a.shape
(3, 4)
>>> c[0,4] = 1234                      # a's data changes
>>> a
array([[   0,    1,    2,    3],
       [1234,    5,    6,    7],
       [   8,    9,   10,   11]])
```
Slicing an array returns a view of it
```python
>>> s = a[ : , 1:3]     # spaces added for clarity; could also be written "s = a[:,1:3]"
>>> s[:] = 10           # s[:] is a view of s. Note the difference between s=10 and s[:]=10
>>> a
array([[   0,   10,   10,    3],
       [1234,   10,   10,    7],
       [   8,   10,   10,   11]])
```
Deep Copy (by copy)
```python
>>> d = a.copy() # a new array object with new data is created
>>> d is a
False
```
For example, suppose a is a huge intermediate result and the final result b only contains a small fraction of a, a deep copy should be made when constructing b with slicing:
```python
>>> a = np.arange(int(1e8))
>>> b = a[:100].copy()
>>> del a  # the memory of `a` can be released.
```


## Random Number
`rand(d0, d1, …, dn)` 	Random values in a given shape.
`randn(d0, d1, …, dn)` 	Return a sample (or samples) from the “standard normal” distribution.
`randint(low[, high, size, dtype])` 	生成在半开半闭区间[low,high)上离散均匀分布的整数值;若high=None，则取值区间变为[0,low)

# Pandas



# Sickit-Learn

