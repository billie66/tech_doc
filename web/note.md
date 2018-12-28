### 静态网站配置 Nginx

找不到的页面，显示自己设计的页面内容，而不是 Nginx 默认的 404 页面样式

```
server {
  listen 80;
  server_name your_domain_name;
  root   /your_file_path;
  location / {
    try_files $uri $uri/ /404.html;
  }
}
```

$uri 加载存在的文件，$uri/ 加载存在的目录，不存在的文件则加载 /404.html 页面，响应 200 状态码

### 配置 Nginx, 在 URL 末尾添加斜杆

用 react-static 部署的静态网站, Nginx 的配置如上所示。在苹果手机微信中访问的 URL 末尾有或没有斜杆，返回结果不一样

```
https://haoqicat.com/ce
https://haoqicat.com/ce/
```

第一个链接显示 404 页面，第二个链接显示正常的页面。访问的结果不同，是因为 react-static 编译后的静态文件中不存在文件名为 `ce` 的文件，而存在 `ce/` 目录并且 `ce/` 目录中有个 `index.html` 文件。

如何让末尾没有斜杆的 URL 也能获取到正确的内容呢？可以通过页面重定向实现，配置 Nginx 如下:

```
server {
  listen 80;
  server_name xxx.haoqicat.com;
  root /home/peter/sites/xxx/dist/;
  location ~ ^([^.\?]*[^/])$ {
     try_files $uri @addslash;
  }
  location @addslash {
     return 301 $uri/;
  }
  location / {
    try_files $uri $uri/ /404.html;
  }
}
```

[参考文档](https://www.ateamsystems.com/tech-blog/nginx-add-trailing-slash-with-301-redirect-without-if-statements/)
