### 新建注释 tag 标签

```
git tag -a v1.0 04a8c75 -m 'my version v1.0'
```

### push 到远端 git 服务器

push 单个 tag
```
git push origin v1.0
```

一次 push 所有的 tag
```
git push origin --tags
```

### 本地删除 tag

```
git tag -d v1.0
```

### 远端删除

```
git push --delete origin v1.0
```

