# Oracle CheatSheet

## Query

- 获取前 N 行

```sql
SELECT val
FROM   rownum_order_test
ORDER BY val DESC
FETCH FIRST 5 ROWS ONLY;
```

- 获取前 N 行，如果第 N 行有多个相同值，则全部返回

```
SELECT val
FROM   rownum_order_test
ORDER BY val DESC
FETCH FIRST 5 ROWS WITH TIES;
```

- 获取前 `x%` 行：

```
SELECT val
FROM   rownum_order_test
ORDER BY val
FETCH FIRST 20 PERCENT ROWS ONLY;
```

- 根据偏移量查询，适用于需要分页的情况：

```
SELECT val
FROM   rownum_order_test
ORDER BY val
OFFSET 4 ROWS FETCH NEXT 4 ROWS ONLY;
```

- 综合使用偏移量与百分比查询：

```
SELECT val
FROM   rownum_order_test
ORDER BY val
OFFSET 4 ROWS FETCH NEXT 20 PERCENT ROWS ONLY;
```

![](https://cdn-images-1.medium.com/max/800/0*AhVo_3sCq-ft64ki.jpg)
