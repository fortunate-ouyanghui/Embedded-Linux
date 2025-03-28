- 将hello.c文件上传到ubuntu的/home/oyh/nfs_rootfs/下
- 将开发板的/mnt挂载到ubuntu的/home/oyh/nfs_rootfs/下
```C
mount -t nfs -o nolock,vers=3 192.168.5.11:/home/oyh/nfs_rootfs /mnt
```
- 在ubuntu的/home/oyh/nfs_rootfs/下编译该程序
```C
arm-buildroot-linux-gnueabihf-gcc -o hello hello.c
```
- 运行
```C
./hello
```
