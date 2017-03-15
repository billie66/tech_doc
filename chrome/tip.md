### 问题描述

```
XMLHttpRequest cannot load http://xxx.com/Login. The
value of the 'Access-Control-Allow-Origin' header in the response must not be
the wildcard '*' when the request's credentials mode is 'include'. Origin
'http://localhost:8080' is therefore not allowed access. The credentials mode
of requests initiated by the XMLHttpRequest is controlled by the
withCredentials attribute
```

解决办法，临时禁止 Chrome 浏览器的安全检查机制

```
open -a Google\ Chrome --args --disable-web-security --user-data-dir
```

