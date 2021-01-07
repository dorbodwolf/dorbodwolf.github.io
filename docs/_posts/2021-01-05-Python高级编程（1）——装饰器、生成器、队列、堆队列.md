# 1 装饰器Decorator


```python
import time
```


```python
# 定义now函数
def now():
    print(time.localtime().tm_hour)
```


```python
# 调用now函数
f = now
f()
```

    13
    


```python
# 读取now函数对象的变量
now.__name__
```




    'now'




```python
f.__name__
```




    'now'




```python
# 定义装饰器
def log(func):
    def wrapper(*args, **kw):
        print('call %s():' % func.__name__)
        return func(*args, **kw)
    return wrapper
```


```python
# 利用log装饰器装饰now函数
@log
def now():
    print(time.localtime().tm_hour)
```


```python
# 调用装饰器返回的同名新函数，实际上是wrapper
now()
```

    call now():
    14
    


```python
# 带参数的装饰器
def log(text):
    def decorator(func):
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```


```python
# 这段装饰代码首先调用log，返回decorator函数；然后调用decorator函数，返回wrapper函数
@log('调用')
def now():
    print('2015-3-25')
```


```python
# 调用now函数的同名函数wrapper
now()
```

    调用 now():
    2015-3-25
    


```python
# @functools.wraps(func)置于wrapper前面，
# 作用是把原始函数的__name__等属性复制到wrapper()函数中，
# 否则，有些依赖函数签名的代码执行就会出错。
import functools

def log(text):
    def decorator(func):
        @functools.wraps(func) 
        def wrapper(*args, **kw):
            print('%s %s():' % (text, func.__name__))
            return func(*args, **kw)
        return wrapper
    return decorator
```

## 1.1 作业
请设计一个decorator，它可作用于任何函数上，并打印该函数的执行时间：



```python
import time, functools

def metric(func):
    @functools.wraps(func) 
    def time_run(*args, **kw):
        t1 = time.time()
        result = func(*args, **kw)
        t2 = time.time()
        intertime = t2 - t1
        print(intertime)
        return result
    return time_run

@metric
def now():
    time.sleep(0.0012)
    print('现在是%s点' % time.localtime().tm_hour)

now()
```

    现在是14点
    0.002978801727294922
    


```python
# 更多测试
@metric
def fast(x, y):
    time.sleep(0.0012)
    return x + y;

@metric
def slow(x, y, z):
    time.sleep(0.1234)
    return x * y * z;

f = fast(11, 22)
s = slow(11, 22, 33)
if f != 33:
    print('测试失败!')
elif s != 7986:
    print('测试失败!')
```

    0.004019975662231445
    0.12505221366882324
    

# 2 生成器
使用生成器创建新的迭代模式


```python
def frange(start, stop, increment):
    x = start
    while x < stop:
        yield x
        x += increment
```


```python
for n in frange(0, 100, 2.5):
    print(n)
```

    0
    2.5
    5.0
    7.5
    10.0
    12.5
    15.0
    17.5
    20.0
    22.5
    25.0
    27.5
    30.0
    32.5
    35.0
    37.5
    40.0
    42.5
    45.0
    47.5
    50.0
    52.5
    55.0
    57.5
    60.0
    62.5
    65.0
    67.5
    70.0
    72.5
    75.0
    77.5
    80.0
    82.5
    85.0
    87.5
    90.0
    92.5
    95.0
    97.5
    

## 2.1 应用：保留最后N行

下面的search函数就是一个生成器，`yield`句返回迭代对象。

`deque`是一个队列，长度是maxlen，不停往里`append`对象，先进的先出，队列中始终是maxlen个对象


```python
from collections import deque

def search(lines, pattern, history=5):
    previous_lines = deque(maxlen=history)
    for line in lines:
        if pattern in line:
            yield line, previous_lines
        previous_lines.append(line)

# Example use on a file
if __name__ == '__main__':
    with open(r'qgis裁剪影像笔记.txt') as f:
        for line, prevlines in search(f, '工具', 5):
            for pline in prevlines:
                print(pline, end='')
            print(line, end='')
            print('-' * 20)
```

    1. 在qgis中加载矢量和待裁剪影像，
    2.使用raster——extraction——clip_raster_by_mask工具裁剪，填写需要的参数。
    --------------------
    1. 在qgis中加载矢量和待裁剪影像，
    2.使用raster——extraction——clip_raster_by_mask工具裁剪，填写需要的参数。
    /
    1）如果需要自己用脚本运行这个工具，修改好参数后粘贴clip_raster_by_mask工具下方的gdalwarp命令到cmd窗口运行即可，可以自己在cmd窗口修改参数。
    --------------------
    1. 在qgis中加载矢量和待裁剪影像，
    2.使用raster——extraction——clip_raster_by_mask工具裁剪，填写需要的参数。
    /
    1）如果需要自己用脚本运行这个工具，修改好参数后粘贴clip_raster_by_mask工具下方的gdalwarp命令到cmd窗口运行即可，可以自己在cmd窗口修改参数。
    2）文件路径和文件名需要是中文。
    3）如果裁剪提示有valid polygon或者self-intersection这样的拓扑错误，使用qgis的processing toolbox搜索fix geometries工具去修复矢量拓扑错误，使用修复后的矢量重新裁剪即可。
    --------------------
    /
    1）如果需要自己用脚本运行这个工具，修改好参数后粘贴clip_raster_by_mask工具下方的gdalwarp命令到cmd窗口运行即可，可以自己在cmd窗口修改参数。
    2）文件路径和文件名需要是中文。
    3）如果裁剪提示有valid polygon或者self-intersection这样的拓扑错误，使用qgis的processing toolbox搜索fix geometries工具去修复矢量拓扑错误，使用修复后的矢量重新裁剪即可。
    4）测试qgis版本为QGIS version 3.14.0-Pi
    5）如需在cmd运行gdalwarp.exe脚本，将脚本所在路径加入系统path，测试使用的是qgis下面的脚本（C:\Program Files\QGIS 3.14\bin），编译安装gdal后也会生成类似的脚本工具。
    --------------------
    

