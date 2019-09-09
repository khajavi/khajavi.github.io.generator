+++
categories = []
date = "2016-01-31T11:01:35+03:30"
description = ""
keywords = []
title = "rddsuite"
draft = true
+++

# عملیات روی آردی‌دی
# makeRDD
ساخت آردی‌دی از کالکشن‌های لوکال اسکالا

```
    val nums = sc.makeRDD(Array(1, 2, 3, 4), 2)
```


# getNumPartitions

```
scala> nums.getNumPartitions
res95: Int = 2
```


# collect

```
scala> nums.collect
res96: Array[Int] = Array(1, 2, 3, 4)
```

# toLocalIterator
یک ایتریتور برای کل عناصر آر‌دی‌دی برمی‌گرداند.


```
scala> nums.toLocalIterator
res0: Iterator[Int] = non-empty iterator
```

```
scala> nums.toLocalIterator.toList
res1: List[Int] = List(1, 2, 3, 4)
```


این قسمت را متوجه نشدم:

> Note: this results in multiple Spark jobs, and if the input RDD is the result of a wide transformation (e.g. join with different partitioners), to avoid recomputing the input RDD should be cached first.

# distinct
فرق بین `distinct(numPartitions: Int)` و `distinct` رو نفهمیدم.


```
scala>     val dups = sc.makeRDD(Array(1, 1, 2, 2, 3, 3, 4, 4), 2)
dups: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[1] at makeRDD at <console>:27

scala> dups.distinct.collect
res3: Array[Int] = Array(4, 2, 1, 3)

scala> dups.distinct(2).collect
res4: Array[Int] = Array(4, 2, 1, 3)

```



# reduce

```
scala> nums.reduce(_ + _)
res5: Int = 10
```

# fold

```
scala> val nums = sc.makeRDD(Array(1, 2, 3, 4), 1)
nums: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[16] at makeRDD at <console>:27

scala> nums.fold(2)(_+_)
res11: Int = 14
```
 را مقایسه کنید با

```
scala> val nums = sc.makeRDD(Array(1, 2, 3, 4), 2)
nums: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[17] at makeRDD at <console>:27

scala> nums.fold(2)(_+_)
res12: Int = 16
```




