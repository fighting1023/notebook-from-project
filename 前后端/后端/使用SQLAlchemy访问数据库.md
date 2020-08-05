## Python的DB-API简介
数据库表是一个二维表，包含多行多列，把一个表的内容用Python的数据结构表示出来的话，可以使用一个列表list表示多行记录，list的每一个元素都是元组tuple，用来表示一行的记录，比如包含id和name的user表：

```Python
[
    ('1','user1'),
    ('2','user2'),
    ('3','user3')
]
```
python的DB-API返回的数据结构都是像上面这样表示的。

## 引入SQLAlchemy
用tuple表示一行数据很难看出表的结构 \
但是把一个tuple用class实例来表示，就可以更容易看出表的结构：
```Python
class User(object):
    def __init__(self,id,name):
        self.id = id
        self.name = name

[
    User('1','user1'),
    User('1','user1'),
    User('2','user2')
]
```
这就是ORM技术，对象关联映射，把数据库表的结构映射到对象上。ORM框架应运而生。\
在Python中最有名的ORM框架是SQLAlchemy\
安装SQLAlchemy的方法：`pip install sqlalchemy`
