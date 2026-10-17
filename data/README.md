# 社区数据维护说明

页面从 `communities.json` 读取数据，前端界面与数据分离。字段金额以人民币计，距离以公里计，面积以平方米计。随站点发布时可直接替换这个文件；浏览器里的“数据管理”也支持 JSON 导入、导出和恢复演示数据。

## 顶层结构

```json
{
  "schemaVersion": 1,
  "datasetUpdatedAt": "2026-10-17",
  "datasetLabel": "来源描述",
  "communities": []
}
```

每个社区字段：

- `id`, `name`, `district`, `area`, `address`, `updatedAt`
- `dataStatus`: `verified` 或 `demo`；演示数据必须继续标为 `demo`
- `sources`: 来源对象数组，含 `name`, `url`, `accessedAt`, `fields`
- `transit`: `{ name, lines, distanceKm }[]`；页面展示 2 公里内站点
- `malls`: `{ name, distanceKm }[]`；页面展示 2 公里内商场
- `units`: `{ layout, areaSqm, unitPriceYuanSqm }[]`
- `rentalIncome.monthlyRentYuan`
- `costs`: `downPaymentRate`, `deedTaxRate`, `agencyFeeRate`, `otherPurchaseYuan`, `renovationYuanPerSqm`, `maintenanceEventYuan` (每次周期性大修金额), `maintenanceIntervalYears`, `sellingCostRate`
- `assumptions`: `annualAppreciationRate`, `annualRentGrowthRate`, `annualHoldingCostGrowthRate`, `annualPropertyFeeYuan`, `annualPropertyTaxYuan`, `modelNote`

## 收益模型

总价 = 户型面积 × 户型单价。首付 = 总价 × 首付比例。购入现金 = 首付 + 契税 + 中介费 + 其他购入支出 + 装修；契税及中介费按总价比例估算。年租金收入以租金年增长率复利增长。持有期成本计入物业费、房产税假设与每隔指定年数的大修金额。期末净终值 = 期末估值 × (1 − 出售成本率) + 累计租金 − 累计持有及维修成本。净实际收益 = 期末净终值按通胀折算至今日价值 − 初始投入。未包含按揭利息/还款、租赁空置、个人所得税及法律政策变动；应结合实际购房资格、税费政策和房屋条件复核。

页面的核心社区运行示例数据纯属演示，不是实盘行情或真实社区调查结果。更新数据时，为每个来源填写链接或出处，并更新 `updatedAt`。

## 预算房源数据

房源参考独立存放在 `market-listings.json`。每个板块字段含 `id`、`name`、来源名称/链接以及 `listings` 数组。每条挂牌记录包含社区、户型、面积、挂牌总价（万元）、单价、来源页面展示的发布日期及来源网址。更新后同步改顶层 `datasetUpdatedAt`。页面默认显示 120–230 万（目标 130–220 万，预留上下各约 10 万），每个板块当前列至少 6 条公开挂牌参考。

页面可导入/导出房源 JSON，导入结果保存在当前浏览器；点击“刷新挂牌数据”则强制重新读取网站公开的数据文件。要让所有访客看到更新，必须把更新的 `market-listings.json` 发布到网站托管仓库。本站没有房产平台 API，因此不会自动实时抓取挂牌；逐条打开来源确认后再更新，避免把历史页面数据误报为当前在售。

谈判滑块默认为挂牌价的 95%，可在挂牌价的 90% 至 100% 范围选择。滑动后实时重算折算单价、35%首付，以及示例现金额（首付 + 1.5%契税 + 1%中介费 + 3500元/㎡装修）。这些比率是演示情景，不是法律税费结论或经纪人议价建议；请按实际家庭住房套数、房屋性质、合同与装修报价调整。
