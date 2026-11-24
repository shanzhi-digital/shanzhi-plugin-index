# 插件同步记录

## 2026-11-24：登记履约无忧 0.2.0

新增 `@local/contract-sure` `0.2.0`，安装来源固定到 Gitee `wzx/contract-sure` 分支上的提交 `1fb95aaaef785bc6fcf1c193159190b7cdf43980`，路径 `plugins/contract-sure`。`publishTimestamp` 为该提交的 committer 时间 `2026-11-24T05:56:09-08:00`（Unix 秒 `1795528569`）。此前本地准备过的 `0.1.0` 登记从未推送，也不再登记：旧版在插件里收账号密码换令牌，且有工具输出导致调用失败的问题。

这个版本改为浏览器授权连接履约系统账户，需要履约系统升级到支持插件授权的版本；履约系统未升级时，插件会提示联系管理员。

### 本次实际验证

- 使用 DeepSeek Harness `0.2.2-rc.5` 所带官方 `parseMarketIndex` 校验完整索引（5个插件、8个版本），通过；`marketInstallTarget` 生成的安装参数为 `git+https://gitee.com/groundhogtang/shanzhi-plugin.git#1fb95aaaef785bc6fcf1c193159190b7cdf43980&path:/plugins/contract-sure`。
- 在禁用 Git 凭据助手、全局/系统 Git 配置和代理的临时环境中，从 Gitee 匿名拉取该提交，核对包名、版本 `0.2.0`、`dsh.bundle.patch` 和 README 可读。
- 插件源码测试 79 项通过。
- 在本机 DeepSeek Harness `0.2.2-rc.5` 桌面端用同一份源码打包安装，连接本机启动的新版履约系统，走通浏览器授权并由插件以新令牌调用履约系统。多账户切换、断开吊销只在插件单元测试和后端接口脚本中验证。

未验证：从「发现」页经 Gitee 安装，以及连接线上履约系统（线上尚未部署插件授权版本）。因此条目保留「公开来源、仅登记」，`engines` 保持空要求。

## 2026-11-16：迁移 Gitee 安装来源

