# 数据源（2026-09-29 实测）

本 skill 是"流程+模板"型，回检阶段的数据需求复用兄弟 skill 已实测的公开接口，
以下接口均于 2026-09-29 在本沙箱亲手验证可用。引用来源文件见每节标注。

## 1. 行情事实（回检"价格/涨跌"类假设）

复用 `~/workspace/skills/laogu-fundamentals/references/data-sources.md`：

| 接口 | URL 模板 | 实测状态（2026-09-29） |
|---|---|---|
| 新浪行情（主力，需 Referer，GBK→UTF-8 转码） | `https://hq.sinajs.cn/list={codes}`（Referer: https://finance.sina.com.cn/） | ✅ 可用。示例 `sz002466` 返回 2026-09-29 15:00 收盘价 40.55 |
| 腾讯行情（备选） | `https://qt.gtimg.cn/q={codes}` | ✅ 本环境可用（部分网络环境 TCP 超时，注意降级）。同上例返回 40.55 |
| 东财 push2（备选，含市值/PE/PB） | `https://push2.eastmoney.com/api/qt/stock/get?secid={secid}&fields=...` | ⚠️ 本次未重测，沿用 laogu-fundamentals 记录（部分环境 502/404），降级用 |

代码前缀规则（复用 laogu-news）：深交所 0/3 开头→`sz`，上交所 6/9 开头→`sh`，北交所 4/8/92 开头→`bj`。

Fallback 链：腾讯 → 新浪 → 东财 push2 → 网页搜索（`{公司名} 股价 {日期}`，标"未核验"）。

## 2. 公告/事件事实（回检"业绩/分红/减持"类假设）

复用 `~/workspace/skills/laogu-fundamentals/references/data-sources.md`：

| 接口 | URL 模板 | 实测状态（2026-09-29） |
|---|---|---|
| 东财公告列表 | `https://np-anotice-stock.eastmoney.com/api/security/ann?...&stock_list={纯数字代码}`（Referer: https://data.eastmoney.com/） | ✅ 可用。`stock_list` 必须纯数字，不带 .SZ 后缀 |
| 东财公告正文 | `https://np-cnotice-stock.eastmoney.com/api/content/ann?art_code={art_code}&client_source=web&page_index={page}` | ✅ 沿用 laogu-fundamentals 实测结论（JS 空壳页面不要直接抓，用此内容接口） |

## 3. 业绩/研报/宏观事实（程序化接口覆盖不到时）

**主力路径：网页搜索**（复用 laogu-fundamentals 方法论）。搜索模板：

- 业绩类：`{公司名称} {2026年半年报/2025年年报} 营业收入 归母净利润`
- 事件类：`{公司名称} {减持/分红/定增/诉讼} {YYYY-MM}`
- 宏观类：`{事件} {YYYY年MM月} 数据 结果`
- 研报类：`{公司名称} 研报 评级 目标价`

要求：至少两个独立来源交叉（上证报/新京报/格隆汇/公司公告转载等），标注来源与日期；
拿不到的指标直接标"未核验"，不许用旧年报倒推、不估算。

## 4. 诚实标注的边界

- 无法程序化获取的"观点原文"（如某大V/研报作者的历史观点）：以用户提供的截图/链接为准，
  宿主用网页搜索核对发布时间，核对不上则标注"原文待用户确认"。
- 本 skill 不承诺自动发现"所有历史观点"：档案库只包含经本 skill 建档的观点，
  用户在别处随口说过的观点不在回检范围内，如实说明。
