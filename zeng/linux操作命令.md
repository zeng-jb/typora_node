1. 开启防火墙

~~~
systemctl start firewalld
~~~

2. 查看指定端口，yes则已开启。

~~~
firewall-cmd --zone= --query-port=3306/tcp
~~~

3. 重启防火墙

~~~
firewall-cmd --reload
~~~

4. 开放指定端口

~~~
firewall-cmd --zone=public --add-port=3306/tcp --permanent
~~~



### Failed to start ssh.service: Unit ssh.service not found.

~~~shell
sudo apt-get install openssh-server
~~~

1.  安装 open ssh:  sudo apt-get install openssh-server
2. 辑配置文件，允许以 root 用户通过 ssh 登录：
          a): sudo vi /etc/ssh/sshd_config
          b): PermitRootLogin prohibit-password  --禁用
          c): PermitRootLogin yes -- 添加
          d):  :wq! -- 保存
3. 重新启动: sudo service ssh restart
4. 重新登陆；






### Ubuntu执行apt-get update报错

更改镜像源

1. 先备份

~~~shell
cd /etc/apt
sudo tar -zcvf sources.list.tar.gz sources.list
~~~

![image-20220303113859809](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/PCAutor/image-20220303113859809.png)

2. 打开 `sudo vim sources.list`

![image-20220303114014365](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/PCAutor/image-20220303114014365.png)

将这些全部改成

~~~
http://mirrors.aliyun.com/ubuntu
~~~

3. 更新完成后：wq，输入 `sudo apt-get update`

![image-20220303114525966](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/PCAutor/image-20220303114525966.png)





### 安装mysql8.0

1.  `sudo apt update` , `sudo apt install mysql-server`
2. 进行初始化配置 `sudo mysql_secure_installation`，注意enter即可
3. 查看版本 `mysql --version`
4. 查看mysql运行状态 `systemctl status mysql.service`
5. 进行连接 `sudo mysql -u root -p`

远程配置连接

`sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf`

打开文本注释掉   `bind-address=127.0.0.1`

重启mysql服务 `sudo /etc/init.d/mysql restart`

连接mysql

~~~
//转换mysql
use mysql;
//创建账户
CREATE USER 'root'@'%' IDENTIFIED BY '123456';
//账户授权
grant all privileges on *.* to 'root'@'%';
//权限刷新
FLUSH PRIVILEGES;
//查看账户
select host, user, authentication_string, plugin from user;
~~~



Public Key Retrieval is not allowed：解决办法

最简单的解决方法是在连接后面添加 `allowPublicKeyRetrieval=true`
