---
layout: post
title:  "Data Structure"
date:   2023-05-08
categories: python
---
I don't know well. Data Structure course logic can be uploaded here.

I can write python code here like below

__Bubble Sort__

```python
def bubble_sort(a):
  for last in range(len(a),1,-1):
    flipped=False
    for j in range(last-1):
      if a[j]>a[j+1]:
        flipped=True
        t=a[j]
        a[j]=a[j+1]
        a[j+1]=t
    if not flipped:
      return a
```

__Merge Sort__
```python
#Merge sort can't be implemented as an in-place algorithm
def merge(a, b):
  i = 0
  j = 0
  res = []
  while i < len(a) and j < len(b):
    va = a[i]
    vb = b[j]
    if va <= vb:
      res.append(va)
      i += 1
    else:
      res.append(vb)
      j += 1
  # now just copy remaining elements
  # (only one of these can be non-empty)
  res.extend(a[i:]) #둘중에 하나는 res에 다 들어감
  res.extend(b[j:])
  return res
"""
a:[1,5,7,9,10]
   i
b:[2,4,8,11]
   j
   
   i,j 하나씩 비교해서 넣은 다음 
   더 작은 걸 옆으로 한칸 옮김김
"""
def merge_sort(a):
  if len(a) <= 1:
    return a
  mid = len(a) // 2
  left_half = merge_sort(a[:mid])
  right_half = merge_sort(a[mid:])
  return merge(left_half, right_half)
```

__Quick Sort__
```python
#This is in-place algorithm
# partition range a[lo:hi+1] and return index of pivot
def partition(a, lo, hi):
  p = (lo + hi)//2
  pivot = a[p]
  a[p] = a[hi]  # Swap pivot with last item
  a[hi] = pivot

  i = lo - 1
  j = hi
  while i < j: 
    i += 1 
    while a[i] < pivot: 
      i += 1
    j -= 1
    while a[j] > pivot and j > lo: 
      j -= 1
    if i < j:
      t = a[i]; a[i] = a[j]; a[j] = t  # swap a[i] and a[j]
  a[hi] = a[i]
  a[i] = pivot # Put pivot where it belongs
  return i     # index of pivot

# sort range a[lo:hi+1]
def quick_sort(a, lo, hi):
  if (lo < hi):
    pivot = partition(a, lo, hi)
    quick_sort(a, lo, pivot - 1)
    quick_sort(a, pivot  + 1, hi)
```

Check out the Drive file, [sorting lecture].

[sorting lecture]: https://colab.research.google.com/drive/1ksQt1prRzU8mgKv34P0KxcbzibDPQHGs?usp=sharing 