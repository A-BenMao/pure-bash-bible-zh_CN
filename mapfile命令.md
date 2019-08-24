
# mapfile #

bash提供了两个内置命令：readarray和mapfile，它们是同义词。它们的作用是从标准输入读取一行行的数据，然后每一行都赋值给一个数组的各元素。显然，在shell编程中更常用的是从文件、从管道读取，不过也可以从文件描述符中读取数据。


> 语法

	mapfile [OPTIONS] ARRAY
	readarray [OPTIONS] ARRAY

```
其中options:
-O INDEX  ：指定从哪个索引号开始存储数据，默认存储数据的起始索引号为0
-n count  ：最多只拷贝多少行到数组中，如果count=0，则拷贝所有行
-s count  ：忽略前count行不读取
-c NUM    ：每读取NUM行就调用一次"-C callback"选项指定的callback程序
-C callback：每读取"-c NUM"选项指定的NUM行就执行一次callback回调程序
-d string  ：指定读取数据时的行分隔符，默认是换行符
-t        ：移除尾随行分隔符，默认是换行符
-u fd      ：指定从文件描述符fd而非标准输入中读取数据
```

- 如果不指定ARRAY参数，则默认使用数组MAPFILE

- 如果不指定"-O"选项，则在存储数据之前先清空数组(如果该数组已存在)

- 给定了"-C callback"却没有给定"-c NUM"时，则默认为每5000行调用一次回调程序

- 回调程序是在读取给定行数之后，赋值到数组元素之前执行的。所以流程为："读NUM行-->callback-->赋值"

- 每次调用回调函数时，都将调用callback之前的最后一行数据及其对应的索引号作为回调程序的参数。例如-c 3 -C callback，则会将索引号2和第3行内容，索引号5和第6行内容作为callback程序的参数

- "-t"去除行尾分隔符，一般来说都是换行符。