# Mintfolio Theme Starter

这是一个可打包的最小独立主题示例。它只包含 `home`、`post`、自己的布局、样式和经 `?url` 导入的 SVG 资源；Core 会为未声明的可选页面使用内置 Minimal。受保护文章直接组合 Core 的 ProtectedArticle 组件。

主题只导入 `@mintfolio/core` 的主题公共入口，不能复制或相对导入宿主的 `src/core`、站点配置或内容集合。先在主题的开发环境中安装 SDK 的本地打包产物，再安装 Astro：

```sh
npm install /absolute/path/to/mintfolio-theme-api-1.0.0.tgz /absolute/path/to/mintfolio-core-0.1.0.tgz astro@^7.3.2
```

将 `theme.mjs` 的 `id`、名称、作者、页面和设置改为自己的内容。包入口固定导出 `./theme`，宿主通过该入口定位清单：

```sh
npm pack
# 在 Mintfolio 站点中安装生成的 tgz，然后：
# theme.config.mjs
export default { theme: 'theme-mintfolio-starter', settings: {}, overrides: { pages: {} } };
```

主题作者应使用 Core 提供的 `post.url`、taxonomy term 的 `url` 和 `theme.urls`，不要自行拼接 `/blog/...` 或 `/about`。v1 的标签、分类和搜索使用已有 `/blog?q=…&tag=…&category=…` 查询路由，不新增端点。`extends`/主题继承不受支持。

在宿主仓库中，`npm run test:theme-package` 会以 npm 12 兼容方式把 SDK、Core、Default 与 Starter 打成实际 tarball，安装到仓库外的独立站点，再检查公开 SDK、六页 fallback 构建、加密输出、CSS 和 SVG 资源。它验证包交付边界，不替代主题自身的浏览器验收。完整契约和边界说明见宿主项目的 `MintfolioCore/docs/theme-api.md`。

## 独立仓库开发

最小第三方主题示例。src 只含主题页面、布局、样式、资产。缺省页面和加密文章界面复用 Core；不复制 Core 实现。

```sh
npm ci
npm run check
npm pack
```

这个仓库可单独安装，不需要 PersonalSite 或其他源码目录。拆分前历史保留在原 PersonalSite，起点见 MIGRATION.md。 尚未发布的依赖固定在 vendor 和锁文件中；更新方式见 vendor/README.md。
