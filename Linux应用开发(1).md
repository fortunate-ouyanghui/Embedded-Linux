## 交叉编译hello程序
```C
#include <stdio.h>

/**
 * 编译 arm-buildroot-linux-gnueabihf-gcc -o hello hello.c
 * 运行：
 *      1. 终端输入：./hello oyh   ->程序输出：hello oyh
 *      2. 终端输入：./hello      ->程序输出：hello world
 * 解释：argc表示参数个数
 *      argv表示参数内容，其中第一个参数是程序名即./hello,在运行方式1中，第一个参数是程序名，第二个参数是oyh；在运行方式2中，第一个参数是程序名，第二个参数为空
 */

int main(int argc,char** argv)
{
    if(argc>=2)
    {
        printf("hello %s\n",argv[1]);
    }
    else
        printf("hello world\n");
    return 0;
}
```
## GCC
- GCC编译过程
![22](https://github.com/user-attachments/assets/bece743d-0d7b-4bc0-b93f-16d0182517c1)
![33](https://github.com/user-attachments/assets/629d95c9-c390-46cb-8b96-19dd3c9be05f)
- GCC常用选项
![44](https://github.com/user-attachments/assets/2672b87c-46cb-49a9-b032-cbcd256b6ac6)
- 制作静态库
```C
制作
gcc -c -o add.o add.c
ar crs libadd.a add.o
使用
gcc -o test main.c libadd.a
```
- 制作动态库
```C
制作
gcc -c -o add.o add.c
gcc -shared -o libadd.so add.o
使用
gcc -o test main.c libadd.so或gcc -o test main.c ladd -L /bin/
```

