---
title: "练习 5 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义智能体][previous-lesson] |
|:--|

启用 GitHub Copilot 智能体模式后，它会自主探索代码库、提出更改、编辑文件并运行命令。由于这些工作会在你的计算机上实时进行，VS Code 中的 Copilot Chat 会实时显示每次工具调用和文件编辑。你可以在行内查看每个差异、接受或拒绝单个更改，并使用后续提示引导对话、完善或扩展工作，而无需离开编辑器。

在本练习中，你将：

- 实时监控无障碍访问智能体的工作。
- 审查并接受建议的文件编辑。
- 在智能体工作过程中引导它添加浅色模式切换开关，以及已有的高对比度模式。

## 场景

你在[练习 4][previous-lesson]中使用的无障碍访问自定义智能体正在实现高对比度模式。工作进行时，设计团队又提出了一项需求：他们也希望提供浅色模式切换开关，供觉得默认主题太暗的用户使用。你无需重新开始新的对话，而是可以引导当前会话扩展现有工作。

## 监控 Copilot 的进度

Copilot Chat 视图会显示智能体执行的每个步骤，包括探索的文件、运行的命令和提出的编辑。每个文件编辑都会在 Chat 中以内联差异的形式显示，并提供 **Keep** / **Undo** 控件。

1. 返回练习 4 中打开的 Copilot Chat 视图。
2. 智能体工作时，滚动 Chat 查看它执行的每次工具调用。你会看到文件读取、文件编辑以及需要运行的终端命令。
3. 智能体提出文件编辑时，差异会以内联方式显示：
    - 选择 **Keep** 接受更改。
    - 选择 **Undo** 撤销更改，让智能体重新尝试。
4. 也可以打开 Chat 顶部的 **Files changed** 指示器，查看智能体在本次会话中修改的完整文件列表。

> [!NOTE]
> 如果工具调用请求权限（例如运行终端命令），智能体会暂停并显示 **Allow** 提示。只批准你认可的命令。

5. 等待智能体完成高对比度模式的实现。完成后应会显示总结更改内容的最终消息。

## 引导智能体添加浅色模式

高对比度模式已就绪，现在请在同一对话中扩展工作，添加浅色模式切换开关。由于继续使用同一 Chat 会话，智能体会保留前面工作的所有上下文，包括修改的组件、使用的样式方案和设置的本地存储模式。

1. 在 Copilot Chat 输入框中发送以下后续提示：

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. 智能体会继续之前的工作，探索已完成的更改并提出浅色模式实现方案。
3. 像审查高对比度模式一样，逐项审查新增编辑。使用 **Keep** 或 **Undo** 处理每个差异。
4. 如果智能体的实现方向不符合预期，例如试图以你不喜欢的方式重构切换 UI，可以选择 Chat 输入框旁边的 **Stop** 按钮停止操作，再发送澄清提示。

> [!TIP]
> 引导正在进行的会话比从头开始更快。可以使用后续提示要求调整（“简化 CSS，使用 CSS 变量而不是重复选择器”）、纠正方向（“不要添加第三个开关，请将浅色模式整合到现有设置面板”）或扩展范围（“同时为两个开关添加键盘快捷键”）。

## 审查工作文件

提交工作前，快速检查智能体修改的所有内容。

1. 在 VS Code 中打开 **Source Control** 视图。
2. 审查已更改文件的完整列表。你应该会看到 Astro 组件、样式和相关测试的更新。
3. 打开几个已更改的文件并查看差异。确认其中体现了自定义智能体要求的无障碍模式，包括 ARIA 属性、键盘导航、语义化 HTML 和本地存储设置。
4. 确认满意后，在 Source Control 面板中暂存并提交更改。下一课会发布这些更改。

## 总结和后续步骤

你使用 Copilot Chat 智能体模式监控并引导了正在进行的会话：审查逐项加入的文件编辑、接受或拒绝更改，并发送后续提示扩展工作，同时保留上下文。

在本课中，你了解了：

- 实时监控智能体的工作。
- 接受或拒绝单个文件编辑。
- 使用后续提示引导正在进行的会话。

在[下一课][next-lesson]中，你将把无障碍访问更改作为拉取请求发布，并审查本练习中本地自定义智能体所做的更改。

## 资源

- [VS Code 中的 Copilot Chat][copilot-chat-vscode]
- [使用智能体模式][agent-mode]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
