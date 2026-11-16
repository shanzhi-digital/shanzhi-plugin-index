# 插件同步记录

同步日期：2026-11-16。源码仓库 [shanzhi-plugin](https://github.com/shanzhi-digital/shanzhi-plugin) 的固定快照为 `47c8446a2f910a9edb55f96ebf687b1d534a59b3`。逐一核对全部4个 `plugins/*/package.json`、组合配置、入口和公开资料，索引更新为4个插件、7个固定版本。

## 版本来源

| 插件 | 版本 | 固定提交 | 插件路径 |
|---|---|---|---|
| 通用查询结果图表 | `0.10.1` | `47c8446a2f910a9edb55f96ebf687b1d534a59b3` | `plugins/datahub-echarts` |
| 通用查询结果图表 | `0.10.0` | `a60434dbbf2ccfc2e0557bbf2e3559eb9f75cd64` | `plugins/datahub-echarts` |
| 通用查询结果图表 | `0.7.0` | `d518a11df256cf6062acbd42cb2cad4d7f363daf` | `plugins/datahub-echarts` |
| 问知文档 | `0.3.0` | `5141b1486fa1d3493d5083eea96304b24789a9c3` | `plugins/datahub-knowledge-docs` |
| 问知文档 | `0.2.0` | `dc0f6d1bf549da82c695fbd138688b809507ca08` | `plugins/datahub-knowledge-docs` |
| 问数增强 | `0.1.1` | `95200f5ac4996c54d76ba4640ecd6d86fb4acfbc` | `plugins/datahub-query-enhance` |
| 公文全流程处理专家 | `2.15.0-local.3` | `2fa149ae8b92b909ae67d41138e8555e1cf28fc2` | `plugins/gongwen` |

`publishTimestamp` 采用对应提交的 GitHub committer 时间，以秒记录。已保留原图表 `0.7.0` 条目，并新增从提交核实的其他版本；未将后续提交冒充历史版本的原始发布时间。

公文插件作者保留为 Jose AI，标为「善治适配」，与三项善治自研插件区分。它仍需 Python 3.10+、python-docx、pydantic、PyYAML 等依赖；索引登记不自动安装这些依赖。三个图标来自同一固定快照中对应插件的 `icon.svg`，遵循源码仓库 MIT 许可；版权见源码插件各自 LICENSE。

## 已运行的检查

- 官方格式1校验器验证完整索引，按 SemVer 排序并核对每个版本生成的固定 Git 安装参数。
- 核对每个登记版本实际的包名、版本、`dsh.bundle.patch`、组合行和运行入口；最新4项与固定源码快照的清单一致。
- 图表源码测试：`core.test.js`、`results.test.js`、`build/event-projection.test.js`，28项通过。
- 问知文档源码测试：`results.test.js`、`event-projection.test.js`、`host-bridge.test.js`、`original-preview.test.js`，52项通过。
- 问数增强源码测试：`trust.test.js`、`host-bridge.test.js`、`event-projection.test.js`，30项通过、2项跳过；跳过项需要指定 `DSH_APP_ASAR` 对应宿主归档。
- 公文 DSH 桥接测试：`dsh/index.test.js`，8项通过，测试使用模拟工具和子进程，不会处理真实业务文档。

上述源码测试合计118项通过、2项跳过。没有进行完整宿主安装、真实 MCP 查询、Python 公文处理、浏览器交互或 CSV/XLSX 导出全链路验证，因此全部条目继续保留「仅登记」。

## 文档差异与发布

图表最新包清单为 `0.10.1`，其插件 README 开头仍写 `0.10.0`；根 README 的插件清单也未列出问知文档和公文。此次以真实包清单和固定源码为准，只同步索引及其说明，不覆盖同事源码或修改业务行为。

发布入口保持为 <https://shanzhi-digital.github.io/shanzhi-plugin-index/index.json>。推送后等待 Pages 发布并检查实际 JSON 和同源图标；Host 中已有列表可能缓存10分钟，可在「发现」页刷新。旧 jsDelivr 分支地址可能保留旧内容，不以它作为本次发布验收入口。插件详情的 GitHub 原始文件网络可达性与索引发布独立。
