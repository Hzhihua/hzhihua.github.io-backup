---
title: 二分查找法
categories: 算法(第四版)
tags: 
    - 算法(第四版)
    - 第一章
date: 2017-10-28 12:59:23
---

# 二分查找法

假设你要在电话簿中查找一个以K开头的名字（现在谁还用电话簿！），可以从头开始翻页，一直翻到以K开头的部分。但是你应该不会这样做，而是直接从中间开始查找，因为你知道以K开头的名字在电话簿中间。

现在假设你要登录Facebook。当你登录的时候，Facebook肯定会核实一下你的账号是否在Facebook上注册过。假设你的用户名为Karlmageddon，Facebook可以从以A开头的部分开始查找，但是更符合逻辑的方法是从中间找起。

这是一个查找问题，在以上所描述的所有情况下，都可以使用同一种算法来解决问题，这中算法就是*二分查找* 。

## 什么是二分查找法

在一个 *有序数组* (必须是有序数组)中查找某一个特定元素的算法。搜索过程从中间开始，如果中间元素正好是要搜索的元素，则搜索过程结束。如果中间元素大于要搜索的元素，则在小于中间元素的另一半中查找。若中间元素小于要搜索的元素，则在大于中间元素的另一半中查找。

## 图解

![二分查找图解](/images/binarySearch/Binary_search_into_array.png)

## 代码实现

```java
public class BinarySearch
{
    /**
     * 查找指定元素是否存在有序数组中
     * @param  int key 要查找的元素
     * @param  array a 有序数组
     * @return 查找成功返回指定索引的位置，失败返回 -1
     */
    public static int search(int key, int[] a)
    {
        // 数组必须是有序的
        int lo = 0;
        int hi = a.length - 1; // 获取数组的最大索引
        int mid = 0; // 中间元素索引
        while (lo <= hi)
        {
            mid = lo + (hi - lo) / 2;
            if (a[mid] == key)
              return mid;
            if (a[mid] > key)
              hi = mid - 1;
            else if (a[mid] < key)
              lo = mid + 1;
        }

        return -1;
    }
}
```

## 增长数量级分类

>  此算法属于 *对数级别(logN)* log底数为2 

## 说明

> 位于算法(第四版)28页