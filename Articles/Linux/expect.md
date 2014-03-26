使用expect  
==========

**1. 安装expect:**  
- 安装tcl -> http://sourceforge.net/projects/tcl/files/Tcl/8.4.19/tcl8.4.19-src.tar.gz/download  
- 安装expect -> http://download.chinaunix.net/download/0003000/2845.shtml  
- 测试  
<code>#expect
expect1.1></code>

**2. 使用expect实现ssh自动登陆脚本：**

<code>#!/usr/local/bin/expect
set host server
set username john
set password 123456
set prompt "{#|$|>}"
set timeout -1
spawn ssh $username@$host
expect "*?\(yes/no\)*" {
        send "yes\r"
        expect "*?assword:*"
        send "$password\r"
} "*?assword:*" {
        send "$password\r"
}

expect eof</code>

说明:  
- set 设置变量  
- spawn 建立进程  
- send中必须要加"\r"  
- 结束时有interact和expect eof, 在crontab中必须使用expect eof才能正确执行  

3. 相关书籍
- Exploring Expect