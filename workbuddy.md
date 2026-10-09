# WorkBuddy 开发上下文说明

## 项目信息
- **项目名称**：麦麦省钱官 McdSaving Expert
- **GitHub 仓库**：https://github.com/hanrixing/mcd-saving-expert
- **官方报名 Issue**：https://github.com/M-China/mcd-developer-innovation-challenge/issues/56
- **开发环境**：WorkBuddy（Windows 桌面端，会话工作区 `E:/个人/workbuddy/2026-10-09-14-09-47`）
- **开发日期**：2026-10-09

## WorkBuddy 在本项目中的使用方式

本项目从赛事研究、方案设计、文件编写到 Git 推送，全程在 WorkBuddy 桌面端内完成。WorkBuddy 作为 AI 协作环境，承担了以下工作：

1. **赛事情报与研究**
   - 通过内置浏览器工具抓取麦当劳 × WorkBuddy 开发者大赛的官方规则（`M-China/mcd-developer-innovation-challenge`）。
   - 提取 README、`activityGuidelines.md`、`RANKING.md`、`CONTEST_DECLARATION.md` 中的关键规则、奖励、合规要求。

2. **方案融合设计**
   - 调用用户既有专家包 `daily-saving-expert`（省钱专家）的《线上订餐省钱实战手册》《优惠信息源地图》等参考文件。
   - 将省钱专家的方法论（券叠加顺序、到店自提杠杆、凑单陷阱识别、营养搭配）与麦当劳官方 MCP 工具（`auto-bind-coupons`、`calculate-price`、`query-nearby-stores`、`list-nutrition-foods` 等）进行映射，形成「从经验建议升级为实时数据算账」的项目定位。

3. **参赛文件一键生成**
   - 在 WorkBuddy 工作区 `E:/个人/workbuddy/2026-10-09-14-09-47/mcd-saving-expert/` 下生成全部参赛文件：
     - `README.md`
     - `CONTEST_DECLARATION.md`（官方原文逐字复制，未改动）
     - `MCP_INTEGRATION.md`
     - `mcp-config.example.json`
     - `SKILL.md`
     - `references/` 下的 5 份方法论 MCP 化改造文档
     - `ISSUE_报名草稿.md`
     - `合规自检与待办.md`

4. **Git 与 GitHub 操作**
   - 本地 `git init`、配置提交身份、完成首次 commit。
   - 添加远程 `origin` 为 `https://github.com/hanrixing/mcd-saving-expert.git`。
   - 通过本机 Git Credential Manager 完成 GitHub 授权后，将 `master` 分支推送至公开仓库。
   - 后续追加 `workbuddy.md` 并再次推送。

5. **任务看板管理**
   - 使用 WorkBuddy 内置 TaskCreate / TaskUpdate / TaskList 管理 14 项子任务，确保参赛流程每一步可追溯。

## 使用到的 WorkBuddy 工具类型

- **文件读写**：Read / Write / Edit
- **代码与命令**：Bash（Git 操作、网络探测）
- **网络研究**：WebFetch / WebSearch
- **任务管理**：TaskCreate / TaskUpdate / TaskList
- **可视化说明**：show_widget（GitHub 建仓/Issue 提交步骤标注）
- **记忆管理**：自动写入工作区 daily log 与 MEMORY.md

## 声明

本项目代码、文档与方法论均由用户在 WorkBuddy 桌面端内，通过对话式协作生成与迭代。`workbuddy.md` 用于证明该作品使用 WorkBuddy 进行开发，以申请大赛「WorkBuddy 专项奖励」中的额外 3000 积分。
