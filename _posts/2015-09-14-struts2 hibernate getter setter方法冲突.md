---
layout: post
title: "struts hibernate getter setter方法冲突"
categories: ssh学习
tags: struts hibernate
---

今天配置struts hibernate环境时遇到一个问题。
这是我的资源实体中的一个属性,get set方法使用eclipse generate 方法生成的。
{% highlight java linenos %}
private int pId;
	
    public int getpId() {
        return pId;
    }
    
    public void setpId(int pId) {
        this.pId = pId;
    }
    
{% endhighlight java %}

可这样在表单中:
{% highlight html linenos %}
<input type="text" name="resource.pId">
{% endhighlight java %}

总是在action中取不到pId的值，同时在后台保存一个new的resource是成功的。
后来才发现struts和hibernate对get set方法的要求存在一点不同。
eclipse的自动生成的get set 方法,hibernate是认可的。
struts则需要注意一点，就是类似于pId这样的命名，struts认可的set get方法是：
{% highlight java linenos %}
public void setPId(int pId) {
        this.pId = pId;
    }
    public int getPId() {
        return pId;
    }
{% endhighlight java %}
所以最后的解决办法就是

####1. 不嫌麻烦的可以写成这样
{% highlight java linenos %}
private int pId;
	
    public int getpId() {
        return pId;
    }
    
    public void setpId(int pId) {
        this.pId = pId;
    }
    public void setPId(int pId) {
        this.pId = pId;
    }
    public int getPId() {
        return pId;
    }
{% endhighlight java %}

####2. 老老实实改属性名称，不要使用类似pId这样的。