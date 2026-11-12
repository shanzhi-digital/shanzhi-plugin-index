# 善治插件目录

供小智办公和 DeepSeek Harness 的「插件 → 发现」页面读取的独立插件索引仓库。索引采用官方插件市场格式 1，可同时收录第三方插件与善治自研插件。

## 配置索引源

在「插件」页面的实验性插件中启用「自定义插件索引」，进入「发现 → 添加索引源」，填入以下地址。该 CDN 入口已于2026-11-12在客户端所在电脑上通过无代理 Node 请求和官方格式校验：

```text
https://fastly.jsdelivr.net/gh/shanzhi-digital/shanzhi-plugin-index@main/index.json
```

备用 CDN 地址：

```text
https://gcore.jsdelivr.net/gh/shanzhi-digital/shanzhi-plugin-index@main/index.json
```

GitHub 原始地址仍可使用，但需要当前网络能够访问 `raw.githubusercontent.com`：

```text
https://raw.githubusercontent.com/shanzhi-digital/shanzhi-plugin-index/main/index.json
```

上述地址读取同一份公开的静态 JSON，不需要 GitHub 登录。网页仓库地址不能代替索引文件地址。索引由 Host 进程读取，浏览器能够访问 GitHub 不代表 Host 的网络和代理也可用；CDN 的可达性同样取决于当前网络。此仓库的创建不修改小智办公源码，也不自动改变现有客户端配置。

如果原始地址显示「无法读取此索引」，在「发现 → 管理索引源」移除该地址，添加上面的 CDN 地址，再刷新。2026-11-12的本机复测中，GitHub 原始地址返回 `ECONNRESET`，两个 CDN 地址均直接返回200、未重定向，内容与仓库一致。成功读取空目录后，应显示目录名称及「此索引没有插件」。

## 当前内容

当前索引有效，但插件列表为空。尚未导入第三方目录、发布自研插件或宣称兼容性测试通过。添加真实插件并更新 `main` 上的 `index.json` 后，客户端刷新索引即可读取；Host 可能缓存索引，发现页的刷新操作会重新获取。CDN 还存在独立缓存，更新不会保证立即可见，发布后需核对实际读取到的内容。

## 仓库分工

- [`index.json`](index.json)：客户端实际读取的目录，维护插件资料、精确版本、兼容范围和安装来源。
- [`CONTRIBUTING.md`](CONTRIBUTING.md)：插件收录、版本维护和发布校验约定。
- [shanzhi-plugin](https://github.com/shanzhi-digital/shanzhi-plugin)：组织现有的私有插件源码库，访问需要仓库权限。本仓库不会复制或公开其源码。

收录公开第三方插件时，通常引用作者的 npm 包或固定 Git 提交即可，不需要复制代码。私有源码的安装仍要求用户拥有相应凭据；公开索引本身不会授予私有仓库访问权限，索引中不得包含令牌或密码。

## 格式与限制

本索引基于 DeepSeek Harness `0.2.2-rc.1` 的格式 1 校验器初始化。发布前按[维护约定](CONTRIBUTING.md)校验当前格式与真实安装来源。

发现页可浏览、筛选、查看详情和确认安装。当前官方市场界面的版本更新只显示状态，升级通常需要卸载后重新安装。插件许可与使用要求由各插件作者维护，本目录的收录不改变其许可证。

参考：[官方发现页](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/client/ui-plugin-market/README.zh.md)、[官方索引格式](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/util/plugin-market-index/README.zh.md)。
