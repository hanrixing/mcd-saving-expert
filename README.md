# 麦麦省钱官 · McdSaving Expert

> 一个基于麦当劳官方 MCP 的 AI 省钱助手 —— 把「凭经验教你判断便宜」升级为「用官方实时数据替你算账」。

<details open>
<summary><b>🌐 English summary</b> (click to collapse / <a href="README_EN.md">full English README</a>)</summary>

An AI money-saving assistant built on McDonald's China **official MCP**.
Prices, coupons and orders are computed from **live official data** — not guessed.

- **Claim coupons** in one shot (`auto-bind-coupons`)
- **Compute the real bill** — item price, discounts, delivery fee, payable total (`calculate-price`)
- **Decide** pickup vs. delivery, combo vs. single, with real nutrition data

**Other assistants give you "advice". McdSaving gives you "the finished bill".**

Works with WorkBuddy + `mcd-mcp` connector. See [README_EN.md](README_EN.md) for installation and usage.

</details>

---

## 介绍

### 为什么要做这个

点外卖的人都有同一种困惑：**"这份到底贵没贵？我是不是又多花了冤枉钱？"**

市面上的省钱助手给出的答案通常是**建议**——"建议比价""建议先领券""建议自提"。但建议不是账。你真正想知道的是：**我此刻点这一单，掏多少、能省多少。**

更麻烦的是，靠人工检索得到的"优惠信息"本质是**经验区间**，会过期、会互相矛盾，甚至会误导。真正权威的答案——**这家店现在的价格、你账户里真实有多少券、一单实际到手多少**——只有官方数据源能给。

### 解决什么

把三件事一次做完：

1. **领券** — 一键领走当前所有可领券，并告诉你账户里真实有多少张券在用
2. **算账** — 真实价格计算：餐品价、优惠、配送费、应付总额，一目了然
3. **决策** — 自提 vs 外送、套餐 vs 单点，用真实价格和真实营养数据帮你选

### 一句话卖点

**别家省钱助手给你"建议"，麦麦省钱官给你"算完的账"。** 因为价格、券、订单全部来自麦当劳官方 MCP 实时数据，不是推测。

---

## 安装方法

### 前置条件