## 2.2 deque数据结构


```python
# deque文档
import collections
help(collections.deque)
```

    Help on class deque in module collections:
    
    class deque(builtins.object)
     |  deque([iterable[, maxlen]]) --> deque object
     |  
     |  A list-like sequence optimized for data accesses near its endpoints.
     |  
     |  Methods defined here:
     |  
     |  __add__(self, value, /)
     |      Return self+value.
     |  
     |  __bool__(self, /)
     |      self != 0
     |  
     |  __contains__(self, key, /)
     |      Return key in self.
     |  
     |  __copy__(...)
     |      Return a shallow copy of a deque.
     |  
     |  __delitem__(self, key, /)
     |      Delete self[key].
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getitem__(self, key, /)
     |      Return self[key].
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __iadd__(self, value, /)
     |      Implement self+=value.
     |  
     |  __imul__(self, value, /)
     |      Implement self*=value.
     |  
     |  __init__(self, /, *args, **kwargs)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __len__(self, /)
     |      Return len(self).
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __mul__(self, value, /)
     |      Return self*value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __reduce__(...)
     |      Return state information for pickling.
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __reversed__(...)
     |      D.__reversed__() -- return a reverse iterator over the deque
     |  
     |  __rmul__(self, value, /)
     |      Return value*self.
     |  
     |  __setitem__(self, key, value, /)
     |      Set self[key] to value.
     |  
     |  __sizeof__(...)
     |      D.__sizeof__() -- size of D in memory, in bytes
     |  
     |  append(...)
     |      Add an element to the right side of the deque.
     |  
     |  appendleft(...)
     |      Add an element to the left side of the deque.
     |  
     |  clear(...)
     |      Remove all elements from the deque.
     |  
     |  copy(...)
     |      Return a shallow copy of a deque.
     |  
     |  count(...)
     |      D.count(value) -> integer -- return number of occurrences of value
     |  
     |  extend(...)
     |      Extend the right side of the deque with elements from the iterable
     |  
     |  extendleft(...)
     |      Extend the left side of the deque with elements from the iterable
     |  
     |  index(...)
     |      D.index(value, [start, [stop]]) -> integer -- return first index of value.
     |      Raises ValueError if the value is not present.
     |  
     |  insert(...)
     |      D.insert(index, object) -- insert object before index
     |  
     |  pop(...)
     |      Remove and return the rightmost element.
     |  
     |  popleft(...)
     |      Remove and return the leftmost element.
     |  
     |  remove(...)
     |      D.remove(value) -- remove first occurrence of value.
     |  
     |  reverse(...)
     |      D.reverse() -- reverse *IN PLACE*
     |  
     |  rotate(...)
     |      Rotate the deque n steps to the right (default n=1).  If n is negative, rotates left.
     |  
     |  ----------------------------------------------------------------------
     |  Static methods defined here:
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  maxlen
     |      maximum size of a deque or None if unbounded
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  __hash__ = None
    
    


```python
# 更多deque测试

from collections import deque
queue = deque(maxlen=5)
for i in range(5):
    queue.append(i)
for i in queue:
    print(i)
```

    0
    1
    2
    3
    4
    

# 3 堆队列（优先队列）实现

查找最大或最小的N个元素


```python
import heapq
nums = [1, 8, 2, 23, 7, -4, 18, 23, 42, 37, 2]
print(heapq.nlargest(3, nums)) # Prints [42, 37, 23]
print(heapq.nsmallest(3, nums)) # Prints [-4, 1, 2]
```

    [42, 37, 23]
    [-4, 1, 2]
    

## 3.1 heapq模块简介

https://docs.python.org/zh-cn/3/library/heapq.html

https://github.com/python/cpython/blob/3.9/Lib/heapq.py

这个模块提供了堆队列算法的实现，又叫优先队列算法。

堆是一个二叉树，它的每个父节点的值都只会小于或大于所有孩子节点（的值）。它使用了数组来实现：从零开始计数，对于所有的 k ，都有 heap[k] <= heap[2*k+1] 和 heap[k] <= heap[2*k+2]。 为了便于比较，不存在的元素被认为是无限大。堆最有趣的特性在于最小的元素总是在根结点：heap[0]。

这个API与教材的堆算法实现有所不同，具体区别有两方面：（a）我们使用了从零开始的索引。这使得节点和其孩子节点索引之间的关系不太直观但更加适合，因为 Python 使用从零开始的索引。 （b）我们的 pop 方法返回最小的项而不是最大的项（这在教材中称为“最小堆”；而“最大堆”在教材中更为常见，因为它更适用于原地排序）。

基于这两方面，把堆看作原生的Python list也没什么奇怪的： heap[0] 表示最小的元素，同时 heap.sort() 维护了堆的不变性！

要创建一个堆，可以使用list来初始化为 [] ，或者你可以通过一个函数 heapify() ，来把一个list转换成堆。

## 3.2 实现一个优先级队列

！！！挖坑


```python

```
