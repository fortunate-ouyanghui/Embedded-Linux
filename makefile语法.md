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
```
