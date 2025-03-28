## 交叉编译hello程序
```C
#include <stdio.h>

/**
 * 编译 gcc -o hello hello.c
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
