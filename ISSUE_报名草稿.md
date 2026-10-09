# Issue 报名草稿

> 用途：提交到官方仓库 `M-China/mcd-developer-innovation-challenge` 的 Issues。
> 提交时把下方代码块内容复制到 Issue 正文，把 `项目地址` 替换成你自己的仓库地址。

---

## 提交方式

1. 打开：https://github.com/M-China/mcd-developer-innovation-challenge/issues/new
2. **Title**：自定义报名标题（例：`麦麦省钱官 McdSaving Expert 参赛申请`）
3. **Body**：复制下方内容
4. 提交后系统会在 Issue 下回复报名成功/失败通知

---

## Issue 正文（复制这段）

```text
【参赛申请】
项目名称：麦麦省钱官 McdSaving Expert
项目地址：https://github.com/你的用户名/mcd-saving-expert
项目简介：基于麦当劳官方 MCP 的 AI 省钱助手。把省钱从「凭经验教你判断」升级为「用官方实时数据替你算账」——一键领券（auto-bind-coupons）、真实到手价核算（calculate-price 拆解标价/优惠/配送费/应付）、自提与外送双场景真实比价、基于官方营养数据的配餐建议。所有价格与优惠均来自麦当劳 MCP 实时接口，不推测、不编造、数字带查询时间标注。
```

---

## ⚠️ 提交前必查清单

| 检查项 | 要求 | 状态 |
|---|---|---|
| 仓库为 **Public** 公开可访问 | 必须是public | ☐ |
| 项目创建时间在 2025-12-25 ~ 2026-10-25 | 官方的报名条件之一 | ☐ |
| `README.md` 存在，文件名不可改 | 必须 | ☐ |
| `CONTEST_DECLARATION.md` 存在，**内容与官方原文一字不差** | 必须 | ☐ |
| `MCP_INTEGRATION.md` 存在，文件名不可改 | 必须 | ☐ |
| `mcp-config.example.json` 存在，**仅环境变量占位符** | 必须 | ☐ |
| 真实使用了麦当劳 MCP 能力 | 必须 | ☐ |
| `workbuddy.md`（若要拿 WorkBuddy 3000 积分专项） | 拿专项奖必须提交 | ☐ |
| 项目内容无违法违规/敏感内容 | 必须 | ☐ |
| 项目地址已替换成你的真实仓库地址 | 别忘了改 | ☐ |

---

## 拿 WorkBuddy 专项奖励的额外要求

规则明确：**排行榜前100 名且真实使用腾讯 WorkBuddy + 提交 `workbuddy.md`**，每人可得3000 积分。

`workbuddy.md` 需要包含你用 WorkBuddy 开发这个 Skill 的**对话上下文**，用于核验是否符合联动活动奖励条件。

**怎么做**：本项目本身就是在 WorkBuddy 里开发的（方法论来自已有的省钱专家包，代码与文档由 WorkBuddy 辅助产出）。把本次开发过程的关键对话导出整理进 `workbuddy.md` 即可。

---

## 传播提示（合规拿 Star）

规则明确禁止**刷榜**：多账号、机器人刷星、群控、串通刷 Star，一经发现**直接取消资格且不通知**。

**合规做法**：
- 真实分享给身边朋友/同事，让他们基于真实兴趣点Star
- 在技术社区（掘金、CSDN、GitHub 中文社区）写一篇开发过程文章，附仓库链接
- 强调项目解决什么真实问题（省钱的"算账"能力），而不是单纯喊"求 Star"

** Star 是核心排名依据**，但**比刷榜更值钱的是让真实用户觉得有用**。