---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几项练习中，你让 Copilot 云智能体处理了三项任务，目标是改进用户体验和添加功能。云智能体以异步方式自主工作，但监控这些任务仍然很重要。

你可以使用多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个控制中心，你可以查看所有具有未关闭拉取请求 (PR) 的智能体任务，了解智能体执行的操作，甚至可以引导正在进行的会话。

在本课中，你将：

- 浏览智能体页面，监控云智能体任务。
- 引导正在进行的会话，请求添加其他功能。

## 场景

将任务分配给智能体以创建高对比度模式后，团队意识到也可以顺便添加浅色模式。由于已经在更新网站样式并添加切换功能，因此同时实现这项功能很合理。你将引导智能体的工作，确保它同时添加浅色模式和高对比度模式。

## 审查 Copilot 云智能体任务

查看当前分配给 Copilot 云智能体的所有任务的状态。

1. 转到 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主面板和左侧面板中的任务列表。你应能看到自己分配给 Copilot 的任务，包括：
    - 更新代码文档。
    - 生成用于修改游戏的 API。
    - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的任务，例如：
    - 从存储库检出代码。
    - 为 Copilot 创建工作环境。
    - 设置 MCP 服务器。
    - 执行完成分配任务所需的各项步骤。

> [!NOTE]
> 具体显示的步骤因 Copilot 的工作状态和执行方式而异。

4. 还要留意右侧出现的拉取请求 (PR) 面板。你可以在其中查看 PR 和已更改的文件，以便进一步监控任务。

## 引导云智能体

了解正在进行的任务后，接下来请在智能体处理高对比度模式时要求它添加浅色模式切换开关。

1. 选择与添加高对比度模式相关的会话。具体标题取决于 Copilot 使用的名称和当前工作状态。

    ![控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到会话显示已完成设置并开始工作。看到类似下方的消息时，就表示进入了此阶段。
3. 在 **Steer active session while Copilot is working** 对话框中，添加以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![智能体页面上突出显示引导活动会话对话框的云智能体任务截图](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 留意 Copilot 如何确认收到提示并将其加入工作流程。

## 让 Copilot 继续工作

与之前一样，Copilot 会继续处理更新后的任务！完成你发送消息时正在执行的具体步骤后，它会将新请求加入工作流程。

与前面一样，这需要几分钟。你可以暂停片刻，回顾目前学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot 智能体页面，即监控和引导 GitHub Copilot 云智能体任务的中心位置。你可以使用这个控制中心跟踪所有正在进行和已完成的任务、审查智能体执行的工作，甚至重新引导正在进行的任务以调整范围或补充说明。

你了解了以下概念：

- 使用控制中心和智能体页面监控云智能体任务。
- 引导正在进行的会话以请求添加其他功能。

Copilot 正在完成无障碍访问功能，接下来请[迭代改进 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
