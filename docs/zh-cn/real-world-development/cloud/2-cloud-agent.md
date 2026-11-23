---
title: "练习 2 - GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义指令][previous-lesson] |
|:--|

几乎所有组织都会遇到技术债务问题。这可能是尚未解决的安全问题、需要更新的旧代码，也可能是因缺少时间而长期搁置的功能请求。GitHub Copilot 云智能体旨在自主执行更新代码、添加功能等任务。智能体完成工作后，会创建一个草稿 PR，供开发者审查。这样可以把繁琐的任务交给智能体，加快开发流程，让开发者有更多时间专注于更重要的工作。

你将在本课中了解如何使用 Copilot 云智能体：

- 自定义生成代码的环境。
- 确保安全地执行操作。
- 编写范围明确的议题。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 有一些技术债务需要处理。最初受雇开发网站的承包商没有留下合适的文档——事实上，你会发现项目完全缺少文档。团队希望首先为应用程序中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队已经准备好改进游戏发现体验。他们希望每个游戏的详情页面都显示相关游戏，也就是同一类别中的其他游戏，以便用户继续浏览。当前不需要完善的实现，只需要能用于 UX 验收测试的版本。这项工作目前不是阻塞项，优先级还有更高的议题。

这两项任务都可能很快被降级为低优先级，因此很适合分配给 Copilot 云智能体。Copilot 云智能体可以异步处理任务，让开发者专注于其他工作，之后再回来审查 Copilot 的成果并确认其符合预期。

