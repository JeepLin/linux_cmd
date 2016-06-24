###mac下ssh配置

//打开mac下当前用户的ssh配置文件<br>
jeepdeMac-mini:~ jeep$ cd ~/.ssh/<br>

//创建config文件<br>
jeepdeMac-mini:.ssh jeep$ vim config <br>

config文件：<br>
Host dev1<br>
 HostName sgdev1.klook.com<br>
 User centos<br>
 IdentityFile ~/.ssh/klook-dev1603.pem<br><br>
Host dev2<br>
 HostName sgdev2.klook.com<br>
 User centos<br>
 IdentityFile ~/.ssh/klook-dev1603.pem<br><br>


//把秘钥文件放到IdentityFile文件下，并开始连接：<br>
jeepdeMac-mini:.ssh jeep$ ssh dev1<br>
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@<br>
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @<br>
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@<br>
Permissions 0755 for '/Users/jeep/.ssh/klook-dev1603.pem' are too open.<br>
It is required that your private key files are NOT accessible by others.<br>
This private key will be ignored.<br>
Load key "/Users/jeep/.ssh/klook-dev1603.pem": bad permissions<br>
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).<br>

//查看密钥权限：<br>
jeepdeMac-mini:.ssh jeep$ ls -all klook-dev1603.pem <br>
-rwxr-xr-x@ 1 jeep  staff  1675  6 23 10:40 klook-dev1603.pem<br><br>

//修改密钥权限为600<br>
jeepdeMac-mini:.ssh jeep$ chmod 600 klook-dev1603.pem <br>

//重新使用ssh连接，连接成功<br>
jeepdeMac-mini:.ssh jeep$ ssh dev1<br>
Last login: Thu Jun 23 10:22:19 2016 from 14.122.222.136<br>
[centos@klook_dev1_app ~]$ ps -ef | grep "web3.0"<br>
root     24680     1  0 10:23 ?        00:00:00 ./web3.0<br>
centos   29699 29612  0 11:12 pts/2    00:00:00 grep --color=auto web3.0<br><br>

/Users/jeep/.ssh目录结构：<br>
jeepdeMac-mini:.ssh jeep$ ls -all ./<br>
total 56<br>
drwx------   9 jeep  staff   306  6 23 11:15 .<br>
drwxr-xr-x+ 31 jeep  staff  1054  6 23 11:15 ..<br>
-rw-r--r--   1 jeep  staff   179  6 23 11:11 config<br>
-rw-------   1 jeep  staff  1675  6 17 10:56 id_boot2docker<br>
-rw-r--r--   1 jeep  staff   407  6 17 10:56 id_boot2docker.pub<br>
-r--------   1 jeep  staff  1766  5 30 11:59 id_rsa<br>
-rw-r--r--   1 jeep  staff   396  5 30 11:59 id_rsa.pub<br>
-rw-------@  1 jeep  staff  1675  6 23 10:40 klook-dev1603.pem<br>
-rw-r--r--   1 jeep  staff   386  6 15 11:12 known_hosts<br>
