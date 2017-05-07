---
layout: post
title: "python小技巧"
date: 2017-05-07 23:09:00
comments:

---
1. 带下标遍历list(enumerate function)

	```
    # -*- coding:utf-8 -*-
    l = ["xxxx", "yyyy"]
    for i, v in enumerate(l):
        print("%s 的下标是 %d" % (v, i))
	```

2. 交换两个变量的值  

	```
    a, b = 0, 1
    a, b = b, a
    print a, b
	```
3. 同时遍历两个list(zip function)

	```
    # -*- coding:utf-8 -*-
    l1 = [1, 2, 3]
    l2 = ['a', 'b', 'c']

    for i, j in zip(l1, l2):
        print i, j
	```
4. 获取字典中的值(get function)

	```
	# -*- coding:utf-8 -*-

	ages = {
	    "jack": 11,
	    "jason": 22
	 }
	
	age = ages.get("jack", "none")
	print age
	age = ages.get("mark", "none")
	print age
	```
5. list遍历中的break问题

	```
	citys = ['beijing', 'shanghai', 'tianjin']
	city = 'beijing'
	
	for c in citys:
	    if city == c:
	        print("found")
	        break
	else: #没有break发生
	    print("not found")
    ```
6. 打开文件

	```
	with open("temp.py") as f:
    for l in f:
        print l
	```
7. try cach写法

	```
	try:
	    t = int("3")
	except:
	    print("Convertion failed")
	else:
	    print("Convertion successful")
	finally:
	    print("Done")
	```