## 认识 GitHub Copilot 云智能体

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)可以像开发者一样在后台执行任务。就像与开发者协作一样，你可以通过多种方式分配任务，包括[将 GitHub 议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配任务后，Copilot 会创建草稿拉取请求以跟踪进度、设置工作环境，并开始处理任务。你可以在 Copilot 会话进行期间或完成后查看其中的工作。待解决方案可供审查时，Copilot 会在拉取请求中提及你。

## 编写范围明确的指令

GitHub Copilot 并非魔法工具——使用它并不意味着可以跳过思考。看似简单的操作往往也有复杂之处，因此[为 Copilot 云智能体设定任务范围时要谨慎][cloud-agent-best-practices]。把它当作 AI 结对编程伙伴：分阶段工作、不断学习、进行试验并根据结果调整。加入生成式 AI 并不会改变软件开发的基本原则。

## 本存储库中的自定义指令

前面的练习介绍了自定义指令及其如何引导 Copilot。如果你已经完成了自定义指令练习，就会看到 `.github/copilot-instructions.md` 的实际效果；如果还没有，现在可以快速查看一下。将工作分配给 Copilot 云智能体之前，先以只读方式查看存储库中已有的指令文件，稍后便能观察到它们的影响。

在 GitHub 网页界面中打开以下文件；如果已启动 codespace，也可以在那里查看：

- `.github/copilot-instructions.md` - 查看 **Code standards** 部分，尤其要留意 TypeScript 规范和 TSDoc 文档注释要求。
- `.github/instructions/unit-tests.instructions.md` - 留意 `applyTo` frontmatter，它将指令限定在 `**/*.test.ts` 文件中。

下一部分将 **Code lacks documentation** 议题分配给云智能体时，留意它创建的拉取请求中是否包含 TSDoc 文档注释、TypeScript 规范和注释头。这些内容来自上述指令文件。后续练习会再次提醒你检查这些内容。

## 为 Copilot 云智能体设置开发环境

无论由谁编写代码，通常都需要特定环境并运行一些设置脚本，以确保环境正常。将任务分配给以类似软件工程师 (SWE) 方式工作的 Copilot 时也是如此。

云智能体通过 [GitHub Actions][github-actions] 执行工作。你可以在 `.github/workflows/copilot-setup-steps.yml` 文件中创建并配置[专用设置工作流][setup-workflow]，让它在云智能体开始工作前运行。这能确保它可以使用所需的开发工具和依赖项。为了方便练习并确保学习过程顺利，此工作流已预先配置。它会确保 Copilot 可以使用 Node.js、项目依赖项、端到端测试所需的浏览器二进制文件，以及单体 Astro 应用程序已迁移并填充数据的 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 可以从存储库的“Actions”选项卡测试设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 仅授予设置步骤所需的最低权限。Copilot 会获得用于自身操作的独立令牌。
    permissions:
      # 例如，如果要在设置步骤中克隆存储库以安装依赖项，需要 contents: read 权限。如果设置步骤不克隆存储库，Copilot 会在步骤完成后自动克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端/应用设置 - Node.js（整个应用现在都是 Astro + Drizzle/libSQL）
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 迁移并填充本地 SQLite 数据库，以便构建和测试时有数据可用。
      - name: Set up the database
        run: npm run db:setup
```

此文件看起来与其他 GitHub 工作流类似，但有几点需要注意：

- 它仅包含一个名为 `copilot-setup-steps` 的作业。Copilot 开始处理拉取请求前，GitHub Actions 会先运行此作业。
- 留意 `workflow_dispatch` 触发器。它允许你从存储库的 **Actions** 选项卡手动运行工作流，以便测试其能否成功运行，而不必等待 Copilot 触发它。

## 添加文档

大家都知道文档很重要，但大多数项目的文档要么已过时，要么完全缺失。这类技术债务经常无人处理，会降低工作效率，增加维护代码库或让新开发者加入团队的难度。Copilot 很擅长编写文档，因此这正是适合分配给 Copilot 云智能体的任务。它会在后台生成所需文档。后续练习中，你会回来审查这些成果。

1. 在新的浏览器选项卡中，转到 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新建议题对话框。
4. 选择 **Blank issue** 新建空白议题。
5. 将 **Title** 设置为 `Code lacks documentation`。
6. 将 **Description** 设置为：

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

  ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。
10. 选择 **Pull Requests** 选项卡。
11. 打开刚创建的拉取请求 (PR)，其标题可能类似于 `[WIP]: Code lacks documentation`。如果列表中没有出现新 PR，请稍等片刻并刷新浏览器窗口。
12. 几分钟后，你应该会看到 Copilot 创建的待办事项列表。

> [!NOTE]
> Copilot 的待办事项列表可能需要几分钟才会出现在 PR 中。Copilot 正在创建工作环境（运行前面介绍的工作流）、分析项目并确定解决问题的最佳方法。

13. 查看列表及其计划完成的任务。
14. 向下滚动拉取请求时间线，你应该会看到 Copilot 已开始处理此议题的更新。
15. 选择 **View session** 按钮。

  ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 你可能需要刷新窗口才能看到更新后的状态指示器。

16. 留意实时会话中的内容，以及 Copilot 如何解决问题。它会探索代码并了解当前状态，暂停思考并决定合适的计划，然后编写代码。

这可能需要几分钟。Copilot 云智能体的主要优势之一是能异步处理任务，让我们有时间专注于其他事情。接下来，我们会利用这一点：先给 Copilot 云智能体分配另一个任务，然后编写应用程序代码来添加功能。

## 为游戏详情页面添加相关游戏部分

如前所述，GitHub Copilot 云智能体的一大优势是可以拆分工作：你可以专注于一组任务，而它同时处理另一组任务。为设计团队添加相关游戏部分可能不会花很长时间，但也仍会占用你处理其他工作的时间。我们来把它分配给 Copilot 云智能体！

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新建议题对话框。
4. 选择 **Blank issue** 使用空白模板。
5. 将 **Title** 设置为 `Show related games on the game details page`。
6. 将 **Description** 设置为：

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

  ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

稍后你会在议题的第一条评论中看到一组 👀，表示 Copilot 已开始处理！

![Copilot 使用眼睛表情符号表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在认真处理第二项请求！Copilot 云智能体以与软件工程师相似的方式工作，因此你无需一直监控它；等任务完成后再审查即可。接下来我们来创建并使用自定义智能体。

## 总结和后续步骤

本课介绍了 [GitHub Copilot 云智能体][copilot-agents]。你可以将议题分配给云智能体，让它异步处理任务。Copilot 可以帮助处理技术债务、创建新功能，或协助将代码从一个框架迁移到另一个框架。

你了解了以下概念：

- 自定义生成代码的环境。
- 确保安全地执行操作。
- 编写范围明确的议题。
- 将议题分配给 Copilot。

云智能体正在后台处理任务，现在我们可以转而创建和使用自定义智能体。[Copilot 云智能体也可以使用 MCP 服务器][cloud-agent-mcp]，并且可以读取自定义指令；我们已在之前的模块中介绍过这些内容。

## 资源

- [关于 Copilot 云智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
