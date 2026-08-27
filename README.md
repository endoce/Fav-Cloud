# Fav-Cloud

一个简洁的个人网址导航页，用于集中访问常用网站、AI 工具、云服务、媒体资源和创客工具。

## 功能

- 按分类展示常用链接
- 自动统计每个分类的链接数量
- 支持亮色与暗色主题
- 记住用户的主题选择
- 响应式网格布局，适配桌面与移动设备
- 按需检测大陆直连与 Google 代理出口，并显示 IP、位置、网络和延迟
- 对比两个出口地址，提示分流是否生效

## 使用

这是一个纯静态项目，不需要安装依赖或执行构建命令。

1. 下载或克隆仓库。
2. 在浏览器中打开 `index.html`。
3. 也可以通过 GitHub Pages 或任意静态网站服务部署。

## 项目文件

- `index.html`：页面结构、样式和交互逻辑
- `FiraCode-Regular.woff2`：页面字体
- `The_Internet.png`：网站图标

## 修改链接

网址分类和链接都位于 `index.html` 的 `.portals` 区域。新增或删除 `<li>` 后，分类右上角的数量会自动更新。

## 网络出口检测

页面底部的网络状态面板只会在用户点击检测按钮后发起请求：

- 大陆出口通过太平洋电脑网的国内 JSONP 接口 `whois.pconline.com.cn` 查询，避免大陆线路访问 Cloudflare 时被代理规则接管。
- Google 出口通过自建 Cloudflare Worker `google-ip.crownpartnersgroup.com` 查询。
- 两个出口地址不同则显示分流正常；相同则提示未检测到分流。
- IP 地址默认脱敏，用户可手动切换为完整显示。

大陆检测不再依赖 `cn-ip.crownpartnersgroup.com`。若使用代理客户端，应让太平洋电脑网接口保持直连，并让 Google 检测域名按 Google 规则走代理。

## 隐私说明

项目中包含一个指向局域网 OctoPrint 服务的地址。该地址仅在对应的本地网络中可访问，不会公开局域网设备本身。

网络出口检测不会自动运行；只有点击检测按钮后才会向上述两个服务发送请求。

## 部署

当前提供两个自动部署地址：

- GitHub Pages：https://endoce.github.io/Fav-Cloud/
- Cloudflare Pages：https://fav-cloud.pages.dev/
- Cloudflare Pages 自定义域：https://fav.ydht.net/

Cloudflare Pages 项目连接 `master` 分支，框架预设为“无”，不填写构建命令，构建输出目录使用 `/`。

## License

本项目暂未声明开源许可证。
