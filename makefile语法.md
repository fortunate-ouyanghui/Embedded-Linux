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


```
