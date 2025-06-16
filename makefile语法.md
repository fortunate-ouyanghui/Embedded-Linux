## 基本语法
```C
目标文件：依赖
tab键 命令
例如：
all:hello.o
  gcc hello.o -o hello
hello.o:hello.c
  gcc -c hello.c -o hello.o
clean:
  rm -rf *.o hello
终端输入：
make all(终端会输出：gcc -c hello.c -o hello.o  gcc hello.o -o hell)
make clean(终端会输出：rm -rf *.o hello)
========================================================================

伪目标(避免文件名重名冲突)
示例：
.PHONY:clean
clean:
  rm -rf *.o hello
========================================================================

变量
变量赋值：
第一种   :=                    (立刻赋值)
第二种   ?=                    ()
第三种   =                     ()
第四种   +=                    ()
变量引用：$(变量名)
示例1：使用=来延迟赋值,使用=来赋值var1赋值的是makefile文件中var1最后被指定的值
var1=aaa
var2=$(var1)bbb
var1=ccc
all:
  echo $(var2)#这里会打印cccbbb而不是aaabbb

示例2：使用?=来赋值，如果var1变量前面没有被赋值，那么就给他赋值为ccc，如果前面已经赋值了，那就i使用前面的值
var1:=aaa
var1?=ccc
var2:=$(var1)bbb
all:
  echo $(var2)#这里会打印aaabbb

示例3：使用+=来赋值，+=是追加赋值
var1:=aaa
var1+=ccc
var2:=$(var1)
all:
  echo $(var2)#这里会打印aaa ccc
========================================================================

自动化变量
hello:hello.o main.o
	gcc hello.o main.o -o hello
hello.o:hello.c
	gcc -c hello.c -o hello.o
main.o:main.c
	gcc -c main.c -o main.o

.PHONY:clean
clean:
	rm -rf *.o hello
简化为:使用$^表示所有依赖 %是通配符 $<表示一系列文件 $@表示所有目标
var:=hello.o main.o
hello:$(var)
	gcc $^ -o hello
%.o:%.c
	gcc -c $< -o $@

.PHONY:clean
clean:
	rm -rf *.o hello
========================================================================

函数
wildcard函数
语法：$(wildcard PATTENR)
功能：展开指定的目录
示例： ./a.c  ./test/b.c有这两个目录
var=(wildcard ./*.c ./test/*.c)
all:
	@echo $(var)#打印 ./a.c 和 ./test/b.c

notdir函数
语法：$(notdir $(var))
功能：去掉路径
示例：
var1=$(wildcaid ./*.c ./test/*.c)
var=$(notdir $(var))
all:
	@echo $(var)#打印a.c 和 b.c

dir函数
语法：$(dir <names...>)
功能：取出目录，这里的目录是指最后一个反斜杠/之前的部分
示例：
var1=$(wildcard ./*.c ./test/*.c)
var2=$(notdir $(var))
var3=$(dir $(var1))
all:
	@echo $(var3)#这里会打印./ 和 。/test/

patsubst函数
语法：$(patsubst 原文件，目标文件，文件列表)
功能：替换文件后缀
示例：这个函数会把var1变量的a.c和b.c的.c后缀替换为.o然后赋值给var2
var=$(wildcard ./*.c ./test/*.c)
var1=$(notdir $(var))
var2=$(patsubst %.c,%.o,$(var1))等价于var2=$(var1:%.c=%.o)
all:
	@echo $(var2)#a.o b.o

foreach函数
语法：$(foreach <var>,<list>,<test>)
功能：把参数<list>中的单词逐一取出放到参数<var>所指定的变量中，然后再执行<test>所包含的表达式。每一次<test>会返回一个字符串
示例：因为var2变量的值为./和./test,所以先把./取出来放在n变量，然后执行wildcard函数得到./*.c;然后取出./test放在n变量，然后执行wildcard函数得到./test/*.c。最后把得到的./a.c和./test/b.c赋值给变量var3
var=$(wildcard ./*.c ./test/*.c)
var1=$(notdir $(var))
var2=$(dir $(var))
var3=$(foreach n,$(var2),$(wildcard $(n)*.c))
all:
	@echo $(var3)#./a.c ./test/b.c
```
