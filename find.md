#Linux中find命令的用法
---

首先我们得知道几个在find命令中有特殊含义的符号:
**单个字符"?",多个字符" * ","-a"并且,"-o"或,"-not"否** 

find -name * cc 表示查找当前目录以及子目录下所有以cc为结尾的文件
find -name mysql * 查找当前目录及字母下所有以mysql开头的文件
find -name mysql * -o -name * cc //查找以mysql开头或者cc结尾的文件

**没有搜索目录,默认是当前目录,也可以在find后面加上目录名 find/data -name xxxx** 

+ -amin n 查找系统中N分钟之前访问的文件 access
+ -atime n 查找系统中nx24小时之前访问的文件
+ -cmin n 查找系统中N分钟之前被改变状态的文件 比如新建\删除操作
+ -ctime n 查找系统中nx24小时之前被改变状态的文件
+ -mmin n 查找系统中N分钟之前被改变文件数据的文件
+ -mtime n 查找系统中nx24小时之前被改变文件数据的文件 

find -mmin -10 //超照最近10分钟修改过的文件
find /temp -atime -1 //查找一天之内在/temp目录下访问过的文件

find /temp -prem 755 //查找/temp目录下权限是755的文件 **这是通过权限条件查找** 

find -size +100M //搜索大于100M的文件 **这是通过文件大小条件查找** 
find -size +100M -l //搜索大于100M的文件,并显示详情

`find -type d[or f]  d是目录,f是文件` 

-exec 让我们用find这个命令去做一件事情
find /temp/ding.html -exec mv {} {}.`date+%F` \;
对找到的文件加上年-月-日;ding.html.2019-11-09
find /temp -atime +30 -exec rm -rf {} \;
***用find搭配exec函数会更方便***

