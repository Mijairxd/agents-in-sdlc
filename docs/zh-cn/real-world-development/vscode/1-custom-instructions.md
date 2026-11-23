---
title: "练习 1 - 自定义指令（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或者 Copilot 需要了解一些背景信息，就要确保它能获取这些上下文。你可以通过多种方式向 Copilot 提供具体上下文，其中一种重要方式是使用[指令文件][instruction-files]来指导代码生成。

在本练习中，你将：

- 了解如何通过存储库自定义指令和按路径指定的指令文件，将项目上下文、编码指南和文档规范提供给 Copilot。
- 在当前指令的帮助下，生成用于筛选功能的第一个数据切片（发布者辅助函数）。
- 在 `.github/copilot-instructions.md` 中添加一条新的存储库级规范。
- 再次运行相同提示，观察生成的代码如何遵循新规范。
- 将指令更新和筛选功能切片提交到 `main`，以便 Copilot 在下一练习中使用更新后的指引。

> [!CAUTION]
> 生成的代码可能不符合你设定的部分规范，因为 Copilot 的输出具有非确定性。本练习的重点是观察更新指令前后 Copilot 行为的*趋势*，而不是要求输出逐字一致。

## 指令文件

### 场景

Tailspin Toys 和优秀的软件开发团队一样，制定了一系列开发规范和要求，包括：

- 数据层始终需要单元测试。
- UI 应采用暗色模式并具有现代感。
- 应通过 TSDoc 文档注释为代码添加说明。
- 每个文件开头都应添加一段注释，说明文件的用途。

使用指令文件，确保 Copilot 了解这些实践要求，并能据此完成任务。

### 自定义指令

自定义指令可向 Copilot 提供上下文和偏好，帮助它了解你的编码风格和要求。借助此功能，你可以引导 Copilot 提供更符合需求的建议和代码片段。你可以指定偏好的编码规范、库，甚至希望添加的注释类型。指令既可以适用于整个存储库，也可以针对特定文件类型，为具体任务提供上下文。

指令文件有两种类型：

- `.github/copilot-instructions.md` 是一个指令文件，会随存储库的**每个**请求发送给 Copilot。此文件应包含项目级信息，即大多数 Copilot 请求都适用的上下文，例如项目技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md` 可针对特定任务或文件类型创建。例如，可为 TypeScript 或 Astro 编写指南，也可为创建 UI 组件或单元测试提供指导。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 代码生成，不适用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用存储库级指令，以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

本练习无法全面介绍如何创建指令文件。不过，示例项目展示了一种有代表性的方法。总体而言：

- 将 `copilot-instructions.md` 中的指引限定为项目级内容，例如项目描述、项目结构和全局编码规范。
- 使用 `*.instructions.md` 为特定文件类型（如单元测试、Astro 组件和数据层）或特定任务提供专门指令。
- 使用自然语言，确保说明清晰，并提供代码示例说明应该和不应该采用的写法。

创建指令文件没有唯一的方法，使用 AI 也是如此。通过实践，你会找到最适合自己项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应具备完善的指令文件。浏览本项目中的指令文件时，你可能会发现有些文件专门用于[更新 UI][ui-instructions]和 [Astro][astro-instructions] 等任务。
>
> Copilot 也可以帮你生成指令文件。不同产品界面的操作方式有所不同（例如，VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`）；当前练习会在相关步骤中介绍对应操作。
>
> 想查找模板或起点？请浏览包含指令文件、自定义智能体和其他资源的存储库 [awesome-copilot][awesome-copilot]。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看本项目中的自定义指令文件

花点时间阅读存储库自带的指令文件：其中有一个核心文件 `copilot-instructions.md`，以及一系列适用于不同任务的 `*.instructions.md` 文件。你可以在编辑器或 GitHub 网页界面中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 查看文件，留意项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。注意 **Code standards** 下还有 **GitHub Actions Workflows** 子部分。这些内容适用于你与 Copilot 的任何交互。
3. 打开 `.github/instructions` 文件夹并浏览其中内容。注意这里有 Astro 文件、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它设置相对于存储库根目录的 glob，用于确定指令适用的文件。例如，任何匹配 `**/*.test.ts` 的 TypeScript 测试文件都会匹配。
5. 留意该文件中有关为本项目创建单元测试的具体指令。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到末尾。留意其中指向其他指令文件（如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成更小、可重复使用的文件，并为 Copilot 提供可参考的示例。这里的路径相对于指令文件，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目的编码规范，但尚未要求在代码中添加文档注释。接下来的步骤会添加 TSDoc 文档注释和文件注释头的规则。

## 为更改创建分支

遵循最佳实践，为本次更改创建分支。

1. 返回上一练习中使用的 codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新指令之前先使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 codespace 并打开 Copilot Chat 面板，然后选择 **New Chat** 开始一个新对话。每个练习会根据需要说明模式和模型的选择方式。

若要了解自定义指令的影响，先在当前指令文件下发送提示。稍后更新指令后，再次发送相同提示，观察结果变化。

