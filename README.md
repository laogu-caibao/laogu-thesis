# 观点追踪（laogu-thesis）

把你的投资观点建档留存，N 周后自动回检"当初说的还成立吗"——敢下判断，更敢认错。

## 功能速览

- **观点建档**：记录时间/标的/核心判断/关键假设/证伪条件，档案一旦写入正文只读，不留事后改口的余地
- **到期回检**：对照今天的事实逐条判定，只许三档结论——成立 / 部分成立 / 被证伪，禁用"基本符合"等模糊话术
- **打脸报告**：被证伪的项必须坦诚列出并复盘"错在哪、为什么错"；连载体例"老谷观点追踪第 N 期"
- **反偏见清单**：事后合理化、选择性记忆、移动球门柱等 6 条自查，专治"马后炮"
- 回检取数复用 laogu 系列已实测公开接口（行情/公告），零 key；合规：只做事实对比与复盘，不做买卖推荐

方法论借鉴 MIT 许可的 ai-berkshire 的 thesis-drift（投资论文追踪）思路，文案全部原创。

## 一键安装

```bash
git clone https://github.com/laogu-caibao/laogu-thesis.git
```

- ZIP 下载：https://github.com/laogu-caibao/laogu-thesis/archive/refs/heads/main.zip
- npx 一键安装：`npx skills add laogu-caibao/laogu-thesis`
- 扣子（Coze）：扣子编程 → 技能面板 → 创建技能 → 本地上传（仓库根目录已有 SKILL.md，直接压缩仓库文件夹即可）；页面要求 `.skill` 后缀时由扣子导入后自动生成，不要只改 zip 扩展名
- Trae：设置 → 技能 → 上传技能（同上 zip）；或手动放到 `~/.trae/skills/laogu-thesis/`（项目级用 `.trae/skills/laogu-thesis/`，TRAE Work 国区版路径为 `~/.trae-cn/skills/`）
- MCP 一次装全：`uvx laogu-mcp`（16+ 工具，skill 负责流程指导、MCP 负责工具调用）

## 目录结构

- `SKILL.md`：完整流程（建档→回检→打脸报告）+ 模板 + 反偏见清单
- `references/sources.md`：复用的兄弟 skill 接口与实测状态 + 网页搜索模板
- `mcp-config.json`：MCP 热更新配置
- `MARKET.md`：市场调研

## 出品：老谷拆财报

以数据为刃，剖市场真相。

- 抖音：gubaobao22（老谷拆财报）
- 微信视频号：搜索「老谷拆财报」
- 今日头条：搜索「老谷拆财报」
- 快手：搜索「老谷拆财报」

财经科普、财报解读。个人观点，仅供参考，不构成投资建议。
