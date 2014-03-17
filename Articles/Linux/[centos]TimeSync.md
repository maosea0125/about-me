[centos]系统同步网络时间  
==========

- 安装ntp: yum -y install ntp
- 安装rdate: yum -y install rdate
- 添加cronjob: * */2 * * *  /usr/sbin/ntpdate time-b.timefreq.bldrdoc.gov
- 也可以通过命令同步: ntpdate time-b.timefreq.bldrdoc.gov