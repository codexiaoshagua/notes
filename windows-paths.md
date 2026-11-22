# Git Bash 在 Windows 上的路径陷阱

## 1. 给原生程序要用正斜杠

Git Bash 里 `/c/Users/x` 是给 bash 自己看的。传给 `git`、`node`、`python` 这种原生程序会变成怪路径。

```bash
# 错
node /c/Users/x/a.js

# 对
node "C:/Users/x/a.js"
```

## 2. `/x` 开头的参数会被当成路径

MSYS 会自动转换。要原样传：

```bash
MSYS2_ARG_CONV_EXCL='*' 程序 /some/flag
```

## 3. `tar` 把 `C:/` 当远程主机

```bash
# 报错：Cannot connect to C:
tar -xf C:/a.tar

# 对
tar --force-local -xf C:/a.tar
```

## 4. 环境变量不要用 POSIX 路径

```bash
# 错（程序会读到空目录）
export APP_ROOT=/d/project

# 对
export APP_ROOT="D:/project"
```

Windows 会把 `/d/project` 解析成 `D:\d\project`。
