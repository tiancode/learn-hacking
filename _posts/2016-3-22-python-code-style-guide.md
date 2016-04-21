---
layout: post
title: pep8：Python代码风格检查工具
---

Python官网定义的代码风格 [PEP 0008 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)。

pep8是检测编码风格是否符合 **_PEP 0008_** 的工具。

**安装pep8：**

{% highlight shell %}
pip install pep8
{% endhighlight %}

**升级pep8：**

{% highlight shell %}
pip install --upgrade pep8
{% endhighlight %}

**卸载pep8：**

{% highlight shell %}
pip uninstall pep8
{% endhighlight %}

*******

如果使用的是Ubuntu，还可以使用从apt仓库中安装：

{% highlight shell %}
$ sudo apt-get install pep8
{% endhighlight %}

###使用示例

故意写几行不符合Python编码风格的代码（test.py）：

{% highlight python %}
import sys, os
from subprocess import Popen, PIPE

def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
{% endhighlight %}

检查是否符合编码规范：

{% highlight shell %}
$ pep8 --first test.py
test.py:1:11: E401 multiple imports on one line
test.py:4:1: E302 expected 2 blank lines, found 1
test.py:6:5: E125 continuation line with same indent as next logical line
{% endhighlight %}

1、4、6行代码不符合规范

你还可以输出不符合规范的代码和原因：

{% highlight shell %}
$ pep8 --show-source --show-pep8 test.py
{% endhighlight %}

![pep8]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-22 at 18.41.49.png)

更多选项，查看帮助信息：

{% highlight shell %}
$ pep8 -h
{% endhighlight %}

********

使用代码测试(CodeStyle.py)：

{% highlight python %}
import pep8

python_code_style_checker = pep8.Checker('test.py', show_source=True)
file_errors = python_code_style_checker.check_all()
print("Found %s errors (and warnings)" % file_errors)
{% endhighlight %}

![pep8 code style]({{ site.baseurl }}/images/2016/3/Screen Shot 2016-03-22 at 18.49.03.png)