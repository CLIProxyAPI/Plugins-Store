# Plugins Store

由 `CLIProxyAPI` 组织维护的自建插件商店源，仓库为 `CLIProxyAPI/Plugins-Store`。

本仓库只维护商店索引。插件源码和安装包在 [CLIProxyAPI/cpa-policy](https://github.com/CLIProxyAPI/cpa-policy)，安装包发布在该仓库的 [Releases](https://github.com/CLIProxyAPI/cpa-policy/releases)。

## 安装

在 CPA 的插件商店源管理中添加：

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

完整配置示例见 [config.example.yaml](config.example.yaml)。建议将 `plugins.configs.cpa-codex-controls.priority` 设为 `-100`，让本插件在优先级大于 -100 的其他插件之后执行同阶段的请求处理。该设置由 CPA 保存，商店安装或更新不会自动设置它；它也不能控制其他插件的独立 HTTP 请求、页面时区或后续处理阶段。

## 收录插件

| ID | 名称 | 版本 | 平台 |
| --- | --- | --- | --- |
| `cpa-codex-controls` | CPA Policy | `1.4.4` | Linux amd64 / arm64，macOS arm64 |

- 按上游账号限制并发，默认 0：不限制、不排队；正数上限支持等待队列。
- Codex 请求时区与位置覆盖，默认关闭，账号设置优先于全局；可检测代理出口位置自动填充。
- 风控中心支持关键词/正则与 Moderations 兼容 API，提供仅观察、前置拦截、账号单独策略、草稿测试和独立审核记录；默认关闭、默认不保存文本摘要。
- 认证文件与 AI 供应商显示全部受支持类型，提供原生请求健康度、当前并发/上限及供应商启停。
- 保留错误事件与插件日志。

插件项目名称为 **CPA Policy**，当前安装包仍使用 `cpa-codex-controls` ID，管理菜单显示「账号设置」。并发策略适用于受支持的各类上游账号；内容审计覆盖 Codex/Responses、OpenAI Chat Completions、Anthropic Messages 和 Gemini/Vertex 用户文本。时区覆盖仅改写支持的结构化时区与位置字段。请求正文隐私替换、图片/音频审核、自动封禁和通知尚未加入。

## 从旧版更新

刷新本插件源，确认 CPA Policy 显示 `1.4.4`，安装更新后重启 CPA。插件 ID 保持不变，已有账号并发、时区与诊断配置继续使用。新增内容审计默认关闭，配置规则或审核 API 后再开启。

## 发布维护

索引采用 `schema_version: 2`，直接下载明确版本的 Release 资源。`registry.json` 中的 SHA256 和字节数均已对照本地文件核对。

安装资源在 `CLIProxyAPI/cpa-policy` 的 `v1.4.4` Release，商店引用已校验的 Linux amd64/arm64 与 macOS arm64 ZIP，并提供源码 ZIP 和 `checksums.txt`。先确认所有资源可下载，再更新此仓库的索引。更新版本须同步版本、资源地址、大小和 SHA256。

Release 动态库已注入 `CLIProxyAPI/cpa-policy` 仓库信息；实际安装来源由商店资源 URL 决定。平台包保留安装说明、内容审计文档及许可证。

## 归属与许可证

插件基于 Hao Wang 的 `haowang02/cpa-plugin-key-billing` 二次开发；时区匹配与位置对齐设计参考 `zyycn/codex-proxy-rs`。原作者 MIT 许可证、Apache-2.0 适配说明和其他许可证见 `LICENSE`、`NOTICE`、`licenses/`，Release 源码包及平台包也保留相关材料。
