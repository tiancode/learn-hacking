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

***

### Lv6：<https://www.hackthissite.org/missions/basic/6/>

Sam使用算法加密了他的密码，我们需要破解这个算法，幸运的是这个算法是可以公开的。

输入abcdef1234，加密为acegik79;=

abcdef012345 ->   acegik68:<>@
    
abcdef     ->     acegik
    
ABCEDF     ->     ACEGIK
    
012345678  ->     02468:<>@B
    
a0123456   ->     a13579;=
    
多输入几个查看规律；C语言解密代码：

```
#include <stdio.h>
#include <string.h>

void decrypt(char *str, char* out)
{
	for(int i = 0; i < strlen(str); i++)
	{
		out[i] = str[i] - i;
	}
}

int main(int argc, char *argv[])
{
	char out[32] = {0};
	decrypt("57d9;hg=", out);
	printf("%s\n", out);
}
```

Sam的加密密码为57d9;hg=，原密码是：56b67ca6

### Lv7：<https://www.hackthissite.org/missions/basic/7/>

看完描述，最先想到的攻击方式就是shell注入攻击。

输入`2016;ls`；找到当前目录的密码文件`k1kh31b1n55h.php`，然后访问 <https://www.hackthissite.org/missions/basic/7/k1kh31b1n55h.php> 查看密码：63474cd3

### Lv8：<https://www.hackthissite.org/missions/basic/8/>

Sam的女儿用PHP写了一些php代码保存文件。

提示：[Server-Side Includes (SSI) Injection](https://www.owasp.org/index.php/Server-Side_Includes_(SSI)_Injection)

输入：`<!--#exec cmd="ls ../" --> ` ， 访问[au12ha39vc.php](https://www.hackthissite.org/missions/basic/8/au12ha39vc.php) 获得密码：e1361dfd
