## 演示网址：
[s.clost.net](https://s.clost.net "s.clost.net")

## 介绍：
首先什么叫短网址呢？他有什么用处呢？短网址是指将任何域名更换成一个t.cn/xxxx类的网址。
比如将网址[https://www.clost.net](https://www.clost.net "www.clost.net")转化成[http://t.cn/A6wT0J1d](http://t.cn/A6wT0J1d "http://t.cn/A6wT0J1d")

   <details>
   <summary> 那么为什么要转换呢？</summary>
   简洁的说可以防红，比如你在你的qq分享你的网站，分享过多很可能会被显示已被拦截等字样，别人以后就只能复制到你的网                   
   址在浏览器打开而不能直接在qq内点开。用短网址就可以很好的防止这一点发生。
   其实市面上有很多网址缩短源码，但都不够简洁，且需要服务器支撑。如果你喜欢极简风格那就来对了！   
   
   </details>

### 特点：
1. 极简风格
1. 将网址转换为t.cn/xxx类格式
1. 基于cloudflare的强大功能，无需服务器支撑即可建立短网址网页

## 教程：
### 前期准备
1. 一个[cloudflare](http://cloudflare.com "cloudflare")账号
1. 拥有自己的域名，[免费申请>>](http://freenom.com "免费申请>>")；也可以不需要域名，但无法定义自己的网址

### 正式部署
#### 一、创建cf的workers
1.进入[cloudflare](http://cloudflare.com "cloudflare")首页,点击进入workers
![6010332F-D475-4589-9B0A-19975E67C6EB.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/853632551.png)
2.点击创建worker
![429F89D4-6A33-4B0E-9FEB-03F61974214A.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/1774752214.png)
#### 二、编辑worker

在脚本框内填入以下代码后，点击保存点击部署。
   <details>
   <summary> 代码已折叠，点击本处展示</summary>
   
     addEventListener('fetch', (event) => {
      return event.respondWith(handleRequest(event.request));
    })

    const handleRequest = async (request) => {
      const render = (body) => {
        return new Response(`
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>T.CN 短网址</title>

    <style media="screen">
      body { background: #ECEFF1; color: rgba(0,0,0,0.87); font-family: Roboto, Helvetica, Arial, sans-serif; margin: 0; padding: 0; }
      #message { background: white; max-width: 360px; margin: 100px auto 16px; padding: 32px 24px; border-radius: 3px; }
      #message h2 {  color: rgba(0,0,0,0.6); font-weight: bold; font-size: 14px; margin: 0 0 8px; }
      #message h1 { color: #ffa100;  font-size: 30px; font-weight: 300;  margin: 0 0 16px;}
      #message p { line-height: 140%; margin: 16px 0 24px; font-size: 14px; }
      #message a { display: block; text-align: center; background: #039be5; text-decoration: none; color: white; padding: 16px; border-radius: 4px; }
      #message, #message a { box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24); }
      #load { color: rgba(0,0,0,0.4); text-align: center; font-size: 13px; }
      @media (max-width: 600px) {
        body, #message { margin-top: 0; background: white; box-shadow: none; }
        body { border-top: 16px solid #ffa100; }
      }
    </style>
  </head>
  <body>
${body}

</body>
</html>`.trim(), {
          status: 200,
          headers: {
            'Content-Type': 'text/html; charset=utf-8'
          }
        });
      }
      request = new URL(request.url);
      if (request.pathname !== '/') return new Response(null, { status: 404 });
      if (request.searchParams.has('url')) {
        const url = request.searchParams.get('url');
        const response = await fetch(`http://service.weibo.com/share/share.php?url=${encodeURIComponent(url)}&title=1`);
        const html = await response.text();
        const short = html.match(/http:\/\/t.cn\/\w+/i);
        const refer = html.match(/\$refer\s+: "(.+?)"/i);
        if (short && refer) {
          return render(`
          <div id="message" align="center">
         
            <center><h1>缩短结果：</h1>
            <a id="copy" onClick="copyUrl2()">${short[0]}</a>

<script>

function copyUrl2(){

    var Url2=document.getElementById("copy").innerText;
var oInput = document.createElement('input');
oInput.value = Url2;
document.body.appendChild(oInput);
oInput.select(); // 选择对象
document.execCommand("Copy"); // 执行浏览器复制命令
oInput.className = 'oInput';
oInput.style.display='none';
alert('复制成功');
    }
</script>
            <center><h1>原始网址：</h1><a href="${refer[1]}">${refer[1]}</a></center>
            <p></p>
            <a href="/">返回</a>
            </div>
          `);
        }
        return render(`
        <div id="message" align="center">
        <center><h1>请求失败</h1></center>
        </div>
        `);
      }
      return render(`
      <div id="message" align="center">
      <center><h1>T.CN 短网址</h1></center>
   <p></p>
        <form method="GET">
        <input name="url"  placeholder="http(s)://XXX.XXX"/>
        <br><br><button type="submit">一键压缩</button>
        </form>
        </div>
      `);
    }
   
   </details>
  
如图所示
![填入代码](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/2327643990.png)

这时候便可以访问你的worker，只不过域名不是自定义的。不过也可以使用了。地址便是上图代码上侧的地址，如这是我的worker地址。
[https://s.clost.workers.dev](https://s.clost.workers.dev "https://s.clost.workers.dev")

#### 三、绑定域名
1.你需要先将你的域名指定任意一个IP地址，但是必须开启默认的代理模式（黄色的云朵图标点亮状态）。然后点击保存。
![指定任意一个IP地址并开启代理](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/1617973151.png)

2.进入workers界面，添加路由
![3224A31E-4D2E-4E4D-8D75-CC13EE6E5796.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/2818873198.png)
3.添加路由，域名处填写`https://你的域名/*`（注意`/*`两个符号务必加上）,worker选择你刚刚创建的worker
![CA8840DA-3830-42FF-A9C2-FE5937B90A21.png](https://cdn.jsdelivr.net/gh/closty/tuchuang/usr/uploads/2020/04/2887380108.png)
###大功告成，访问你的域名试试吧！
如访问[https://s.clost.net](https://s.clost.net "https://s.clost.net")
