
# declare #

declare为shell指令，在第一种语法中可用来声明变量并设置变量的属性([rix]即为变量的属性），在第二种语法中可用来显示shell函数。若不加上任何参数，则会显示全部的shell变量与函数。


> 语法

	declare [+/-][rxi][变量名称＝设置值] 或 declare -f/-F


> 参数说明

- +/-　”-“可用来指定变量的属性，”+”则是取消变量所设的属性；

- -f  列出之前由用户在脚本中定义的函数名称和函数体；

- -r [name[=value]] 或 readonly name：将变量定义为只读（不可修改和删除）；

- -x name[=value] 或 export name[=value]：将变量设置为环境变量，可供shell以外的程序来使用；

- -i 将变量定义为整数型（求值结果仅为整数，否则显示为0）；

- -a name：声明变量为普通数组；

- -A name：声明变量为关联数组（支持索引下标为字符串）；

- -F  仅显示函数名（格式为declare -f function_name）；

- -g name：在shell函数中可创建全局变量；

- -p [name]：显示指定变量的属性和值。


### 改变变量属性 ###

	# declare -i ef //声明整数型变量
	# ef=1  //变量赋值（整数值）
	# echo $ef //显示变量内容
	1
	# ef="wer" //变量赋值（文本值）
	# echo $ef 
	0
	# declare +i ef //取消变量属性
	# ef="wer"
	# echo $ef
	wer

### 列出脚本中的函数 ###

	[root@ ~]# cat aa
	aaa(){
	dsfasdf
	}
	bbb(){
	dasfasdf
	}
	
	declare -F
	printf '==============\n'
	declare -f

	[root@ ~]# ./aa
	declare -f aaa
	declare -f bbb
	==============
	aaa () 
	{ 
	    dsfasdf
	}
	bbb () 
	{ 
	    dasfasdf
	}


