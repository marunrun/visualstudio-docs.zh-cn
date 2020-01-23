---
title: 提高 .NET 开发工作效率
description: 概述导航、代码分析、单元测试和其他功能，帮助提升编写 .NET 代码的速度和质量。
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.date: 11/21/2019
ms.topic: conceptual
helpviewer_keywords:
- editor
ms.workload:
- dotnet
ms.openlocfilehash: 0aa8e19f2be78671587dd1d9bc6254306c82a78c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75567497"
---
# <a name="visual-studio-productivity-guide-for-c-developers"></a>面向 C# 开发人员的 Visual Studio 工作效率指南

了解 Visual Studio 如何提高开发人员的工作效率。 充分利用性能和生产效率改进，如：导航到反编译程序集、键入时的变量名称建议、“测试资源管理器”中的层次结构视图、“转到全部”(Ctrl+T) 导航到文件/类型/成员/符号声明、智能“异常帮助程序”、代码样式配置和执行、以及众多重构和代码修补程序     。

## <a name="im-used-to-keyboard-shortcuts-from-a-different-editor"></a>我已经习惯了不同编辑器的键盘快捷方式

::: moniker range="vs-2017"

**Visual Studio 2017 版本 15.8 中的新增内容**

::: moniker-end

如果来自其他 IDE 或编码环境，可将键盘方案更改为 Visual Studio Code  或 ReSharper (Visual Studio)  ：

![Visual Studio 中的键盘方案](../ide/media/VS2017Guide-Keyboard.png)

某些扩展也提供键盘方案：