源码及安装仓库切换到 [shanzhi-plugin](https://gitee.com/groundhogtang/shanzhi-plugin)。索引仍为4个插件、7个固定版本，发布入口和同源图标保持在现有 GitHub Pages。4个当前版本固定到已核实的 Gitee 快照 `3812bef12ef4977a1dff74c68c51b0f306810000`，其 Git committer 时间为 `2026-11-16T15:44:43+08:00`，Unix 秒为 `1794815083`。

### 当前版本来源

全部版本的安装仓库均为 `https://gitee.com/groundhogtang/shanzhi-plugin.git`。

| 插件 | 版本 | 固定提交 | 插件路径 |
|---|---|---|---|
| 通用查询结果图表 | `0.10.1` | `3812bef12ef4977a1dff74c68c51b0f306810000` | `plugins/datahub-echarts` |
| 通用查询结果图表 | `0.10.0` | `a60434dbbf2ccfc2e0557bbf2e3559eb9f75cd64` | `plugins/datahub-echarts` |
| 通用查询结果图表 | `0.7.0` | `d518a11df256cf6062acbd42cb2cad4d7f363daf` | `plugins/datahub-echarts` |
| 问知文档 | `0.3.0` | `3812bef12ef4977a1dff74c68c51b0f306810000` | `plugins/datahub-knowledge-docs` |
| 问知文档 | `0.2.0` | `dc0f6d1bf549da82c695fbd138688b809507ca08` | `plugins/datahub-knowledge-docs` |
| 问数增强 | `0.1.1` | `3812bef12ef4977a1dff74c68c51b0f306810000` | `plugins/datahub-query-enhance` |
| 公文全流程处理专家 | `2.15.0-local.3` | `3812bef12ef4977a1dff74c68c51b0f306810000` | `plugins/gongwen` |

此次按维护者确认，4个当前版本沿用源码包清单版本号，但更换为更新的源码快照；其中包含图表表头和数据居中修复及插件说明更新。它们的 `publishTimestamp` 改为当前快照的提交时间，表示此次登记的源码快照时间，不表示首次版本发布或 npm 发布时间。3个历史版本的提交和时间保持不变。此为同版本重新固定来源的例外；后续代码发布应提高插件版本号并新增索引版本。已安装用户不会自动更新，且不能仅靠版本号识别此次变化。

### 本次实际验证

- 使用本机 DeepSeek Harness `0.2.2-rc.1` 所带官方 `parseMarketIndex` 校验完整索引，通过；通过 `marketInstallTarget` 核对全部7个固定 Git 安装参数，仓库、提交和 `path:` 子目录均匹配。
- 在禁用 Git 凭据助手、全局/系统 Git 配置和代理的临时环境中，从 Gitee 成功匿名克隆完整仓库。
- 从该 Gitee 克隆逐项读取7个版本的 `package.json`，核对包名、版本、`dsh.bundle.patch` 指向的组合配置和运行入口文件；4个当前版本的 README 文件均可从固定提交读取。
- 核对4个当前版本的提交时间为 `1794815083`；3个历史版本的提交和时间与迁移前索引一致。
- 核对分类、标签及本地图标路径；`git diff --check` 通过。

本次未运行插件源码测试、未执行宿主安装与启用，也未验证宿主详情界面的实际读取、生产 MCP、Python 公文处理或 CSV/XLSX 导出。因此全部条目继续保留「公开来源、仅登记」，兼容性要求沿用原包声明。下方118项通过、2项跳过属于上一轮快照的历史记录，不代表当前 Gitee 快照的测试结果。

### 发布边界

发布入口保持为 <https://shanzhi-digital.github.io/shanzhi-plugin-index/index.json>。本轮验证覆盖索引及 Gitee 来源；Pages 发布验收需在推送后完成。发布后需要等待 Pages 更新，核对线上 JSON、同源图标和宿主发现列表。Host 及 CDN 有独立缓存，旧 jsDelivr 分支地址可能保留旧内容。用户仍需能够访问索引站点；插件安装和源码详情改从 Gitee 读取，具体网络及宿主行为以实际安装验证为准。

## 上一轮同步记录：GitHub 快照 `47c8446`

同步日期：2026-11-16。当时源码仓库为 GitHub 的 `shanzhi-digital/shanzhi-plugin`，核对快照为 `47c8446a2f910a9edb55f96ebf687b1d534a59b3`。逐一核对全部4个 `plugins/*/package.json`、组合配置、入口和公开资料，登记4个插件、7个固定版本。

当时4个当前版本的来源提交分别为：图表 `0.10.1` 对应 `47c8446a2f910a9edb55f96ebf687b1d534a59b3`，问知 `0.3.0` 对应 `5141b1486fa1d3493d5083eea96304b24789a9c3`，问数增强 `0.1.1` 对应 `95200f5ac4996c54d76ba4640ecd6d86fb4acfbc`，公文 `2.15.0-local.3` 对应 `2fa149ae8b92b909ae67d41138e8555e1cf28fc2`。时间使用当时对应提交的 Git committer 时间。

公文插件作者保留为 Jose AI，标为「善治适配」，与三项善治自研插件区分。它仍需 Python 3.10+、python-docx、pydantic、PyYAML 等依赖；索引登记不自动安装这些依赖。三个图标来自 `47c8446` 快照中对应插件的 `icon.svg`，遵循源码仓库 MIT 许可；版权见源码插件各自 LICENSE。本次迁移沿用这些图标。

### 历史检查与测试结果

- 官方格式1校验器验证完整索引，按 SemVer 排序并核对每个版本生成的固定 Git 安装参数。
- 核对每个登记版本实际的包名、版本、`dsh.bundle.patch`、组合行和运行入口。
- 图表源码测试：`core.test.js`、`results.test.js`、`build/event-projection.test.js`，28项通过。
- 问知文档源码测试：`results.test.js`、`event-projection.test.js`、`host-bridge.test.js`、`original-preview.test.js`，52项通过。
- 问数增强源码测试：`trust.test.js`、`host-bridge.test.js`、`event-projection.test.js`，30项通过、2项跳过；跳过项需要指定 `DSH_APP_ASAR` 对应宿主归档。
- 公文 DSH 桥接测试：`dsh/index.test.js`，8项通过，测试使用模拟工具和子进程，不会处理真实业务文档。

上述历史源码测试合计118项通过、2项跳过。当时没有进行完整宿主安装、真实 MCP 查询、Python 公文处理、浏览器交互或 CSV/XLSX 导出全链路验证。

当时图表包清单为 `0.10.1`，其插件 README 开头仍写 `0.10.0`；根 README 的插件清单也未列出问知文档和公文。同步以真实包清单和固定源码为准。当前 Gitee 快照已包含后续插件说明更新。