- WorkBuddy客户端
- 一个麦当劳中国 MCP Token（[免费申请](https://open.mcd.cn/mcp)）

> Token 申请：登录 → 控制台 → 激活 → 同意协议 → 复制 Token

### 步骤

**1. 配置 MCP 连接器**

打开 WorkBuddy → 左侧边栏【专家 · 技能 · 连接器】→【连接器】→ 右上角【自定义连接器】→【配置 MCP】，填入：

```json
{
  "mcpServers": {
    "mcd-mcp": {
      "type": "streamablehttp",
      "url": "https://mcp.mcd.cn",
      "headers": {
        "Authorization": "Bearer YOUR_MCP_TOKEN"
      }
    }
  }
}
```

⚠️ 务必把 `YOUR_MCP_TOKEN` 替换成你的真实 Token，然后点击【保存】。

**2. 启用连接器**

回到【自定义连接器】，将 `mcd-mcp` 设为【启用】。

**3. 安装 Skill**

把本仓库的 `SKILL.md` 与 `references/` 目录放入你的 Skill 目录，或直接在对话中引用本仓库。

---

## 使用示例

### 示例一：今天有什么券可以领

> **你**：现在有什么券可以领？
>
> **助手**：先帮你把可领的券全领上——
> 调用 `available-coupons` 查询可领券 → 调用 `auto-bind-coupons` 一键领取 → 调用 `query-my-coupons` 核对账户实有券
>
> **结果**：已为你领取 4 张券，当前账户可用券 7 张。最近可用的：
> - 巨无霸套餐立减 8 元（满 45 元可用）
> - 麦辣鸡腿堡单点立减 5 元
> - 下午茶时段券（14:00–17:00）
> - 免配送费券 × 2
>
> 提示：其中 2 张免配送费券将在 3 天后过期，建议本周用掉。

### 示例二：这一单到底多少錢

> **你**：附近有麦当劳吗？点一个巨无霸套餐要多少钱？
>
> **助手**：调用 `query-nearby-stores` 查附近门店 → `query-meals` 查该店可售餐品 → `query-meal-detail` 查套餐组成 → `calculate-price` 计算真实到手价
>
> **结果**：距离你 1.2 公里有**琼山凤翔东路店**（营业中）。
> 巨无霸超值套餐（巨无霸 + 中薯 + 可乐）：
> - 标价：45.0 元
> - 可用券：-8 元（巨无霸套餐立减）
> - 配送费：3.0 元
> - **应付：40.0 元**
>
> 建议：到店自提可省3 元配送费，实付约 **37.0 元**。

### 示例三：自提还是外送

> **你**：自提和外卖哪个划算？
>
> **助手**：分别用 `create-order`（到店取餐）与麦乐送场景计算，比对总额
>
> **结果**：
> | 方式 | 餐品 | 优惠 | 配送费 | 应付 |
> |---|---|---|---|---|
> | 到店自提 | 45.0 | -8 元 | 0 | **37.0 元** |
> | 麦乐送 | 45.0 | -8 元 | 3.0 | **40.0 元** |
>
> **结论**：自提立省 3 元，到店仅 1.2 公里，建议自提。

### 示例四：控热量怎么点

> **你**：减脂期能吃麦当劳吗？帮我配个 500 大卡的
>
> **助手**：调用 `list-nutrition-foods` 查真实营养成分 → 组合配餐并计算总热量
>
> **结果**：
> - 巨无霸（单堡）：约 520 大卡 → 偏高，建议换麦辣鸡腿堡（约 500 大卡）或 grilled Chicken
> - 玉米杯（中）：约 80 大卡，膳食纤维高，适合作为碳水替代
> - 不建议搭配含糖饮料，可换无糖可乐
>
> ⚠️ 本助手不构成医疗或营养专业建议，特殊饮食需求请遵医嘱。

---

## 目标用户

| 人群 | 典型场景 | 能省多少 |
|---|---|---|
| 上班族 | 每周点 3–5 次，午市高峰配送费高 | 5–15 元/单 |
| 精打细算的学生党 | 预算紧，纠结自提还是外送 | 3–8 元/单 |
| 减脂人群 | 想吃麦当劳又怕热量超标 | 省心+ 控热量 |
| 优惠券敏感人群 | 不知道账户里有多少券在过期 | 避免浪费 |

---

## 项目结构

```
mcd-saving-expert/
├── SKILL.md                      # Skill 主入口
├── README.md                     # 项目介绍（中文，本文件）
├── README_EN.md                  # English README
├── CONTEST_DECLARATION.md# 参赛声明（官方原文）
├── MCP_INTEGRATION.md            # MCP 能力说明与调用流程
├── mcp-config.example.json       # 脱敏配置示例
├── workbuddy.md                  # WorkBuddy 开发对话上下文
├── docs/
│   └── mcp-proof.jpg             # 真实调用麦当劳 MCP 的存证截图
└── references/
    ├── 省钱方法论总纲.md          # 核心判断框架
    ├── 券叠加与失效预警.md        # 券的正确使用顺序
    ├── 自提与外送决策.md          # 到店自提省钱逻辑
    ├── 凑单陷阱识别.md            # 先涨后降/凑单更贵
    └── 营养搭配参考.md            # 真实营养数据组合
```

---

## 设计原则

1. **官方数据优先**：价格、券、营养一律来自麦当劳 MCP，不推测、不编造
2. **不确定就说不确定**：查询失败如实告知，不给假数字
3. **信息时效性**：券和价格实时变化，缓存结果需标注查询时间
4. **守好边界**：不构成医疗/营养建议，消费决策权在用户

---

## 真实使用存证

本项目已**真实调用麦当劳官方 MCP** 完成「附近门店查询 + 可领券查询」，截图见 [docs/mcp-proof.jpg](docs/mcp-proof.jpg)（海口市琼山区附近 5 家门店及可领券信息，由 `mcd-mcp` 实时返回，非编造）。作为报名参赛的"真实使用"凭证。

---

## 致谢

- 麦当劳中国提供开放 MCP 能力
- WorkBuddy 提供开发与运行平台