# linux系统同步时间

## centos7

```shell
#更新系统时间---年月日
[root@Centos7.x ~]# timedatectl set-time 2018-08-30

#更新系统时间---时分秒
[root@Centos7.x ~]# timedatectl set-time 10:25:17

###以上两步都是人为设置时间，并不准确，所以有网络的情况下我们一般用ntpdate命令更新系统时间
[root@Centos7.x ~]# ntpdate ntp1.aliyun.com

#更新时区(亚洲-中国-上海)
[root@Centos7.x ~]# timedatectl set-timezone Asia/Shanghai

#设置硬件时间
[root@Centos7.x ~]# hwclock --set --date="06/18/14 14:55" （月/日/年时:分:秒）
或者
[root@Centos7.x ~]# clock --set --date="06/18/14 14:55"   （月/日/年时:分:秒）

#将硬件时钟调整为与系统时钟一致
[root@Centos7.x ~]# timedatectl set-local-rtc 1
或者
[root@Centos7.x ~]# hwclock --systohc --localtime (好像这个更有效)

#最后将日期写入CMOS永久生效
[root@Centos7.x ~]# clock -w 
或者
[root@Centos7.x ~]# hwclock -w 

#再次查看系统时间和硬件时间，他们就一致了
```

## centos6

```shell
#更新系统时间---年月日
[root@Centos6.x ~]#date -s  2018-08-30

#更新系统时间---时分秒
[root@Centos6.x ~]# date -s 10:25:17

###以上两步都是人为设置时间，并不准确，所以有网络的情况下我们一般用ntpdate命令更新系统时间
[root@Centos6.x ~]# ntpdate ntp1.aliyun.com



#更新时区(亚洲-中国-上海)
[root@Centos6.x ~]# vi /etc/sysconfig/clock 
ZONE="Asia/Shanghai"

#设置硬件时间
[root@Centos6.x ~]# hwclock --set --date="06/18/14 14:55" （月/日/年时:分:秒）
或者
[root@Centos6.x ~]# clock --set --date="06/18/14 14:55"   （月/日/年时:分:秒）

#硬件时钟与系统时钟同步:hc代表硬件时间，sys代表系统时间，即用硬件时钟同步系统时钟
[root@Centos6.x ~]# hwclock --hctosys
或者 
[root@Centos6.x ~]# clock --hctosys  


#系统时钟和硬件时钟同步：即用系统时钟同步硬件时钟
[root@Centos6.x ~]# hwclock --systohc 
或者 
[root@Centos6.x ~]# clock --systohc  

#最后将日期写入CMOS永久生效
[root@Centos6.x ~]# clock -w 
或者
[root@Centos6.x ~]# hwclock -w 

#再次查看系统时间和硬件时间，他们就一致了
```

