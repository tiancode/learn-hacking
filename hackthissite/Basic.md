全是基本问题，比较简单。

***

### Lv1：<https://www.hackthissite.org/missions/basic/1/>

sam把密码写到了html中；在Html中找密码；密码是`ab7b6ce8`:

![lv1](https://github.com/tiancode/start-learn-kali-linux/blob/master/hackthissite/image/Screen%20Shot%202016-05-09%20at%2016.36.37.png)

***

### Lv2：<https://www.hackthissite.org/missions/basic/2/>

Sam使用脚本判断用户输入的密码是否和文件中的明文密码匹配，但是他忘记了上传密码文件；直接提交就可以（Null == Null）。

***

### Lv3：<https://www.hackthissite.org/missions/basic/3/>

承接上一题，Sam提交了这个文件，but there were deeper problems than that。

找到判断密码的脚本文件password.php：

![Lv3](https://github.com/tiancode/start-learn-kali-linux/blob/master/hackthissite/image/Screen%20Shot%202016-05-09%20at%2017.14.06.png)

访问 <https://www.hackthissite.org/missions/basic/3/password.php> 直接获取密码：5e9fadc2。

***

### Lv4：<https://www.hackthissite.org/missions/basic/4/>

Samc创建了一个php脚本用来发送他的密码；更改html中sam的邮件地址为自己的邮件地址：

![Lv4](https://github.com/tiancode/start-learn-kali-linux/blob/master/hackthissite/image/Screen%20Shot%202016-05-09%20at%2017.32.21.png)

点击Send password to Sam：

![Lv4](https://github.com/tiancode/start-learn-kali-linux/blob/master/hackthissite/image/Screen%20Shot%202016-05-09%20at%2017.28.10.png)
