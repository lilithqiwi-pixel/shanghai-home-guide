# 沪上置业指南

这是一个无构建步骤的响应式静态网站。开发预览请在 `outputs` 目录运行 `python -m http.server 8000`，然后访问 `http://localhost:8000`。浏览器直接打开 HTML 文件时，现代浏览器可能会限制 JSON 数据读取。

社区数据单独维护在 [data/communities.json](data/communities.json)，房源数据在 [data/market-listings.json](data/market-listings.json)。页面的“数据管理”可导入、导出两类 JSON；导入只影响当前浏览器。房源区的“刷新挂牌数据”重新读取网站已发布的数据文件。

## 房源数据更新

核对平台挂牌页是否仍有效，更新 `data/market-listings.json` 中的价格、挂牌日期、面积及来源链接，并更新 `datasetUpdatedAt`。每个板块的 `listings` 是可编辑记录数组。发布新文件后，访客点击“刷新挂牌数据”即可读取新版本；已部署的网站需要先把修改后的文件上传/提交到托管仓库。

## 建立可分享的网址

可用 GitHub Pages 发布这个静态站点。GitHub 官方文档说明 Pages 可直接发布仓库里的 HTML、CSS 和 JavaScript 文件；可选择从分支的根目录发布。

1. 在 GitHub 新建仓库，例如 `shanghai-home-guide`。
2. 将 `outputs` 里面的 `index.html`、`app.js`、`styles.css`、`negotiation.css`，以及 `data` 文件夹上传到仓库根目录。不要把整个 `outputs` 文件夹再套一层。
3. 打开仓库 **Settings → Pages → Build and deployment**，选择 **Deploy from a branch**，分支选 `main`，目录选 `/(root)`，然后保存。
4. 发布完成后，Pages 设置页会显示网址，通常形如 `https://你的用户名.github.io/shanghai-home-guide/`。

仓库设为公开时，网站代码和挂牌数据也会公开。以后更新房源数据文件并提交到仓库，Pages 会按发布设置更新网站。此站没有房产平台的实时接口，所以“刷新”是读取最新发布的 JSON；房源核实和更新仍需有人维护。

核心社区详情中的社区租金与部分参考单价仍是演示估算；“预算房源参考”另列公开平台挂牌摘录，并显示原页面日期与链接。挂牌可能已售出或调价，不能视为实时可售保证。谈判滑块的税费和装修使用演示假设，不代表真实可谈价或个性化购房成本。
