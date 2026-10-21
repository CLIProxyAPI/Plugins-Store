# Plugins Store

由 `CLIProxyAPI` 组织维护的自建插件商店源，仓库为 `CLIProxyAPI/Plugins-Store`。

> 首次发布准备中。安装包与校验文件发布完成后，再启用商店索引。

## 安装

发布完成后，在 CPA 的插件商店源管理中添加：

```text
https://raw.githubusercontent.com/CLIProxyAPI/Plugins-Store/main/registry.json
```

或合并到配置：

```yaml
plugins:
  store-sources:
    - https://raw.githubusercontent.com/CLIProxyAPI/Plugins-Store/main/registry.json
```

需要支持 schema 2 direct 源和 schema 6 插件的 CPA；本地验证使用 CPA 7.3.7。选择插件安装，按宿主提示重启，再从管理菜单进入「账号设置」。

## 收录插件

| ID | 名称 | 版本 | 平台 |
| --- | --- | --- | --- |
| `cpa-codex-controls` | Codex 账号设置 | `1.4.2-timezone.14` | Linux amd64 / arm64，macOS arm64 |

- 按上游账号限制并发，默认 0：不限制、不排队；正数上限支持等待队列。
- Codex 请求时区与位置覆盖，默认关闭，账号设置优先于全局；可检测代理出口位置自动填充。
- 保留错误事件、插件日志。当前管理页面仅显示 Codex 账号。

`CPA Policy` 是讨论中的后续名称；本批已验证资源仍使用上述插件 ID。未改名，也未包含多供应商扩展、违禁内容检测或请求隐私过滤。

## 发布维护

索引采用 `schema_version: 2`，直接下载明确版本的 Release 资源。`registry.json` 中的 SHA256 和字节数均已对照本地文件核对。

准备的 Release 标签为 `v1.4.2-timezone.14`，上传三个平台 ZIP、源码 ZIP 和 `checksums.txt`。先确认所有资源可下载，再公开索引；不要提交大体积安装包到 Git 历史。更新版本须同步版本、资源地址、大小和 SHA256。

这批动态库内的仓库元数据仍是构建时的占位地址；安装来源由此商店的真实资源 URL 决定。源码和包内旧说明是该构建的历史材料，后续重新构建时再注入真实仓库地址。

## 归属与许可证

插件基于 Hao Wang 的 `haowang02/cpa-plugin-key-billing` 二次开发；时区匹配与位置对齐设计参考 `zyycn/codex-proxy-rs`。原作者 MIT 许可证、Apache-2.0 适配说明和其他许可证见 `LICENSE`、`NOTICE`、`licenses/`，Release 源码包及平台包也保留相关材料。
