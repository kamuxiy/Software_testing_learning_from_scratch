# Linux 基础

## 1.操作系统定义和作用

操作系统直接运行在计算机上的系统软件， 它是控制硬件和支持软件运行的计算机程序。
向下控制硬件向上支持软件的运行，具有承上启下的作用。

## 2.常用虚拟机软件

- VMware
- VirtualBox

## 3.在虚拟机上安装 Linux

推荐几个教程，也可以自己去搜，网上有很多详细教程。

[VMware 虚拟机安装 Linux 教程(超详细)-七维大脑](https://blog.csdn.net/weixin_52799373/article/details/124324077)

## 4.Linux 常用命令（重要）

- `ls`：列出目录下的文件
- `pwd`：显示当前工作目录
- `clear`: 清屏
- `cd`：切换目录
- `touch`：创建文件
- `mkdir`：创建目录
- `rmdir`：删除目录
- `rm`：删除文件，`-r`递归删除文件，`-f`强制删除文件
- `cp`：复制文件
- `mv`：移动文件
- `cat`：查看文件内容
- `echo`：输出内容到文件
- `find`：查找文件，`-name`: 查找文件名，一般使用通配符`*`表示 0 或多个字符，`?`表示一个字符
- `grep`：查找文件中包含指定字符串的行
- `chmod`：修改文件权限，一般使用数字法，`-R`递归修改文件权限，可读为`4`，可执行为`1`，可写为`2`
- `tail`：显示文件的后几行
- `vi`、`vim`：编辑文件
- `>`: 将文件内容重定向到另一个文件(覆盖)
- `>>`: 将文件内容重定向到另一个文件(追加)

\*软硬连接、正则表达、压缩、用户操作做了解即可

## 5.ssh

使用`ssh 用户名@主机名`登录主机

# 6.重点要记的命令

`ifconfig` 查看网卡的配置
`ifconfig ethX up` 启用 'ethX' 网卡设备信息
`ifconfig ethX down` 禁用 'ethX' 网卡设备信息
`ping IP/域名` 测试从本机到对方网络的连通性
`du -h filename` 以适合的方式查看文件占用磁盘空间大小
`du -sh dirname` 查看指定文件目录下磁盘占用量
`tail -f filename` 动态显示文件内容(默认后 10 行) （可通过 echo 重定向演 示）
`export` 环境变量查看
`export env="value"` 添加环境变量
`wget url` 下载文件
`wget url -O filename` 下载文件并重命名
`uname -a` 显示内核版本
`cat /etc/redhat-release` 查看 centos 版本
`ps -aux` 或 `ps -ef` 显示进程状态
`kill pid` 停止某进程
`kill -9 pid` 强制杀掉进程
`history` 显示历史输入的命令
`top` 动态的显示系统耗费资源最多的进程(P 按 cpu 排序 M 按 memory 排序 Q 退出)
`poweroff` 关机
`reboot` 重启
`free` 显示内存使用情况( `-k` 以 KB 为单位，`-m` 以 MB 为单位，`-g` 以 GB 为单位)
`systemctl status firewalld` 查看防火墙状态
`systemctl stop firewalld` 关闭防火墙
`netstat -an` 查看端口使用情况
`du -h --max-depth=0 *` 查看当前目录文件及文件夹大小
`ps -ef | grep 'xxx' |awk '{print $2}' |xargs kill -9` 停止包含 xxx 相关的进程