- [适用于 Visual Studio 的 HotKeys (ReSharper/IntelliJ)](https://marketplace.visualstudio.com/items?itemName=JustinClareburtMSFT.HotKeys)
- [Emacs 模拟](https://marketplace.visualstudio.com/items?itemName=JustinClareburtMSFT.EmacsEmulation)
- [VSVim](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim)

Visual Studio 常用快捷方式如下：

| 快捷方式（所有配置文件） | 命令 | 描述 |
|-|-|-|
|  Ctrl + T  | 转到全部 | 导航到任何文件、类型、成员或符号声明 |
| F12（也可使用 Ctrl+单击    ） | 转到定义 | 导航到定义符号的位置 |
| Ctrl+F12   | 转到实现 | 从基类型或基成员导航到各种实现 |
| Shift+F12   | 查找所有引用 | 查看所有符号或文本引用 |
|  Alt + Home  | 转到基类 | 向上导航继承链 |
| Ctrl+.   （也可使用 C# 配置文件中的 Alt+Enter   ） | 快速操作和重构 | 查看光标位置或代码选定内容处可用的代码修复、代码生成操作、重构或其他快速操作 |
| **Ctrl**+**D** | 复制行 | 复制光标所在的代码行（适用于 Visual Studio 2017 版本 15.6  及更高版本） |
| **Shift**+**Alt**+ **+** / **-** | 扩大/收缩选定内容 | 在编辑器中扩大或收缩当前选定内容（适用于 Visual Studio 2017 版本 15.5 及更高版本）  |
| **Shift** + **Alt** +  **.** | 插入下一个匹配的脱字号 | 在与当前选择匹配的下一个位置添加选择和脱字号（适用于 Visual Studio 2017 版本 15.8 及更高版本）  |
| Ctrl+Q   | 搜索 | 搜索所有 Visual Studio 设置 |
| **F5** | 开始调试 | 开始调试应用程序 |
| Ctrl+F5   | 不进行调试直接运行 | 不进行调试，直接在本地运行应用程序 |
| Ctrl+K,D（默认配置文件）或 Ctrl+E,D（C# 配置文件）       | 设置文档的格式 | 基于换行、间距和缩进设置，清理文件中的格式设置冲突 |
| Ctrl+\\、Ctrl+E（默认配置文件）或 Ctrl+W,E（C# 配置文件）        | 查看错误列表 | 查看文档、项目或解决方案中的所有错误 |
| **Alt** + **PgUp/PgDn** | 转到下一个/上一个问题 | 跳转到文档中的上一个/下一个错误、警告和建议（适用于 Visual Studio 2017 版本 15.8 及更高版本）  |
| Ctrl+K，/    | 切换单行注释/取消注释 | 此命令将添加或删除单行注释，具体取决于选定内容是否已添加注释 |
| Ctrl+Shift+/    | 切换块注释/取消注释 | 此命令将添加或删除块注释，具体取决于所选内容 |

> [!NOTE]
> 一些扩展取消绑定默认的 Visual Studio 键绑定。 若要使用以上命令，请按以下方式将键绑定还原为 Visual Studio 默认设置：转到“工具” > “导入和导出设置” > “重置所有设置”，或转到“工具” > “选项” > “键盘” > “重置”        。

有关键盘快捷方式和命令的详细信息，请参阅[高效工作快捷方式](../ide/productivity-shortcuts.md)和[常用键盘快捷方式](default-keyboard-shortcuts-for-frequently-used-commands-in-visual-studio.md)。

## <a name="navigate-quickly-to-files-or-types"></a>快速导航到文件或类型

Visual Studio 有一种名为“转到全部”(Ctrl+T) 的功能    。 通过“转到全部”  可快速跳转到任何文件、类型、成员或符号声明。

- 更改此搜索栏的位置或使用“齿轮”  图标关闭“实时导航预览”。
- 使用语法（如 `t mytype`）筛选结果。
- 将搜索范围限定在当前文档。
- 支持 Camelcase 匹配。

![Visual Studio 中的转到全部](../ide/media/VS2017Guide-go-to-all.png)

## <a name="enforce-code-style-rules"></a>强制实施代码样式规则

可以使用 EditorConfig 文件编写编码约定，并使其跟随源。

![Visual Studio 中的代码样式实施](../ide/media/VSGuide_CodeStyle.png)

- 选择“添加” > “新建项目”，向项目添加默认的或 .NET 样式的 EditorConfig 文件。   在“添加新项目”对话框中，搜索“editorconfig”。  选择任意一个“editorconfig 文件”项模板，然后选择“添加”。  

   ![Visual Studio 中的 EditorConfig 项模板](media/editorconfig-item-templates.png)

::: moniker range=">=vs-2019"

- 基于“工具”  >“选项”  >“文本编辑器”  >“C#”  >“代码样式”  中的代码样式设置自动创建 .editorconfig  文件。

   ![通过 VS 2019 中的设置生成 .editorconfig 文件](media/vs-2019/generate-editorconfig-file.png)

::: moniker-end

- 用于 Visual Studio 的 IntelliCode 的[代码推断功能](/visualstudio/intellicode/code-style-inference)通过现有代码推断代码样式。 然后它将使用已定义的代码样式首选项创建非空的 EditorConfig 文件。

- 通过编辑器直接配置代码样式规则的严重性级别。 如果用户当前没有 .editorconfig 文件，系统将自动生成该文件。 将光标置于错误、警告或建议上，然后键入 Ctrl+.   打开“快速操作和重构”菜单。 选择“配置或禁止显示问题”  。 然后选择规则并选择要为该规则配置的严重性级别。 这将使用规则的新严重性更新现有的 EditorConfig。

   ![在编辑器中直接配置代码样式规则的严重性级别](../ide/media/configure-severity-level.png)

请参阅 [.NET 编码约定选项](editorconfig-code-style-settings-reference.md)文档，其中也包含完整的 EditorConfig 文件的示例。

::: moniker range=">=vs-2019"

## <a name="code-cleanup"></a>代码清理

Visual Studio 通过“代码清理”功能按需设置代码文件的格式，其中包括代码样式首选项。  若要运行代码清理功能，请单击编辑器底部的扫把图标，或者按“Ctrl+K，Ctrl+E”     。

![Visual Studio 2019 中的“代码清理”按钮](media/execute-code-cleanup.png)

此外，还可以在整个项目或解决方中运行代码清理功能。 在“解决方案资源管理器”中右键单击项目或解决方案名称，选择“分析和代码清理”，然后选择“运行代码清理”。   

![在整个项目或解决方中运行代码清理功能](media/run-code-cleanup-project-solution.png)

代码清理不仅可以设置文件的空格、缩进等格式，还可以应用选定的代码样式。  将从 [EditorConfig 文件](code-styles-and-code-cleanup.md#code-styles-in-editorconfig-files)（若项目有此文件）或从“选项”对话框的[代码样式设置](code-styles-and-code-cleanup.md#code-styles-in-the-options-dialog-box)中读取对各个代码样式的偏好设置。 

::: moniker-end

## <a name="refactorings-and-code-fixes"></a>重构和代码修补程序

Visual Studio 包含大量重构、代码生成操作和代码修补程序。 红色波浪线表示错误，绿色波浪线表示警告，三个灰色点表示代码建议。 若要访问代码修补程序，可以单击灯泡或螺丝刀图标或按 Ctrl+   。 或 Alt+Enter   。 每个修补程序都附带一个显示修补工作方式实时代码差异的预览窗口。

常用的快速修复和重构包括：

- 重命名
- 提取方法
- 更改方法签名
- 生成构造函数
- 生成方法
- 将类型移动到文件
- 添加 NULL 检查
- 添加参数
- 删除不必要的 Using
- 用于 LINQ 查询或 LINQ 方法的 Foreach 循环
- 拉取成员

有关详细信息，请参阅[代码生成功能](code-generation-in-visual-studio.md)。

可以[安装 FxCop 分析器](../code-quality/install-fxcop-analyzers.md)来标记代码问题。 也可以使用 [Roslyn 分析器](https://github.com/dotnet/roslyn/wiki/Getting-Started-Writing-a-Custom-Analyzer-&-Code-Fix)编写自己的重构或代码修补程序。

有几个社区成员写了一些免费扩展，这些扩展添加了其他的代码检查：

- [Roslynator](https://marketplace.visualstudio.com/items?itemName=josefpihrt.Roslynator2017)
- [SonarLint for Visual Studio](https://marketplace.visualstudio.com/items?itemName=SonarSource.SonarLintforVisualStudio2017)
- [StyleCopAnalyzers](https://www.nuget.org/packages/stylecop.analyzers/)
- [CodeCracker](https://www.nuget.org/packages/codecracker.CSharp/)

![在 Visual Studio 中重构](../ide/media/VSGuide_CodeAnalysis.png)

## <a name="find-usages-go-to-implementation-and-navigate-to-decompiled-assemblies"></a>“查找使用情况”、“转到实现”和“导航到反编译程序集”

Visual Studio 具有许多功能可帮助你搜索和[导航代码](../ide/navigating-code.md)。

| 功能 | 快捷键 | 详细信息/改进 |
|- | - | -|
| 查找所有引用 | Shift+F12  | 结果已着色，可按项目、定义和引用类型（例如，读取或写入）等分组。 还可“锁定”结果。 |
| 转到实现 | Ctrl+F12   | 可以对 `override` 关键字使用转到定义来导航到重写成员 |
| 转到定义 | F12 或 Ctrl+单击   | 按住 Ctrl  ，同时单击以导航到定义 |
| 查看定义 | Alt+F12   | 定义的内联视图 |
| 结构可视化工具 | 括号中的灰色虚线 | 悬停鼠标查看代码结构 |
| 导航到反编译的程序集 | F12 或 Ctrl+单击    | 通过启用该功能导航到外部源（使用 ILSpy 进行了反编译）：“工具” > “选项” > “文本编辑器” > “C#” > “高级” > “启用导航到反编译源”       。 |

![转到全部和查找所有引用](../ide/media/VSIDE_Productivity_Navigation.png)

## <a name="improved-intellisense"></a>改进的 IntelliSense

使用用于 Visual Studio 的 IntelliCode 来获取[上下文感知代码补全](/visualstudio/intellicode/intellicode-visual-studio)，而不仅仅是按字母排序的列表。 还可以根据你自己特定于域的库训练[自定义 IntelliSense 模型](/visualstudio/intellicode/custom-model-faq)。

## <a name="unit-testing"></a>单元测试

从 Visual Studio 2017 开始，测试体验有了许多改进。 可以使用 MSTest v1、MSTest v2、NUnit 或 XUnit 测试框架进行测试。

- 测试资源管理器  测试发现速度很快。

- 使用分层排序  组织测试资源管理器  中的测试。

   ![Visual Studio 中的文本资源管理器的层次结构视图](../ide/media/VSGuide_Testing.png)

- [Live Unit Testing](../test/live-unit-testing.md) 持续运行受代码更改影响的测试并更新内联编辑器图标以显示测试的状态。 包含或排除实时测试集中的特定测试或测试项目。 （仅限 Visual Studio Enterprise Edition。）

## <a name="debugging"></a>调试

Visual Studio 的一些调试功能包括：

::: moniker range=">=vs-2019"

- 可以搜索“Watch”  、“Autos”  和“Locals”  窗口内的字符串。
- 运行到点击位置  ，可以通过该功能将鼠标悬停在一行代码旁，点击出现的绿色“运行”图标，则程序会运行到该行停止。
- 异常帮助程序  ，该功能将最重要的信息置于对话框顶层，例如，哪些变量在 `NullReferenceException` 中是 `null`。
- [后退式调试](../debugger/view-historical-application-state.md)，可通过该功能返回到上一个断点或步骤，并查看当时应用程序的状态。
- [快照调试](/azure/application-insights/app-insights-snapshot-debugger)，可通过该功能在引发异常时调查实时 Web 应用的状态（必须是在 Azure 上）。

::: moniker-end

::: moniker range="vs-2017"

- 运行到点击位置  ，可以通过该功能将鼠标悬停在一行代码旁，点击出现的绿色“运行”图标，则程序会运行到该行停止。
- 异常帮助程序  ，该功能将最重要的信息置于对话框顶层，例如，哪些变量在 `NullReferenceException` 中是 `null`。
- [后退式调试](../debugger/view-historical-application-state.md)，可通过该功能返回到上一个断点或步骤，并查看当时应用程序的状态。
- [快照调试](/azure/application-insights/app-insights-snapshot-debugger)，可通过该功能在引发异常时调查实时 Web 应用的状态（必须是在 Azure 上）。

::: moniker-end

![Visual Studio 中的异常帮助程序](../ide/media/VSGuide_Debugging.png)

## <a name="version-control"></a>版本控制

可以使用 git 或 TFVC 在 Visual Studio 中存储和更新代码。

::: moniker range=">=vs-2019"

- 安装 [Visual Studio 拉取请求](https://marketplace.visualstudio.com/items?itemName=vsideversioncontrolmsft.pr4vs)创建、查看、签出和运行拉取请求，而无需离开 Visual Studio。

::: moniker-end

- 在[团队资源管理器](reference/team-explorer-reference.md)中整理本地更改，并使用状态栏跟踪挂起的提交和更改。

- 在 Visual Studio 中通过 [Visual Studio 持续交付工具](https://marketplace.visualstudio.com/items?itemName=VSIDEDevOpsMSFT.ContinuousDeliveryToolsforVisualStudio)扩展设置 ASP.NET 项目的持续集成和交付。

![Visual Studio 中的源控件](../ide/media/VSIDE_Productivity_SourceControl.png)

## <a name="what-other-features-should-i-know-about"></a>我还需要了解哪些功能？

下面是提升写代码效率的编辑器和工作效率功能列表。 可能需要启用某些功能，因为它们默认处于禁用状态（它们可能在计算机上检索内容、具有争议性或者当前处于试验阶段）。

| 功能 | 详细信息 | 如何启用 |
|-|-|-|
| 在解决方案资源管理器中查找文件 | 突出显示了解决方案资源管理器中活动的文件  | “工具” > “选项” > “项目和解决方案” > “跟踪解决方案资源管理器中的活动项”     |
| 为引用程序集和 NuGet 包中的类型添加 using | 显示错误灯泡和代码修补程序，以便为未引用的类型安装 NuGet 包 | “工具” > “选项” > “文本编辑器” > “C#” > “高级” > “建议对引用程序集中的类型使用 using”和“建议对 NuGet 包中的类型使用 using”        |
| 启用完整解决方案分析 | 请在错误列表中查看解决方案中的所有错误  | “工具” > “选项” > “文本编辑器” > “C#” > “高级” > “启用完整解决方案分析”       |
| 启用导航到反编译源 | 对外部源的类型/成员启用“转到定义”并使用 ILSpy 反编译程序显示方法体 | “工具” > “选项” > “文本编辑器” > “C#” > “高级” > “启用导航到反编译源”       |
| 完成/建议模式 | 更改 IntelliSense 中的完成行为。 有 IntelliJ 背景的开发人员往往会使用此处的非默认设置。 | “菜单” > “编辑” > “IntelliSense” > “切换完成模式”     |
| [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md) | 显示编辑器中的代码引用信息和更改历史记录。 （源代码管理 CodeLens 指示器在 Visual Studio Community Edition 中不可用。） | “工具” > “选项” > “文本编辑器” > “所有语言” > “CodeLens”      |
| [代码片段](../ide/visual-csharp-code-snippets.md) | 帮助清除常见样本代码 | 键入代码片段名称，然后按两次 Tab  。 |
