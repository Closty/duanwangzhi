## 演示网址：
[s.clost.net](https://s.clost.net "s.clost.net")

## 介绍：
[![](https://img.shields.io/badge/短网址-极简风格-orange?link=https://s.clost.net)](https://github.com/Closty/duanwangzhi)
[![](https://img.shields.io/badge/by-%E7%93%B6%E5%AD%90-green?link=https://www.clost.net)](https://www.clost.net/default/513.html)
[![HitCount](http://hits.dwyl.com/closty/duanwangzhi.svg)](http://hits.dwyl.com/closty/duanwangzhi)

首先什么叫短网址呢？他有什么用处呢？短网址是指将任何域名更换成一个`t.cn/xxxx`类的网址。
比如将网址[https://www.clost.net](https://www.clost.net "www.clost.net")转化成[https://t.cn/A6wT0J1d](https://t.cn/A6wT0J1d "https://t.cn/A6wT0J1d")

   <details>
   <summary> 那么为什么要转换呢？</summary>
   一方面，直观来说可以将网址变短，比如分享微信的链接，一大串字符会限制你文章字数；另一方面，可以防红，比如你在你的qq分享你的网站，分享过多会导致腾讯    检测并封除域名便会被显示已被拦截等字样，别人以后就只能复制到你的网址在浏览器打开而不能直接在qq内点开。用短网址就可以很好的防止这一点发生。当然这样的操作是要付费的，需要修改源码api接口，请<a href="https://t.cn/A6AGG52u">自行百度</a>。
   其实市面上有很多网址缩短源码，但都不够简洁，且需要服务器支撑。如果你喜欢极简风格那就来对了！   
   
   </details>

### 特点：
1. 极简风格
1. 将网址转换为`https://t.cn/xxx`类格式
1. 基于cloudflare的强大功能，无需服务器支撑即可建立短网址网页

## 教程：
### 前期准备
1. 一个[cloudflare](http://cloudflare.com)账号
1. 拥有自己的域名，[freenom免费申请>>](http://freenom.com "免费申请>>")；

### 正式部署
#### 一、创建cf（cloudflare）的workers
<details>
<summary> 如何创建cloudflare-workers？</summary>
1.进入 <a href=http://cloudflare.com>cloudflare首页<a> ,点击进入workers
   
![6010332F-D475-4589-9B0A-19975E67C6EB.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/853632551.png)<br>
2.点击创建worker
![429F89D4-6A33-4B0E-9FEB-03F61974214A.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/1774752214.png)
<br>
</details>


#### 二、编辑worker
<details>
<summary> 如何编辑cloudflare-workers？</summary>
在脚本框内填入<a href=https://github.com/Closty/duanwangzhi/blob/master/短网址代码.html>本项目中以html结尾的代码<a> ；打开后将其中的所有代码复制并粘贴填入cf-worker的编辑框中。
  
如图所示

![填入代码](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/2327643990.png)<br>

这时候便可以访问你的worker，只不过域名不是自定义的。不过也可以使用了。地址便是上图代码上侧的地址，如这是我的worker地址。[https://s.clost.workers.dev](https://s.clost.workers.dev "https://s.clost.workers.dev")<br>
</details>


#### 三、绑定域名
<details>
<summary> 如何绑定域名？</summary>
1.你需要先将你的域名指定任意一个IP地址，但是必须开启默认的代理模式（黄色的云朵图标点亮状态）。然后点击保存。
   
![指定任意一个IP地址并开启代理](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/1617973151.png)<br>

2.进入workers界面，添加路由

![3224A31E-4D2E-4E4D-8D75-CC13EE6E5796.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/2818873198.png)<br>
3.添加路由，域名处填写`https://你的域名/*`（注意`/*`两个符号务必加上）,worker选择你刚刚创建的worker

![CA8840DA-3830-42FF-A9C2-FE5937B90A21.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/2887380108.png)<br>
</details>


### 大功告成，访问你的域名试试吧！<br>
如访问[https://s.clost.net](https://s.clost.net "https://s.clost.net")

## 贡献：

[Closty](https://github.com/closty)

以及带添加的人们
