---
title: "练习 1 - 自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或者 Copilot 需要了解一些背景信息，就要确保它能获取这些上下文。[指令文件][instruction-files]用于提供此类指导，让 Copilot 不仅了解你希望它做什么，也了解应该如何完成。

在本练习中，你将：

- 了解如何通过存储库自定义指令和按路径指定的指令文件，将项目上下文、编码指南和文档规范提供给 Copilot。
- 在 `.github/copilot-instructions.md` 中添加一条新的存储库级规范。

> [!NOTE]
> 与 VS Code 和 CLI 练习不同，本练习不会比较提示的前后效果。Copilot 云智能体会异步处理 GitHub 议题，因此难以实时并排展示指令的影响。稍后审查云智能体创建的拉取请求时，你会看到指令文件的作用。

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

- `.github/copilot-instructions.md` 是一个指令文件，会随存储库的**每个**请求发送给 Copilot。此文件应包含项目级信息，即大多数 Copilot Chat 或 CLI 请求都适用的上下文，例如技术栈、项目概述、最佳实践和全局指导。
- `.github/instructions/*.instructions.md` 可针对特定任务或文件类型创建。例如，可为 TypeScript 或 Astro 编写指南，也可为创建 UI 组件或单元测试提供指导。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 代码生成，不适用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时都会使用存储库级指令，以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> 最后，Copilot 还[支持其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

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

## 添加新的存储库规范

接下来要编辑一次文件：添加一条项目级规则，要求使用 TSDoc 文档注释和文件级注释头记录代码文档。云智能体稍后处理本练习中分配的议题时会遵循这条规则。

编辑前，先创建一个分支（云智能体会读取议题目标分支中的指令，但你仍应在独立分支中提交更改）：

1. 在 codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

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

## 提交、推送并合并指令更新

云智能体会读取议题目标分支中的指令。下一练习中，你会将议题分配给 Copilot，届时 Copilot 会从 `main` 分支创建新分支。因此，必须先将指令更改合并到 `main`，云智能体才能使用。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上打开从 `custom-instructions-cloud` 到 `main` 的拉取请求并将其合并。这样，云智能体在下一练习中处理议题时就会读取这些指令。

> [!TIP]
> 如果希望在本次研讨会中直接使用 `main`，可以跳过分支步骤并直接提交到 `main`。此处创建分支是为了让练习更贴近真实项目的工作方式。

## 总结和后续步骤

你了解了 Copilot 如何读取本项目的指令文件，并在 `.github/copilot-instructions.md` 中添加了新的存储库级规范。接下来，你会在本练习余下的内容中看到云智能体创建的拉取请求如何遵循此规范。

接下来，将[第一个议题分配给 Copilot 云智能体][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot — 指令文件和其他资源合集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
