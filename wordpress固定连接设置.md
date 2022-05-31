# Wordpress固定连接设置



首先我们去wordpress后台，设置->固定连接，我们选择自定义结构

![image-20220307100613428](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/image-20220307100613428.png)

一般像这样既可。url就会变成这样

![image-20220307100720877](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/image-20220307100720877.png)

我们也可以在postid后面加上 `.html` 这样我们写的文章页面就会有带html后缀的url啦。

但是问题来啦？我们这样设置一般来说会直接404，并且我们建立的分类也是404，那应该怎么解决呢？

**我们可以这样做：**

1. 用 [SmartFTP](https://www.smartftp.com/)连接我们的建立网站的根目录

![image-20220307101300905](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/image-20220307101300905.png)

2. 我们看到有个 `.htaccess`文件的，我们右键编辑它
3. 将代码复制进去

~~~
RewriteEngine On

RewriteBase /

RewriteRule ^index\.php$ – [L]

RewriteCond %{REQUEST_FILENAME} !-f

RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule . /index.php [L]
~~~

4. 保存
5. 网站刷新一下，我们可以看到可以正常访问页面啦，我们建立的分类也没问题

![image-20220307102204256](https://gitee.com/zeng-jiabin/typora_imgs/raw/master/image-20220307102204256.png)



6. 大功告成