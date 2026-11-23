---
slug: zh-cn/real-world-development/cli
title: "GitHub Copilot CLI"
description: "学习 Copilot CLI 模式、自定义功能、MCP 工具和拉取请求自动化，同时构建、验证并交付 Tailspin Toys 的两项更改。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI](https://docs.github.com/copilot/concepts/agents/about-copilot-cli)** 将 GitHub Copilot 作为智能体编码助手带入终端。它可以探索代码库、生成代码、运行命令并连接外部工具——所有操作都在命令行中完成，无需切换到图形化编辑器即可顺畅工作。

通过这些练习，你将先安装并验证 Copilot CLI，再使用自定义指令为它提供项目上下文，然后通过规划模式有目的地构建功能。接下来连接 Playwright MCP 服务器，在真实浏览器中测试功能，并通过可重复使用的智能体技能和自定义智能体扩展 Copilot。最后，探索用于管理上下文、模型和共享的斜杠命令，并回顾所学内容。你还可以学习[可选的 GitHub Copilot CLI 和 Foundry 系列课程][foundry]，通过三个模块准备模型、构建并部署托管智能体，以及将其集成到网站中。

## 练习

| 练习 | 主题 | 说明 |
|----------|-------|-------------|
| [0. 先决条件][ex0] | 设置 | 创建存储库和 codespace |
| [1. 安装 Copilot CLI][ex1] | 安装 | 安装并验证 Copilot CLI |
| [2. 添加星级评分][ex2] | 初次更改 | 添加评分并创建第一个 PR |
| [3. 智能体模式][ex3] | 代码生成 | 使用 Plan 和 Autopilot 模式实现筛选功能 |
| [4. 自定义指令][ex4] | 上下文 | 添加规范并观察 Copilot CLI 如何遵循规范 |
| [5. 智能体技能][ex5] | 技能 | 使用技能执行可重复的质量检查 |
| [6. Playwright MCP][ex6] | 外部工具 | 添加 Playwright MCP 服务器，并在浏览器中测试功能 |
| [7. QA 智能体][ex7] | 智能体 | 创建并使用专用 QA 智能体 |
| [8. 创建并合并拉取请求][ex8] | PR 工作流 | 使用 Agent Merge 管理筛选功能 PR |
| [9. CLI 实用工具][ex9] | CLI 功能 | 探索上下文、模型、共享和可选的云委派 |
| [10. 总结和后续步骤][ex10] | 总结 | 回顾工作流并了解后续资源 |
| [可选：集成 Foundry][foundry] | 托管智能体 | 准备模型、构建并部署基于目录的 Backer Concierge，并将其连接到网站 |

## 先决条件

参加本研讨会前，请确保具备以下条件：

- [ ] 拥有已启用 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 计划的 GitHub 帐户
- [ ] 了解终端/命令行的基本操作
- [ ] 已安装并配置 Git

> [!TIP]
> 没有付费计划？通过 [GitHub Education][callout-student-plan-education] 验证身份的学生可免费使用 GitHub Copilot。**Copilot Student** 计划包含本研讨会使用的智能体、MCP、代码审查和 Copilot CLI 功能，因此可完成所有练习。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> 如果使用 Copilot Business 或 Copilot Enterprise，请确认管理员已为你启用 Copilot CLI。

## 开始

**[从练习 0：先决条件开始 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
