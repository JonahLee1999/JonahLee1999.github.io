---
layout: post
title: kramdown的rough有无行号
categories: Blog
description: kramdown的rough高亮
keywords: highlight
---

我fork的模板中其实已经设置了代码高亮了，这里只是打下怎么设置行号。


### 无行号

在这个模板里，其实只要用*```cpp*(用于代码前)和*```*(用于代码后)就可以设置代码高亮了。注意那个cpp其实是你所用的语言。可以是Java和Python还有Ruby之类的，然后就是不要打错。之前我打成了*```C++*就老是高亮不出来，真是习惯害死人啊。


* Show

```cpp
	for(int i=1;i<n;i++)
	{
		int k=0;//寻找之前小于子序列的最大值 
		for(int j=i-1;j>=0;j--)
		{
			if(a[j]>=a[i]&&k<b[j])
			{
				k=b[j];
			}
		}
		b[i]=k+1;
		if(b[i]>max)
			max=b[i];
	}
```




### 有行号

有行号的话那么在代码前加上 *{% highlight cpp linenos %}* ，代码后加上 *{% endhighlight %}* ，不要使用*```cpp*了。其中cpp是使用的语言，linenos是行号。


* Show
{% highlight cpp linenos %}
	for(int i=1;i<n;i++)
	{
		int k=0;//寻找之前小于子序列的最大值 
		for(int j=i-1;j>=0;j--)
		{
			if(a[j]>=a[i]&&k<b[j])
			{
				k=b[j];
			}
		}
		b[i]=k+1;
		if(b[i]>max)
			max=b[i];
	}
{% endhighlight %}