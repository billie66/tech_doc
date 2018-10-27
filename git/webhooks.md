- 创建一个 hook

接口定义：

```
POST /repos/:owner/:repo/hooks
```

curl 命令：

```
curl -u "your_username" -d "@data.json" -X POST
https://api.github.com/repos/xxx/xxx/hooks
```

data.json 文件内容：

```
{
  "name": "web",
  "active": true,
  "events": ["push"],
  "config": {
    "url": "http://example.com",
    "content_type": "json"
  }
}
```

- 列出所有的 hooks

接口定义：

```
GET /repos/:owner/:repo/hooks
```

curl 命令：

```
curl -u "your_username" -i
https://api.github.com/repos/xxx/xxx/hooks
```

- 删除一个 hook

接口定义：

```
DELETE /repos/:owner/:repo/hooks/:hook_id
```

curl 命令：

```
curl -u "your_username" -X DELETE
https://api.github.com/repos/xxx/xxx/hooks/xxx
```

### 参考

https://developer.github.com/webhooks/

