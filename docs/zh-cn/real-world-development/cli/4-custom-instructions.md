---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "浏览存储库指令、添加文档规范，并将其应用到筛选代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，就要确保 Copilot 能获取相应指导。[指令文件][instruction-files]不仅能说明你希望编写什么代码，还能说明代码应如何组织。现在你已构建筛选功能，接下来将查看 Copilot 使用的指令、添加一项文档规范，并将其应用到代码中。

在本课中，你将：

- 了解存储库指令和按路径指定的指令文件如何传递给智能体。
- 更新指令文件，确保遵循编码规范。
- 查看指令文件对代码的影响。

## 场景

Tailspin Toys 和优秀的软件开发团队一样，制定了一系列开发规范和要求，包括：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值（如适用，也包括可注入的 `db` 参数）。
- 可重复使用的 Astro 组件应说明其 `Props` 接口；相关代码更改时，注释也必须同步更新。
- 保留现有格式和 lint 指南。

借助指令文件，确保 Copilot 了解这些实践要求，并能据此完成任务。

## 指令文件

自定义指令可向 Copilot 提供上下文和偏好，帮助它了解你的编码风格和要求。借助此功能，你可以引导 Copilot 提供更符合需求的建议和代码片段。你可以指定偏好的编码规范、库，甚至希望添加的注释类型。指令既可以适用于整个存储库，也可以针对特定文件类型，为具体任务提供上下文。

指令文件有两种类型：

- `.github/copilot-instructions.md` 是一个指令文件，会随存储库的**每个**请求发送给 Copilot。此文件应包含对大多数请求都适用的项目级信息。
- `.github/instructions/*.instructions.md` 可针对特定语言、文件类型或任务提供指引。

> [!NOTE]
> 其他指令格式及其支持情况因环境而异。依赖特定格式前，请查看[自定义指令支持参考][custom-instructions-support]。

## 查看本项目中的自定义指令文件

起始项目中已包含一些指令文件。先浏览这些内容，再进行更改，以便了解更改的影响。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（而不是终端）中打开 `.github/copilot-instructions.md`。
3. 查看项目简介和编码指导。此文件中的指令适用于你在此存储库中与 Copilot 的所有交互。
4. 打开 `.github/instructions` 文件夹并浏览其中的文件。注意这里有 Astro 文件、Drizzle 数据层、测试等方面的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` frontmatter，它设置指令适用文件的 glob 模式。
6. 打开 `.github/instructions/drizzle.instructions.md`，留意它指向其他指令文件和项目现有文件的链接。

## 更新指令文件以符合团队规范

虽然现有文件已经是很好的起点，但仍有缺失内容。接下来修改核心文件 `copilot-instructions.md`，确保新生成的 TypeScript 包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分，该部分应位于第 35 行附近。
2. 在最后一条要点下方添加以下内容：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存！

## 使用更新后的指导

Copilot CLI 会在每次对话启动时读取存储库指令。保存更新后的指令后，退出并恢复筛选会话，这样 Copilot 就能在保留功能上下文的同时加载新指令。

1. 如果筛选对话仍处于打开状态，输入 `/exit` 退出。Copilot CLI 会自动保存对话。
2. 在 `game-filters-cli` 分支的存储库根目录中，恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果系统提示，请选择筛选对话，并确认检出的是 `game-filters-cli` 分支。
3. 请 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff` 并查看更改的 TypeScript 文件。留意新生成的 TSDoc 注释，并确认它们准确说明了代码。

## 总结和后续步骤

你了解了 Copilot 如何读取指令文件，并将新规范应用到功能中。具体来说，你：

- 了解存储库指令和按路径指定的指令文件如何传递给智能体。
- 更新了指令文件，确保遵循编码规范。
- 查看了指令文件对代码的影响。

接下来，[自定义并运行可重复使用的 quality-checks 技能][next-lesson]，确保以一致的方式运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot — 指令文件和其他资源合集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
