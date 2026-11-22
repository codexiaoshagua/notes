# `node:sqlite` 的版本门槛

Node 22 加了内置的 `node:sqlite`，但早期版本要加实验标志才能用。

## 结论

**v22.13.0 起**不需要 `--experimental-sqlite`。

早期版本会报：

```
Error: Cannot find module 'node:sqlite'
```

或者要求你加 flag。

## 检查版本

```bash
node -p "process.versions.node"
```

## 一个旁证

`pdfjs-dist` 自己的 `package.json` 里写着：

```json
"engines": { "node": ">=22.13.0 || >=24" }
```

说明 22.13 这个门槛不是我猜的，是生态里的实际约束。

## 一句话

**要用 `node:sqlite`，就把 engines 写成 `>=22.13.0`。**
