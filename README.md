# 善治插件目录

供小智办公和 DeepSeek Harness 的「插件 → 发现」页面读取的独立插件索引仓库。索引采用官方插件市场格式 1，可同时收录第三方插件与善治自研插件。

## 配置索引源

在「插件」页面的实验性插件中启用「自定义插件索引」，进入「发现 → 添加索引源」，填入以下 GitHub Pages 地址。已于2026-11-12在客户端所在电脑上通过无代理 Node 请求和官方格式校验，并确认返回已登记的插件：

```text
https://shanzhi-digital.github.io/shanzhi-plugin-index/index.json
```

Pages 从本仓库 `main` 根目录静态发布，不需要另购服务器。每次更新后应等待 Pages 构建完成并核对返回内容。备用 CDN 地址可能保留较长时间的分支缓存：

```text
https://fastly.jsdelivr.net/gh/shanzhi-digital/shanzhi-plugin-index@main/index.json
```

另一个 CDN 地址：

```text
https://gcore.jsdelivr.net/gh/shanzhi-digital/shanzhi-plugin-index@main/index.json
```

GitHub 原始地址仍可使用，但需要当前网络能够访问 `raw.githubusercontent.com`：

```text
https://raw.githubusercontent.com/shanzhi-digital/shanzhi-plugin-index/main/index.json
```

上述地址读取同一仓库的公开静态 JSON，不需要 GitHub 登录，但缓存可能返回不同时间的版本。网页仓库地址不能代替索引文件地址。索引由 Host 进程读取，浏览器能够访问 GitHub 不代表 Host 的网络和代理也可用。此仓库不自动改变现有客户端配置，小智分发的首次默认配置单独维护。

如果原始地址显示「无法读取此索引」，或 CDN 一直显示旧的空目录，在「发现 → 管理索引源」移除该地址，添加上面的 Pages 地址，再刷新。2026-11-12的本机复测中，GitHub 原始地址返回 `ECONNRESET`；CDN 虽返回200但仍缓存空目录，Pages 地址直接返回200且包含图表插件。

## 当前内容

已按2026-11-16的 Gitee 源码仓库快照 `3812bef12ef4977a1dff74c68c51b0f306810000` 同步全部4个可安装组合包（提交时间为 `2026-11-16T15:44:43+08:00`）：

| 插件 | 包名 | 版本 | 状态 |
|---|---|---|---|
| 通用查询结果图表 | `@local/datahub-echarts` | `0.10.2` | 默认表格、多结果标签、图表切换、CSV/XLSX 导出、整轮进一步分析 |
| 问知文档 | `@local/datahub-knowledge-docs` | `0.3.0` | 文件列表、检索来源与证据、授权原文右侧预览 |
| 问数增强 | `@local/datahub-query-enhance` | `0.1.1` | 公共技能读取指引、中文列别名、数据洞察与指标可信状态 |
| 公文全流程处理专家 | `gongwen-skill` | `2.15.0-local.3` | Jose AI 开源插件的善治适配版；公文检查、修复、生成及版式处理 |
| 履约无忧 | `@local/contract-sure` | `0.3.1` | 浏览器授权连接履约系统账户；合同识别核对卡、三流流水对账、履约看板与原件预览；内置 5 个 skill |
| 销售管理 | `@local/salesforge` | `0.3.1` | 浏览器授权连接 SalesForge 销售管理系统账户；查询和维护客户、渠道、项目、日报周报和销售目标，删除和移交负责人先由用户在卡片上确认，写日报只改错别字；内置 6 个 skill |

全部18个版本的安装来源均为 `https://gitee.com/groundhogtang/shanzhi-plugin.git`，固定到对应源码版本的完整提交和插件子目录。上表问知文档、问数增强和公文三项的版本使用上述快照；履约无忧当前版本 `0.3.1` 于2026-11-25登记，固定到提交 `3e42acdbc2b692f4cba36c747ae7e5dd962cde79`（提交时间 `2026-11-24T22:28:01-08:00`）；销售管理当前版本 `0.3.1` 和通用查询结果图表当前版本 `0.10.2` 于2026-11-25登记，固定到同一提交 `2198ed52818d57ed499630516fd641cabfd92d09`（提交时间 `2026-11-25T00:33:23-08:00`）。履约无忧和销售管理分别需要履约系统、销售管理系统先升级到支持插件授权的版本（销售管理从 `0.3.0` 起还要销售管理系统允许插件维护业务数据，已于同日部署），履约无忧历史版本 `0.3.0`、`0.2.1`、`0.2.0` 与销售管理历史版本 `0.3.0`、`0.2.0`、`0.1.0` 保留原提交；图表历史版本 `0.10.1`、`0.10.0`、`0.7.0` 与问知历史版本 `0.2.0` 保留原提交。原包未声明 `engines.dsh`，索引保留空要求，不把包的 peer 依赖误作宿主兼容承诺。时间字段使用已核实源码提交的时间，不表示已向 npm 发布。

登记 `0.10.1` 时的图表源码包含表头和数据居中修复及 README 更新，但包版本未提高，因此该版本对应的源码快照发生变化，已安装版本不会自动升级。后续代码更新须提高包版本后再登记。

118项通过、2项因缺少对应宿主集成环境跳过，是上一轮 `47c8446` 源码快照的专项测试记录，不代表本次快照已通过这些测试；本轮验证结果详见[同步记录](SYNC.md)。所有条目仍为公开来源、仅登记（`listing-only`）：尚未验证宿主安装与兼容性，也未进行生产 MCP 访问、Python 公文处理或 CSV/XLSX 导出全链路验收。图标直接使用对应源码的原图形，在本索引站点的 `icons` 目录同源托管。

更新 `main` 后，用户在「发现」页刷新即可读取新条目；索引不会自动更新本机已安装版本。Host 和 CDN 均有独立缓存，发布后需核对实际读取内容。插件详情由宿主从 Gitee 源码读取，若源码读取失败，详情可能单独报网络错误，不代表索引同步失败。

## 仓库分工

- [`index.json`](index.json)：客户端实际读取的目录，维护插件资料、精确版本、兼容范围和安装来源。
- [`CONTRIBUTING.md`](CONTRIBUTING.md)：插件收录、版本维护和发布校验约定。
- [shanzhi-plugin](https://gitee.com/groundhogtang/shanzhi-plugin)：公开插件源码库，提供详情与固定提交的安装来源。本仓库只引用版本和路径，不复制源码。

收录公开第三方插件时，通常引用作者的 npm 包或固定 Git 提交即可，不需要复制代码。私有源码的安装仍要求用户拥有相应凭据；公开索引本身不会授予私有仓库访问权限，索引中不得包含令牌或密码。

## 格式与限制

本索引基于 DeepSeek Harness `0.2.2-rc.1` 的格式 1 校验器初始化。发布前按[维护约定](CONTRIBUTING.md)校验当前格式与真实安装来源。

发现页可浏览、筛选、查看详情和确认安装。当前官方市场界面的版本更新只显示状态，升级通常需要卸载后重新安装。插件许可与使用要求由各插件作者维护，本目录的收录不改变其许可证。

参考：[官方发现页](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/client/ui-plugin-market/README.zh.md)、[官方索引格式](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/util/plugin-market-index/README.zh.md)。
