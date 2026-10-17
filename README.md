# 沪上置业指南

这是一个无构建步骤的响应式静态网站。开发预览需在 `outputs` 目录运行静态 HTTP 服务，再访问 `http://localhost:8000`。

首页搜索按小区名称、区域和 120–230 万总价筛选挂牌房源。首页精选 6 个社区，完整挂牌在同一结果区。详情里可调整挂牌价下浮 1%–10%、全款/50%/80%首付、月租金、年房价变化和通胀假设；购入成本及收益测算会随输入同步。装修估算为 2,000 元/㎡。

## 更新房源

数据文件为 [data/market-listings.json](data/market-listings.json)。页面的“数据管理”可导入、导出 JSON，但导入只保存在当前浏览器。公开网站更新步骤：

1. 核验来源平台上的挂牌状态、总价、户型、面积和发布日期。
2. 更新 `datasetUpdatedAt` 和 `data/market-listings.json` 中相应记录。
3. 将更新后的 `app.js`、`index.html`、`styles.css`、`negotiation.css` 与 `data/market-listings.json` 上传/提交到 GitHub 仓库根目录。
4. 等 GitHub Pages 发布完成后，访客点“更新数据”重新读取最新文件。

刷新按钮不抓取房产平台，也不会自行发现新房源；本站没有房产平台 API。当前数据是带来源链接和挂牌页日期的快照，非完整实时库存。对于缺少足够合适挂牌的区域，不用估价或虚构房源补数。

GitHub Pages 发布方式见仓库设置 **Settings → Pages → Deploy from a branch → main → /(root)**。代码与 JSON 放在仓库根目录，不能再套一个 `outputs` 文件夹。
