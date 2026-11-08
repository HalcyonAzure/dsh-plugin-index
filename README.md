# dsh-plugin-index

我自己的 DSH 插件源：一份 DSH 插件市场索引（format 1），记录我发布或自用的 DSH 插件，供自己在 **插件 → 发现（Discover）** 里浏览和安装。

**索引地址**

```
https://raw.githubusercontent.com/HalcyonAzure/dsh-plugin-index/main/index.json
```

## 收录的插件

| 插件 | 版本 | 说明 | 仓库 |
| --- | --- | --- | --- |
| `dsh-mcp-manager` | 1.1.0 | 左侧栏 MCP 服务器面板：添加、测试、启停、删除 MCP 服务器；支持 stdio 与 streamable HTTP，密钥存入 DSH 凭据库 | [dsh-mcp-manager](https://github.com/HalcyonAzure/dsh-mcp-manager) |
| `dsh-magpie-quota` | 1.1.2 | 会话顶栏显示当前模型对应 Magpie 账号的剩余额度，点击查看全部账号 | [dsh-magpie-quota](https://github.com/HalcyonAzure/dsh-magpie-quota) |

## 在 DSH 里使用

1. 启用插件市场 bundle（只需一次）：设置 → 插件 → 官方插件里启用 **Experimental custom plugin indexes**（`@deepseek-ai/dsh-experimental-plugin-market-bundle`）。启用后「插件」页多出 **发现 / Discover** 标签页。
2. 在 Discover 里 **Manage index sources…** → **Add index source**，把上面的索引地址填进 **Index URL**。
3. 索引里的插件会带着图标、说明和版本列表出现在 Discover；安装仍走 `plugin_manager` 的安装流程。

> 如果只想装某一个插件，也可以跳过索引：插件 → 添加插件 → 直接填插件仓库地址（例如 `https://github.com/HalcyonAzure/dsh-mcp-manager`）。

## 这份索引怎么维护

编辑 `index.json` 即可，DSH 每次读取时用内置的 `@deepseek-ai/dsh-plugin-market-index` 校验；格式错误会在 Discover 的源条目上直接显示 JSON 路径和原因。

约定：

- `format` 固定为 `1`，`title` / `description` 是 `{ "en": ..., "zh": ... }` 本地化文本（必须含 `en`）。
- 每个插件一项：`name` 必须等于包的 `name`，`versions` 至少一项。
- 每个版本用 **git 源 + 40 位 commit** 固定：`{"type":"git","url":"https://github.com/<owner>/<repo>","commit":"<sha>"}`，插件在仓库根目录，不需要 `path`。这样不会因为分支移动而改变内容。
- `icon` 用 pin 到 commit 的 `raw.githubusercontent.com` 地址；格式也接受 `data:` 内联图片（≤32 KiB）。
- `publishTimestamp` 是 Unix 秒，用该版本提交时间；`metadata.category` / `labels` 必须引用文件顶部 `metadata` 里声明过的 id。
- 发新版本时：在插件仓库提交并打 tag → 把这里的 `versions` 增加一项（新版本在前不必手动排序，校验器按 SemVer 排序）。

字段完整定义见 DSH 包 `@deepseek-ai/dsh-plugin-market-index` 的 README 与校验器源码。

## English

A personal DSH plugin-market index (format 1) listing my own DSH plugins. Enable the *Experimental custom plugin indexes* bundle, then add this index URL under **Plugins → Discover → Manage index sources…**; installs stay commit-pinned.

## License

MIT © [HalcyonAzure](https://github.com/HalcyonAzure)
