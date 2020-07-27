# mysql常用语法
## 1.关联查询
```mysql
mysql> SELECT A.warehouse_name,B.product_name,B.num from warehouse_category A,warehouse B where A.id = B.warehouse_name and A.warehouse_name = '中科院';
```
此语句：查询 A的warehouse_name,B的product_name,B的num
        从 warehouse_category表(A) 和 wareohouse表(B)
        条件 A的id=B的warehouse_name and B的warehouse_name='中科院'