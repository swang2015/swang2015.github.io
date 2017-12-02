---
layout: post
title:  "Spark Core Programming"
date:   2014-06-22 10:30:00 -0500
categories: big-data
tags: spark
---

Spark is a lightning-fast cluster computing technology. Its in-memory cluster computing feature increases the processing speed of an application. _Resilient Distributed Datasets (RDD)_ is a fundamental data structure of Spark, which can be created in two ways: by referencing datasets in external storage and by applying _transformations_. _Actions_ is performed when we want to work with the actual dataset. Remember that RDD is lazy, so nothing will be executed until a transformation or action is triggered.


### RDD Transformations


| Transformation | Description |
| --- | --- |
| `map` | Create new data from function. |
| `filter` | Filter by creteria. |
| `flatMap` | Function returns a sequence instead of a value.  |
| `sample` | Sample data. |
| `union` | Union of two datasets. |
| `intersection` | Intersection of two datasets. |
| `distinct` | Distinct elements. |
| `groupByKey` | Group on a dataset of (K, V) pairs. |
| `reduceByKey` | Reduce on a dataset of (K, V) pairs. |
| `sortByKey` | Sort on a dataset of (K, V) pairs. |
| `join` | Join two datasets based on a related column. |


### RDD Actions


| Action | Description |
| --- | --- |
| `reduce` | Aggregation. |
| `collect` | Return as array. |
| `count` | Number of elements. |
| `countByKey` | Count of each key. |
| `take` | First n elements. |
| `saveAsTextFile` | Write to text file. |



