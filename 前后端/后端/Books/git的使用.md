# git的使用


## 1.进入clone文件夹
```angularjs
cd 文档/Books/
```

## 2.确认是clone文件夹
    其中有隐藏文件`.git`,`.`,`..`
```angularjs
ubuntu@ubuntu:~/文档/Books$ ls -a
.  ..  book_flask  book_scrapy  book_vue  .git  .idea  notebook  README.md

```
## 3.将文件内容添加到索引
```angularjs
git add .
```

## 4.对更新的文件添加注释
```angularjs
git commit -m '注释'
```

## 5.将github中的代码拉取下来对比代码的变化(尤其多人使用)
```angularjs
git pull
```

## 6.推送更新的代码到github
```angularjs
git push
```


## 7.案例
```
ubuntu@ubuntu:~$ cd 文档/Books/
ubuntu@ubuntu:~/文档/Books$ ls -a
.  ..  book_flask  book_scrapy  book_vue  .git  .idea  notebook  README.md
ubuntu@ubuntu:~/文档/Books$ git add .
ubuntu@ubuntu:~/文档/Books$ git commit -m 'day000-3'
[master 1cf46ff] day000-3
 2 files changed, 37 insertions(+), 17 deletions(-)
 create mode 100644 "notebook/git\347\232\204\344\275\277\347\224\250.md"
ubuntu@ubuntu:~/文档/Books$ git pull
已经是最新的。
ubuntu@ubuntu:~/文档/Books$ git push
Username for 'https://github.com': Lihzxxx@163.com
Password for 'https://Lihzxxx@163.com@github.com': 
对象计数中: 6, 完成.
Delta compression using up to 8 threads.
压缩对象中: 100% (5/5), 完成.
写入对象中: 100% (6/6), 688 bytes | 688.00 KiB/s, 完成.
Total 6 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To https://github.com/fighting1023/Books.git
   53a7bf0..1cf46ff  master -> master
ubuntu@ubuntu:~/文档/Books$ 

```