# 对搜索算法的分析
## 二分搜索
阅读Python的bisection模块，并使用它！

一个基本的思路:
最小值为0，最大值为数组长度！
找出中间值
判断搜索的数与中间值的大小关系。
并且明确最后返回的是low的值即可。
循环体类似这样： while low < high
如果存在多个这样的值，
这里分为两种情况：
1. 如果需要找到最右的那个值的位置， 判断条件是什么样子
2. 如果需要找到最左边的那个值的位置，判断条件是什么样子
其实就是判断条件是x<a[mid]还是x>a[mid]的问题。
也就是等于在哪个方向的问题。


对于最后low到底到哪里的问题，不妨思考一下条件的边界。
比如现在low处在连续值的最后一个位置，high的值为这个位置加1.
mid的值是这个位置。很显然，x<a[mid]不成立，low的值就变为了high.
此时循环条件不成立，low的值在哪里一目了然了吧。

其中，mid的收敛过程是很快的。毕竟二分。

还有一个问题：
这样查找，查找左边的最小值的位置，是low的值.
如果要查找最右的值的位置，应该是low的值减1.

思考这样一个例子即可：  0 2 2 2
最后一次，中间值一定是在边界位置。
要查找2的左边最小值的位置，右边最小值的位置

```python
"""Bisection algorithms."""

def insort_right(a, x, lo=0, hi=None):
    """Insert item x in list a, and keep it sorted assuming a is sorted.

    If x is already in a, insert it to the right of the rightmost x.

    Optional args lo (default 0) and hi (default len(a)) bound the
    slice of a to be searched.
    """

    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        if x < a[mid]: hi = mid
        else: lo = mid+1
    a.insert(lo, x)



def bisect_right(a, x, lo=0, hi=None):
    """Return the index where to insert item x in list a, assuming a is sorted.

    The return value i is such that all e in a[:i] have e <= x, and all e in
    a[i:] have e > x.  So if x already appears in the list, a.insert(x) will
    insert just after the rightmost x already there.

    Optional args lo (default 0) and hi (default len(a)) bound the
    slice of a to be searched.
    """

    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        if x < a[mid]: hi = mid
        else: lo = mid+1
    return lo

def insort_left(a, x, lo=0, hi=None):
    """Insert item x in list a, and keep it sorted assuming a is sorted.

    If x is already in a, insert it to the left of the leftmost x.

    Optional args lo (default 0) and hi (default len(a)) bound the
    slice of a to be searched.
    """

    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        if x > a[mid]: lo = mid+1
        else: hi = mid
    a.insert(lo, x)


def bisect_left(a, x, lo=0, hi=None):
    """Return the index where to insert item x in list a, assuming a is sorted.

    The return value i is such that all e in a[:i] have e < x, and all e in
    a[i:] have e >= x.  So if x already appears in the list, a.insert(x) will
    insert just before the leftmost x already there.

    Optional args lo (default 0) and hi (default len(a)) bound the
    slice of a to be searched.
    """

    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo+hi)//2
        if x > a[mid]: lo = mid+1
        else: hi = mid
    return lo


```
