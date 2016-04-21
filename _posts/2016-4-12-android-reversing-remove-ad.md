---
layout: post
title: 移除Android应用广告－Android逆向工程
---

我用以前做过的一个小游戏为例，源代码地址：<http://git.oschina.net/androidsourcecode/parity>，如果不想自己编译，其中已有编译好的APK包（Parity-release-signed.apk）。这个游戏内使用了google的插页广告。我的目的是逆向破解这个apk，去掉其中的广告。

[Android逆向工程基本环境设置](http://topspeedsnail.com/android-reversing-env-setup/)

********

如果要破解的应用已经安装到了手机里，我们需要使用adb pull从手机里下载这个app。

确保手机已打开usb调试，连接到电脑，执行：

{% highlight shell %}
# adb shell 'pm list packages -f'
{% endhighlight %}

上面命令列出了android手机中已安装的app，找到要破解的app：

![adb shell list app]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-12 11-48-46.png)

下载app：

{% highlight shell %}
# adb pull /data/app/com.topspeedsnail.parity-1/base.apk
{% endhighlight %}

*********

使用apktool解压、反汇编要破解的apk：

{% highlight shell %}
# apktool d base.apk
{% endhighlight %}

d选项是decode的意思。

如果出现如下错误，说明你的apktool工具没有安装正确的framework。

```
I: Decoding AndroidManifest.xml with resources...
I: Loading resource table from file: /root/apktool/framework/1.apk
W: Could not decode attr value, using undecoded value instead: ns=android, name=versionCode, value=0x00000001
I: Loading resource table from file: /root/apktool/framework/1.apk
W: Could not decode attr value, using undecoded value instead: ns=android, name=versionName, value=0x00000019
I: Loading resource table from file: /root/apktool/framework/1.apk
W: Could not decode attr value, using undecoded value instead: ns=android, name=versionCode, value=0x00000001
I: Loading resource table from file: /root/apktool/framework/1.apk
W: Could not decode attr value, using undecoded value instead: ns=android, name=versionName, value=0x00000019
Exception in thread "main" java.lang.NullPointerException
	at java.io.Writer.write(Writer.java:157)
	at brut.androlib.res.util.ExtMXSerializer.writeAttributeValue(ExtMXSerializer.java:38)
```

关于apktool framework的解释：

> As you probably know, Android apps utilize code and resources that are found on the Android OS itself. These are known as framework resources and Apktool relies on these to properly decode and build apks. 
> 
> Every Apktool release contains internally the most up to date AOSP framework at the time of the release. This allows you to decode and build most apks without a problem. However, manufacturers add their own framework files in addition to the regular AOSP ones. To use apktool against these manufacturer apks you must first install the manufacturer framework files.

解决方法，下载android手机里的framework-res.apk。我使用的系统是android 5.1。

![adb shell]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-12 12-15-25.png)

把下载的文件移动到apktool的framework目录：

{% highlight shell %}
# mv framework-res.apk /root/apktool/framework/1.apk
{% endhighlight %}

再次反编译；反汇编之后的目录：

![apktool]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-12 12-45-42.png)

你应该对比源代码好好的研究一下这个目录。

**********

从AndroidManifest.xml文件和smali/com/google/ads目录可以看出，这个游戏使用了google广告。

![android]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-12 12-52-50.png)

![android]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-12 12-54-48.png)

### 移除广告最简单的方法

找到google投放代码的ID（AdmodPlugin.smali）：

![android]({{ site.baseurl }}/images/2016/4/Screenshot from 2016-04-12 13-07-43.png)

对应的源代码：

{% highlight java %}
public class AdmobPlugin {
	private static Cocos2dxActivity activity;
    private static final String TAG = "cocos2d";
	private static InterstitialAd interstitial;
	private static AdView adView;
	
	private final static String MY_INTERSTITIAL_ID = "ca-app-pub-28...";
	private final static String MY_BANNER_ID = "ca-app-pub-286...";
	
