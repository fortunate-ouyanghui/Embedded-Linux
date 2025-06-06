# ubuntu基础
## ubuntu各目录作用

 /  
 ├── bin          所有用户都可以使用的、基本的命令  
 ├── boot         启动文件，比如内核等  
 ├── dev          设备文件，Linux特有的  
 ├── etc          配置文件  
 ├── home         家目录  
 │   ├── book     用户book的家目录  
 ├── lib          库  
 ├── media        插上U盘等外设时会挂载到该目录下  
 ├── mnt          用来挂载其他文件系统  
 ├── opt          Optional，可选的程序  
 ├── proc         用来挂载虚拟的proc文件系统，可以查看各进程(process)的信息  
 ├── root         root用户的家目录  
 ├── sbin         基本的系统命令，系统管理员才能使用  
 ├── sys          用来挂载虚拟的sys文件系统，可以查看系统信息：比如设备信息  
 ├── tmp          临时目录，存放临时文件  
 ├── usr          Unix Software Resource, 存放可分享的与不可变动的的数据  
 │   ├── bin      绝大部分的用户可使用指令都放在这里(与开机无关), /bin中的命令跟开机有关  
 │   ├── games    游戏  
 │   ├── include  头文件  
 │   ├── lib      库  
 │   ├── local    系统管理员在本机自行安装、下载的软件  
 │   ├── sbin     非系统正常运作所需要的系统命令  
 │   ├── share    放置共享文件的地方, 比如/usr/share/man里存放帮助文件  
 │   └── src      源码  
 └── var          主要针对常态性变动的文件，包括缓存(cache)、log文件等  
## Shell命令与PATH环境变量
- Linux Shell负责接收用户的输入，根据用户的输入找到其他程序并运行。shell程序会去PATH环境变量所指的位置找该应用程序
  设置PATH的方法：  
  first永久设置
  ```C
  sudo gedit /etc/environment
  ```
  添加环境变量/home/ma
  ```C
  PATH=/opt/ros/humble/bin:/home/oyh/miniconda3/condabin:/home/oyh/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin:/home/ma
  ```
  second临时设置(只对当时终端有效)    
  在bashrc文件中添加
  ```C
  export PATH=$PATH:/home/ma
  ```  
- Linux命令的格式：命令+选项+参数。如：ls -l a
## 目录与文件操作命令
### 目录操作
- 打印当前目录
```C
pwd
```
- 上级路径
```C
cd ..
```
- 家目录
```C
cd ~
```
- 返回上一次目录
```C
cd -
```
### 文件操作
- 创建文件夹 /ms
```C
mkdir ms
```
- 创建文件 1.txt
```C
touch 1.txt
```
- 删除文件或目录
```C
rm ms -rf
```
- 列出内容或目录
```C
ls 
```
- 拷贝文件1.txt为2.txt
```C
cp 1.txt 2.txt
```
- 移动1.txt 到 ms
```C
mv 1.txt /ms
```
- 显示文件1.txt的内容
```C
cat 1.txt
```
### 权限和属性命令
- 赋权指令
```C
chmod 777 /dev/ttyACM0
```
- 改变文件所属用户组
```C
chown root:root 1.txt
```
### find和grep命令
- 查找文件2.txt
```C
find -name 2.txt
```
- 查找指定特点文件
```C
grep "good" * -nwr
```
### 压缩和解压缩命令
- 压缩文件test
```C
tar czf test.tar.gz test
```
- 解压缩
```C
tar xzf test.tar.gz
```
### 网络命令
```C
ifconfig
```
### vi编辑器
- 退出并保存
```C
:wq
```
- 退出不保存
```C
:q!
```
- 删除一个单词
```C
dw
```
- 删除光标后的一整行内容
```C
dd
```
- 查找
```C
/rclcpp 表示查找rclcpp,继续查找下一个rclcpp点击n
```
- 其余看图片  
![1](https://github.com/user-attachments/assets/94ed698a-581b-4ed9-851c-03d39c731446)
