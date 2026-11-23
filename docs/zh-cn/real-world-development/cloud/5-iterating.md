---
title: "练习 5：迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作

在本练习中，你让 GitHub Copilot 处理了多个任务，以改进用户体验并添加功能。你要求 Copilot 为代码添加文档、为设计团队创建相关游戏功能以供迭代，以及实现高对比度和浅色模式切换等无障碍访问功能。现在我们来查看代码更改；必要时，也可以向 Copilot 提供反馈，进一步改进其工作。

### 场景

如前面多次强调的，采用生成式 AI 并不会改变软件设计和 DevOps 的基本原则。我们仍然需要审查生成的代码并遵循正常的 DevOps 流程。接下来，我们会在为团队其他成员启用审查之前，检查 GitHub Copilot 为代码文档、相关游戏功能和无障碍访问功能提供的建议。

## 安全性与 GitHub Copilot 云智能体

由于 Copilot 云智能体会在无人监督的情况下异步执行任务，因此我们设置了一些安全限制，以确保操作安全。这些限制包括：

- Copilot 仅对存储库具有读取权限，对其创建的代码分支具有写入权限。
- 云智能体在 GitHub Actions 中运行，并会创建一个独立的临时环境来工作。
- 运行任何 GitHub Actions 工作流前，都需要人工批准。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，MCP 服务器也包括在内。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个拉取请求 (PR)，其中包含为代码添加的文档。你将在 GitHub.com 上通过标准 PR 界面完成此任务。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这属于**预期行为**，因为 Copilot 默认只能有限地访问外部资源，包括外部 MCP 服务器。如果需要，可以[为 Copilot 云智能体自定义或禁用防火墙][agent-firewall]。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests**，打开拉取请求列表。
3. 打开标题类似于 **Add missing documentation** 的拉取请求。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求会带有 **[WIP]** 标记。请等待 Copilot 完成工作，这可能需要几分钟。你可以趁此休息片刻，或回顾目前学到的内容。

4. 拉取请求准备就绪后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新添加了 TSDoc 文档注释和其他文档的代码。实际更改内容会有所不同。

    浏览更改时，留意 TSDoc 文档注释、TypeScript 规范和注释头。这些内容来自你在练习 2 开始时查看的自定义指令文件。

6. 审查完更新并确认无误后，返回 **Conversation** 选项卡并向下滚动。
7. 你应该会看到一些工作流正在等待批准的提示。
8. 如果有工作流正在等待批准，请选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 你应该会看到工作流在拉取请求的检查部分排队运行。如果一切顺利，单体 Astro 应用程序的项目检查就会通过。这可能需要几分钟。

## 请求 GitHub Copilot 更改

与 Copilot 协作并非单向过程。你可以像提及团队成员一样在拉取请求评论或代码行内评论中提及 Copilot。Copilot 会读取这些评论并启动新会话来处理问题。由于结果具有非确定性，我们无法规定你应该提出什么具体要求。你可以考虑让 Copilot：

- 在每个代码文件顶部添加简要说明文件用途的注释头。
- 在 TypeScript 和 Astro 文件中添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用程序的结构。

