# Linux
+++
* #### 基础语句

  cd：进入目录  pwd：显示路径  ls：查看文件等

  cat file1：查看file1的文件内容

​	rm:删除文档  mkdir:创建目录   cp file1 dir1:复制file1到dir1   mv file2 dir2:移动file2到dir2

​	（/filecp）是重命名为filecp的意思

<img src="C:\Users\ZhuanZ（无密码）\Pictures\Screenshots\屏幕截图 2026-01-29 140909.png" alt="屏幕截图 2026-01-29 140909" style="zoom:80%;" />

​	rmdir:删除空目录   rm -r:删除非空目录

​	head/tail file:查看前/后10行（默认10行

​	head/tail -n 5 file:查看前/后5行

​	grep "l" file1 **其中-n显示行号   -i忽略大小写   -r在目录中递归查找**

<img src="C:\Users\ZhuanZ（无密码）\Pictures\Screenshots\屏幕截图 2026-01-29 150001.png" alt="屏幕截图 2026-01-29 150001" style="zoom:80%;" />

(^C是强制退出)

​	find -name "file3":（默认在当前目录）查找file3文件的地址

​	find -name “*3”：查找带有"3"的文件的地址

![屏幕截图 2026-01-29 152732](C:\Users\ZhuanZ（无密码）\Pictures\Screenshots\屏幕截图 2026-01-29 152732.png)

​	find -size +/- nM:查找大于/小于n兆的文件

​	find -maxdepth 2 -size +/- nM:层数区别

​	find -mtime -1:在一天内被**修改**的文件   find -mmin -1:在1分钟之内被**修改**的文件

​	fine -ctime -cmin:在一天 一分钟内被**创建**的文件

​	find -type f(查找文件) d(查找目录) l(查询符号)

​	<img src="C:\Users\ZhuanZ（无密码）\Pictures\Screenshots\屏幕截图 2026-01-29 160344.png" alt="屏幕截图 2026-01-29 160344" style="zoom:80%;" />

（还不会就看这个视频https://www.bilibili.com/video/BV1hw411z7Eh/?spm_id_from=333.337.search-card.all.click&vd_source=0f90f2fa90be4f490a6243549c4fbe7f

+ #### nano基本用法

​	-l：行号   -m：用鼠标点击或滚动   +n：跳转到第n行

+ #### ssh

​	ping (ip地址) 判断是否联通

```Linux
ssh -p 22 user@host
```

​    -p：指定端口号    user：登录的用户名    host：登录的主机。(22为默认端口号)

​	tbc…

