1. 关闭之前练习留下的编辑器选项卡，避免 Copilot 获取不必要的上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道辅助函数应放在哪里。
3. 在 Chat 视图的智能体下拉列表中选择 **Agent**，以便 Copilot 应用文件更改。

   ![Chat 视图中智能体选择器的截图。](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot 会探索项目并应用代码更新，通常会同时修改辅助函数文件及其测试。
6. 留意生成的辅助函数是一个类型化函数：它将 `db` 客户端作为第一个参数，并返回类型化的发布者数组。这是 `.github/instructions/drizzle.instructions.md` 中数据层规范的作用，该文件适用于 `src/lib/*.ts`。
7. 留意生成的代码**缺少** TSDoc 文档注释和文件级注释头。

> [!CAUTION]
> Copilot 的输出具有非确定性，因此它也可能在没有相关指令时添加文档注释。如果出现这种情况也没关系，本练习的重点仍然是观察更新指令后行为的一致性变化。

## 添加新的存储库规范

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。我们来补充存储库的编码规范，以便 Copilot 提供更好的代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分，该部分应位于第 27 行附近。注意其中记录了项目编码规范，但尚无代码文档规则，这也是之前生成的辅助函数没有文档注释的原因。
3. 在现有规范下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，指令文件既可以放在存储库级文件 `.github/copilot-instructions.md` 中提供全局指导，也可以放在 `*.instructions.md` 文件中，针对特定语言、文件类型或任务提供指导。存储库级文件适合记录诸如文档注释规则之类的项目级规范。

## 重新运行提示并观察变化

1. 返回 Copilot Chat 并选择 **New Chat** 清除对话内容。
2. 再次打开 `src/lib/publishers.ts`，让 Copilot 聚焦于正确的文件。
3. 发送与之前相同的提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 留意生成的文件现在是否以类似以下注释块开头：

   ```typescript
   /**
    * Tailspin Toys 众筹平台的发布者数据访问辅助函数。
    * 提供从数据库检索发布者信息的函数。
    */
   ```

5. 留意生成的函数现在是否包含类似以下内容的 TSDoc 注释：

   ```typescript
   /**
    * 返回所有发布者的 ID 和名称列表。
    *
    * @param db - Drizzle 数据库客户端。
    * @returns 一个 Promise，解析为发布者对象数组。
    */
   ```

你刚刚引导 Copilot 遵循新的项目规范，并将其应用到真实代码中；下一练习会在此基础上继续构建。

## 提交指令并推送分支

指令文件与其他项目文件一样，都应通过源代码管理进行维护。接下来将它们提交并推送到存储库。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
2. 在终端中运行以下命令，确认指令和辅助函数更改已存在：

   ```bash
   git status
   ```

3. 在终端中暂存并提交指令更新，以及 Copilot 为辅助函数基础所做的所有更改：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # 如果 git status 显示还有其他配套更改（例如测试），也要添加这些文件。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 在终端中将分支推送到存储库：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支推送完成后，创建拉取请求并关联到待办事项中的文档规范议题。你可以手动操作，不过也可以让 Copilot 使用已连接的 GitHub 工具查找议题、创建关联 PR，然后合并 PR。

> [!NOTE]
> 这是首次让 Copilot 代表你在 GitHub 上操作。项目模板已将 GitHub 工具连接到工作区，因此无需额外设置。Copilot 首次使用这些工具时，VS Code 可能会提示你登录 GitHub；按照提示完成登录即可。后续练习会介绍此连接的工作方式（模型上下文协议）。

1. 在 codespace 中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图，并确保在智能体选择器中选中 **Agent**。
3. 请 Copilot 查找与更新指令文件相关的议题，并从当前分支创建 PR，说明指令更新和新增的发布者辅助函数基础：

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot 会开始查找议题并创建 PR。
5. 如果系统提示你 **Allow** Copilot 代表你执行 GitHub 操作，请审查操作并酌情选择 **Allow**。
6. 创建 PR 后，要求 Copilot 合并 PR 并将分支切回 main：

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. 如果系统提示你 **Allow** Copilot 代表你执行 GitHub 操作和 shell 命令，请审查操作并酌情选择 **Allow**。

现在，你已借助 GitHub Copilot 创建并合并了拉取请求！

## 总结和后续步骤

你了解了 Copilot 如何读取本项目的指令文件，并使用 VS Code 中的 Copilot Chat 完成以下任务：

- 发送代码生成提示，观察 Copilot 在现有指令下生成的内容。
- 在 `.github/copilot-instructions.md` 中添加新的存储库级规范。
- 再次发送相同提示，观察生成的代码如何遵循新规范。
- 将指令更新和辅助函数基础提交到 `main`，以便下一练习继续使用。

接下来，让 Copilot 在[智能体模式][next-lesson]中运用这些指令，跨代码库添加新功能。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义指令][personal-instructions]
- [Awesome Copilot — 指令文件和其他资源合集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