1. 在代码文档相关的 PR 中添加评论，并像提及其他用户一样提及 **@copilot**，请求其进行更改。可以采用上面的建议，也可以提出其他希望 Copilot 在代码库文档中改进的内容。
2. 选择 **View Session**，观察 Copilot 执行工作。留意 Copilot 如何启动新会话以进行更新。
3. 选择 **Back to pull request**，返回拉取请求。

    ![返回拉取请求](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，拉取请求中应该会出现新的提交。
5. 选择 **Files changed** 选项卡，审查更改。

你可以继续迭代，直到满意为止。确认结果满意后，可以将 PR 从草稿转换为准备审查状态，然后合并到 main 分支。

![将 PR 转为准备审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

现在回到 Copilot 为处理游戏详情页面显示相关游戏的议题而创建的 PR。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似于 **Show related games on the game details page** 的 PR。
4. 选择 **Files changed** 选项卡，审查 Copilot 生成的代码。
5. 审查更新并确认无误后，返回 **Conversation** 选项卡并向下滚动。
6. 你应该会看到一些工作流正在等待批准的提示。
7. 如果有工作流正在等待批准，请选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

8. 你应该会看到工作流在拉取请求的检查部分排队运行。如果一切顺利，单体 Astro 应用程序的项目检查就会通过。这可能需要几分钟。
9. **可选：**你还可以在 Codespace 中切换到此分支，手动测试相关游戏功能。转到 Codespace，打开终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已经创建了相关游戏功能！与之前一样，你可以通过迭代让 Copilot 云智能体进行更改。例如，可以要求 Copilot 调整显示的相关游戏数量，或添加注释头和 TSDoc 文档注释（请记住，分配此任务时，你还没有更新自定义指令）。与之前一样，可以在 **Conversation** 选项卡中添加评论来提出更改请求，Copilot 会读取评论并启动新会话。

## 审查无障碍访问功能

最后，审查使用无障碍访问自定义智能体实现的功能。这个 PR 应同时包含你在练习 3 中分配的高对比度模式，以及你在练习 4 的智能体控制中心中提出的浅色模式。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似于 **Add high contrast mode to website** 的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求会带有 **[WIP]** 标记。请等待 Copilot 完成工作，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查 Copilot 生成的代码。
5. 审查实现，重点检查：
   - 用于切换模式的 UI 组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍访问属性（ARIA 标签、键盘导航等）。
   - 用于管理模式切换的 JavaScript/TypeScript 代码。

6. 审查更新并确认无误后，返回 **Conversation** 选项卡并向下滚动。
7. 你应该会看到一些工作流正在等待批准的提示。
8. 如果有工作流正在等待批准，请选择 **Approve and run workflows**。

   ![批准并运行工作流](../../../_images/shared-approve-workflows.png)

9. 你应该会看到工作流在拉取请求的检查部分排队运行。如果一切顺利，单体 Astro 应用程序的项目检查就会通过。这可能需要几分钟。
10. **可选：**你可以在 Codespace 中切换到此分支，手动测试无障碍访问功能。转到 Codespace，打开终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名称）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用程序，在浏览器中测试高对比度和浅色模式切换，确认功能按预期运行，并且在重新加载页面后仍会保留设置。

留意无障碍访问自定义智能体如何引导 Copilot 遵循无障碍最佳实践来实现这些功能。如果发现无障碍访问问题或可改进之处，可以像之前审查 PR 一样在评论中提及 **@copilot**，请求进行更新。

## 可选练习 — 继续委派任务

云智能体最适合处理实际待办事项，让你能转而处理其他工作。若要培养这种工作习惯，可以为存储库创建几个议题并分配给 Copilot。以下是一些想法：

- 在游戏详情页面创建支持者兴趣表单。
- 为游戏列表页面实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云智能体练习。在这些课程中，你：

- **查看了存储库附带的自定义指令文件**，以便之后观察它们对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，观察它设置环境、制定计划并异步执行任务。
- **创建并使用自定义智能体**进行无障碍访问改进，添加高对比度和浅色模式切换功能。
- **使用 Copilot 智能体页面作为控制中心**，监控并引导无障碍访问会话。
- **审查并迭代改进云智能体的拉取请求**，提及 `@copilot` 请求更改并批准工作流。

## 回顾和后续步骤

你已完成云智能体练习。如果还想继续探索，其他练习可以补充你在这里学到的内容：

- 🖥️ **[VS Code 练习](../../vscode/)** — 在 IDE 中直接探索 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 练习](../../cli/)** — 在终端中使用 Plan 和 Autopilot 模式、智能体技能、自定义 QA 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接，交付两个经审查的更改。

在自己的存储库中，还可以尝试以下后续任务：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为其他技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
