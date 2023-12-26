---
layout:       post
title:        "Mysql优化"
author:       "zxg"
header-style: text
catalog:      true
tags:
    - MySQL
---

## Mysql优化

- 避免在where字段中判断null
  
  在 MySQL 中，避免在 WHERE 子句中直接对字段进行 NULL 判断是因为它可能会导致索引无法有效使用，从而影响查询性能。
  
  当在 WHERE 子句中对字段进行 NULL 判断时，MySQL 无法有效地使用索引来加速查询。这是因为对于包含 NULL 值的列，索引存储的方式不同于普通的索引。MySQL 使用了一种称为“空间占用位图”的技术来处理 NULL 值。空间占用位图是一个额外的数据结构，用于标记每个索引项是否包含 NULL 值。当查询中包含对 NULL 值的判断时，MySQL 必须扫描空间占用位图，这会引入额外的开销，降低查询性能。
  
  为了避免在 WHERE 子句中对字段进行 NULL 判断，可以考虑使用其他方法来处理 NULL 值。以下是一些常用的替代方案：
  
  1. 使用 IS NULL 或 IS NOT NULL：代替直接使用等于（=）或不等于（<>）操作符进行 NULL 判断，可以使用 IS NULL 或 IS NOT NULL 来判断字段是否为 NULL。这种方式可以更有效地使用索引。
  
  2. 使用默认值或约束：在设计数据库表时，可以为字段设置默认值或非空约束，这样可以避免在查询时处理 NULL 值的情况。
  
  3. 使用特殊值代替 NULL：有时可以使用特殊的非 NULL 值来代替实际的 NULL 值。例如，可以使用空字符串代替 NULL 值，然后在查询时根据需要处理空字符串。

- 