	public static void setActivity(Cocos2dxActivity act){
		activity = act;
	}
	...
{% endhighlight %}

把AdmodPlugin.smali中的广告ID更改为无效ID；

有些人会替换为自己的ID然后再打包发布－咒生孩子没屁眼!!!咒

打包为apk文件：

{% highlight shell %}
# apktool b base -o base_no_ads.apk
{% endhighlight %}

如果有如下错误：

```
I: Building resources...
W: aapt location could not be found. Defaulting back to default
Exception in thread "main" brut.androlib.AndrolibException: brut.androlib.AndrolibException: brut.common.BrutException: could not exec command: [aapt, p, --forced-package-id, 127, --min-sdk-version, 9, --version-code, 1, --version-name, 1.0, -F, /tmp/APKTOOL3434486203532207501.tmp, -0, resources.arsc, -0, assets/level/easy/10, -0, assets/level/easy/12, -0, assets/level/easy/14, -0, assets/level/easy/23, -0, assets/level/easy/28, -0, assets/level/easy/4, -0, assets/level/medium/11, -0, assets/level/medium/20, -0, assets/level/medium/4, -0, assets/level/medium/5, -0, assets/level/medium/7, -0, arsc, -I, /root/apktool/framework/1.apk, -S, /root/Hacking/base/res, -M, /root/Hacking/base/AndroidManifest.xml]
	at brut.androlib.Androlib.buildResourcesFull(Androlib.java:465)
	at brut.androlib.Androlib.buildResources(Androlib.java:403)
	at brut.androlib.Androlib.build(Androlib.java:291)
	at brut.androlib.Androlib.build(Androlib.java:261)
	at brut.apktool.Main.cmdBuild(Main.java:225)
	at brut.apktool.Main.main(Main.java:84)
Caused by: brut.androlib.AndrolibException: brut.common.BrutException: could not exec command: [aapt, p, --forced-package-id, 127, --min-sdk-version, 9, --version-code, 1, --version-name, 1.0, -F, /tmp/APKTOOL3434486203532207501.tmp, -0, resources.arsc, -0, assets/level/easy/10, -0, assets/level/easy/12, -0, assets/level/easy/14, -0, assets/level/easy/23, -0, assets/level/easy/28, -0, assets/level/easy/4, -0, assets/level/medium/11, -0, assets/level/medium/20, -0, assets/level/medium/4, -0, assets/level/medium/5, -0, assets/level/medium/7, -0, arsc, -I, /root/apktool/framework/1.apk, -S, /root/Hacking/base/res, -M, /root/Hacking/base/AndroidManifest.xml]
	at brut.androlib.res.AndrolibResources.aaptPackage(AndrolibResources.java:425)
	at brut.androlib.Androlib.buildResourcesFull(Androlib.java:451)
	... 5 more
Caused by: brut.common.BrutException: could not exec command: [aapt, p, --forced-package-id, 127, --min-sdk-version, 9, --version-code, 1, --version-name, 1.0, -F, /tmp/APKTOOL3434486203532207501.tmp, -0, resources.arsc, -0, assets/level/easy/10, -0, assets/level/easy/12, -0, assets/level/easy/14, -0, assets/level/easy/23, -0, assets/level/easy/28, -0, assets/level/easy/4, -0, assets/level/medium/11, -0, assets/level/medium/20, -0, assets/level/medium/4, -0, assets/level/medium/5, -0, assets/level/medium/7, -0, arsc, -I, /root/apktool/framework/1.apk, -S, /root/Hacking/base/res, -M, /root/Hacking/base/AndroidManifest.xml]
	at brut.util.OS.exec(OS.java:94)
	at brut.androlib.res.AndrolibResources.aaptPackage(AndrolibResources.java:419)
	... 6 more
Caused by: java.io.IOException: Cannot run program "aapt": error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at java.lang.Runtime.exec(Runtime.java:620)
	at java.lang.Runtime.exec(Runtime.java:485)
	at brut.util.OS.exec(OS.java:84)
	... 7 more
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.<init>(UNIXProcess.java:248)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 10 more
```

指定aapt所在目录：

{% highlight shell %}
# apktool b --aapt /opt/android-sdk/build-tools/23.0.3/aapt base -o base_no_ads.apk
{% endhighlight %}

签名：

{% highlight shell %}
# keytool -genkey -alias mykey -keyalg RSA -validity 40000 -keystore your.keystore
{% endhighlight %}

{% highlight shell %}
# jarsigner -keystore your_keystore base_no_ads.apk your_key_name
{% endhighlight %}

安装到手机：

{% highlight shell %}
# adb install base_no_ads.apk 
{% endhighlight %}

******

其他移除广告的方法：

* 修改com.google.ads代码，隐藏广告
* 删除调用广告的代码
* 修改资源文件，把android:layout_width 和 android:layout_height改为0px，实现隐藏广告。

对破解最有用的Dalvik汇编指令：if-xxx：条件判断。例如：if-eqz v0, :cond_0，如果v0 == 0，跳转到:cond_0。

****

[学习Android逆向工程](http://topspeedsnail.com/start-learn-android-reversing/)

[Android逆向工具：Androguard（一）](http://topspeedsnail.com/reversing-engineering-android-androguard/)