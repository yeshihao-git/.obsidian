#tools
# github 历史版本回退
```bash
git reset --hard <commit id>
git push -f
```

# .gitignore 中写入忽略 已跟踪文件 规则失效问题

在文件已被跟踪的情况下，在 .gitignore 中写入忽略规则是无效的，正确操作如下
1. 取消文件跟踪
```bash
git rm -r --cached <文件夹> # 若是文件不需要 -r
```

2. 在 .gitignore 中写入忽略规则
```bash
# .gitignore
<文件>
<文件夹>/
```

3. git commit