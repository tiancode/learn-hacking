---
layout: post
title: 使用foremost恢复删除的文件
---

foremost是一个根据文件头和内部数据恢复文件的一个工具。

> Recover files using their headers, footers, and data structures.

最初代码是由美国空军特别调查办公室（OSI）的两个调查员编写的，主要是为了犯罪调查。

它可以恢复的文件类型：

```
jpg    Support for the JFIF and Exif formats including  implementations
              used in modern digital cameras.
gif
png
bmp    Support for windows bmp format.
avi
exe    Support  for Windows PE binaries, will extract DLL and EXE files
              along with their compile times
mpg    Support for most MPEG files (must begin with 0x000001BA)
wav
riff   This will extract AVI and RIFF since they use the same file for‐
              mat (RIFF). note faster than running each separately.
wmv    Note may also extract wma files as they have similar format.
mov
pdf
ole    This  will  grab  any  file  using the OLE file structure.  This
              includes PowerPoint, Word, Excel, Access, and StarWriter
doc    Note it is more efficient to run OLE as you get  more  bang  for
              your  buck.   If you wish to ignore all other ole files then use
              this.
zip    Note is will extract .jar files as well because they use a simi‐
              lar  format.   Open Office docs are just zip'd XML files so they
              are extracted as well.  These include SXW, SXC, SXI, and SX? for
              undetermined  OpenOffice  files.  Office 2007 files are also XML
              based (PPTX,DOCX,XLSX)
rar
htm
cpp    C source code detection, note this is primitive and may generate
              documents other than C code.
mp4    Support for MP4 files.
all    Run  all  pre-defined  extraction  methods. [Default if no -t is
              specified]
```

Kali Linux默认安装了foremost；如果你使用的是Ubuntu，可以执行如下命令安装：

{% highlight shell %}
# apt-get install foremost
{% endhighlight %}

### 使用foremost恢复文件

假如你误删了一个png文件：

{% highlight shell %}
# rm -f test.png
{% endhighlight %}

恢复：

{% highlight shell %}
# foremost -t png -i /dev/sda1
{% endhighlight %}

恢复的文件默认保存在当前的output目录。

如果你不知道要恢复的文件在哪个分区，可以使用mount命令查看。

注：它也支持Windows的文件系统；如果文件所在的硬盘块区已经被其他数据覆盖，那么这个文件就不可恢复了。

如果硬盘很大也许需要用很长时间执行。执行完成之后，去output目录找到已恢复的文件。

output根目录有一个audit.txt的文件，它保存了foremost执行的汇总信息。

*****

如果要恢复所有支持的文件，使用all：

{% highlight shell %}
# foremost -t all -i /dev/sda1
{% endhighlight %}

关于foremost的更多信息，查看帮助：

{% highlight shell %}
# man foremost
{% endhighlight %}