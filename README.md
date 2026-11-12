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

当前已登记源码仓库中现有的一个插件：

| 插件 | 包名 | 版本 | 状态 |
|---|---|---|---|
| 通用查询结果图表 | `@local/datahub-echarts` | `0.7.0` | 善治自研、公开来源、仅登记；安装与运行兼容性未验证 |

安装来源固定到源码仓库的完整提交和 `plugins/datahub-echarts` 子目录。该包未声明 `engines.dsh`，索引保留空要求，不表示已经通过当前版本兼容性测试。时间字段记录已核实源码提交的时间，不表示已向 npm 发布。

源码仓库现已由维护者改为公开，本目录相应更新为「公开来源」，仍保留「仅登记」：尚未验证安装与当前 DSH 的运行兼容性，也未发布 npm 包。更新 `main` 后，客户端刷新索引即可读取；Host 和 CDN 均有独立缓存，更新不保证立即可见，发布后需核对实际读取内容。

## 仓库分工

- [`index.json`](index.json)：客户端实际读取的目录，维护插件资料、精确版本、兼容范围和安装来源。
- [`CONTRIBUTING.md`](CONTRIBUTING.md)：插件收录、版本维护和发布校验约定。
- [shanzhi-plugin](https://github.com/shanzhi-digital/shanzhi-plugin)：组织的公开插件源码库。本仓库只引用版本和路径，不复制源码。

收录公开第三方插件时，通常引用作者的 npm 包或固定 Git 提交即可，不需要复制代码。私有源码的安装仍要求用户拥有相应凭据；公开索引本身不会授予私有仓库访问权限，索引中不得包含令牌或密码。

## 格式与限制

本索引基于 DeepSeek Harness `0.2.2-rc.1` 的格式 1 校验器初始化。发布前按[维护约定](CONTRIBUTING.md)校验当前格式与真实安装来源。

发现页可浏览、筛选、查看详情和确认安装。当前官方市场界面的版本更新只显示状态，升级通常需要卸载后重新安装。插件许可与使用要求由各插件作者维护，本目录的收录不改变其许可证。

参考：[官方发现页](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/client/ui-plugin-market/README.zh.md)、[官方索引格式](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/util/plugin-market-index/README.zh.md)。
