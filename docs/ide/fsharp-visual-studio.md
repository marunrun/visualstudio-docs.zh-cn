---
title: F# 工具
description: 了解 F# 中支持的 Visual Studio 功能。
ms.date: 07/11/2018
ms.topic: reference
helpviewer_keywords:
- F# features [Visual Studio]
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 176504ceb7c80a36028e7d5f1806aa598cdf708e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645370"
---
# <a name="develop-with-visual-f-in-visual-studio"></a>在 Visual Studio 中使用 Visual F# 进行开发

本文介绍用于进行 F# 开发的 Visual Studio 功能的相关信息。

## <a name="install-f-support"></a>安装 F# 支持

要在 Visual Studio 中使用 F# 进行开发，请首先安装“.NET 桌面开发”工作负荷（如果尚未安装）  。 请通过 Visual Studio 安装程序安装 Visual Studio 工作负荷，可以通过选择“工具” > “获取工具和功能”将其打开   。

![Visual Studio 中的 .NET 桌面开发工作负荷](media/dotnet-desktop-development-workload.png)

## <a name="f-project-features"></a>F# 项目的功能

Visual Studio 中提供适用于 F# 的多种项目和项模板。 下图显示了一些用于 .NET Core 和 .NET Standard 的 F# 项目模板：

![Visual Studio 中的 F# 项目模板](media/fsharp-project-templates.png)

下图显示了一些 F# 项模板：

![Visual Studio 中的 F# 项模板](media/fsharp-item-templates.png)

有关用于数据访问的项模板的详细信息，请参阅 [F# 类型提供程序](/dotnet/fsharp/tutorials/type-providers/index)。

下表总结了项目属性中适用于 F# 的功能：

|项目设置|受 F# 支持？|说明|
|---------------|----------------|-----|
|资源文件|是||
|生成、调试和引用设置|是||
|多目标|是||
|图标和清单|No|通过编译器命令行选项提供。|
|ASP.NET 客户端服务|No||
|ClickOnce|No|以其他 .NET 语言使用客户端项目（如果适用）。|
|强命名|No|通过编译器命令行选项提供。|
|程序集发布和版本控制|No||
|代码分析|No|可手动运行或在生成后命令中运行代码分析工具。|
|安全性（更改信任级别）|No||

## <a name="project-designer"></a>项目设计器

项目设计器包含按相关功能分组的多个项目属性页  。 适用于 F# 项目的大多数页是可用于其他语言的子集，下表提供这些页的说明。 还提供了指向相应 C# 项目设计器页的链接  。

|“项目设计器”页|相关链接|说明|
| - |-------------|-----------|
|应用程序|[“应用程序”页，项目设计器](reference/application-page-project-designer-csharp.md)|支持指定应用程序级设置和属性，例如要创建库还是可执行文件、应用程序面向的 .NET 版本，以及有关应用程序所使用资源文件的存储位置的信息。|
|生成|[“项目设计器”->“生成”页](reference/build-page-project-designer-csharp.md)|支持控制代码的编译方式。|
|生成事件|[“生成事件”页，项目设计器](reference/build-events-page-project-designer-csharp.md)|支持指定编译之前或之后要运行的命令。|
|调试|[“项目设计器”->“调试”页](reference/debug-page-project-designer.md)|支持控制调试期间应用程序的运行方式。 其中包括要使用的命令、应用程序的启动目录和要启用的任何特殊调试模式，如本机代码和 SQL。|
|包（仅限 .NET SDK）|不可用|支持在作为 NuGet 包发布时定义 NuGet 包元数据。|
|引用路径|[管理项目中的引用](managing-references-in-a-project.md)|支持指定搜索代码依赖的程序集的位置。|
|资源（仅限 .NET SDK）|不可用|支持生成和管理默认资源文件。|

### <a name="f-specific-settings"></a>F# 的特定设置

下表总结了特定于 F# 的设置：

|“项目设计器”页|设置|说明|
| - |-------|-----------|
|生成|生成尾调用|选中后即可使用 Microsoft 中间语言 (MSIL) 尾指令。 这将导致对尾递归函数重复使用堆栈帧。 等效于 `--tailcalls` 编译器选项。|
|生成|其他标志|允许指定其他编译器命令行选项。|

## <a name="code-and-text-editor-features"></a>代码和文本编辑器功能

F# 中支持 Visual Studio 代码和文本编辑器的以下功能：

|功能|说明|受 F# 支持？|
|-------|-----------|----------------|
|自动注释|支持对代码部分添加注释或取消注释。|是|
|自动设置格式|使用标准缩进和样式重新设置代码格式。|No|
|书签|支持在编辑器中保存位置。|是|
|更改缩进|对所选行实施缩进或取消缩进。|是|
|智能缩进|根据 F# 作用域规则对光标实施自动缩进和取消缩进。|是|
|[查找和替换文本](finding-and-replacing-text.md)|支持在文件、项目或解决方案中执行搜索，并更改文本。|是|
|转到 .NET API 的定义|将光标置于 .NET API 时，显示 .NET 元数据生成的代码。|No|
|转到用户定义的 API 的定义|将光标置于定义的程序实体时，可将光标移至代码中定义实体的位置。|是|
|转到行|支持按行号转到文件中的特定行。|是|
|文件顶部的导航栏|支持跳到代码中的位置（例如按函数名称）。|是|
|块结构指南|显示指示 F# 作用域的指南，可通过悬停鼠标进行预览。|是|
|[大纲显示](outlining.md)|支持折叠代码的部分以创建更紧凑的视图。|是|
|替换为制表符|将空格转换为制表符。|是|
|类型着色|以特殊颜色显示定义的类型名称。|是|
|快速查找。 查看“快速查找”、“查找和替换”窗口。|支持在文件或项目中搜索。|是|
|通过 Ctrl+单击调用“转到定义”  |允许通过按住 Ctrl 并单击 F# 符号来调用“转到定义”  。|是|
|从“快速信息”到“转到定义”|可调用“转到定义”的可单击符号内部工具提示。|是|
|转到全部|通过 Ctrl+T 启用对所有 F# 构造的全局、模糊匹配导航   。|是|
|内联重命名|重命名一个符号内联的所有匹配项。|是|
|查找所有引用|在代码库中查找一个符号的所有匹配项。|是|
|简化名称代码修复|删除 F# 符号的不必要限定符。|是|
|删除未使用的 `open` 语句代码修复|删除文档中所有不必要的 `open` 语句。|是|
|未使用的值代码修复|建议将未使用的标识符重命名为下划线。|是|

有关在 Visual Studio 中编辑代码和文本编辑器的功能的常规信息，请参阅[在编辑器中编写代码](writing-code-in-the-code-and-text-editor.md)。

## <a name="intellisense-features"></a>IntelliSense 功能

下表总结了 F# 中支持的和不支持的 IntelliSense 功能：

|功能|说明|受 F# 支持？|
|-------|-----------|----------------|
|自动实现接口|为接口方法生成代码存根。|是|
|代码片段|将采用通用编码结构的库中的代码注入主题。|No|
|完成单词|通过在键入过程中完成字词和名称来减少键入操作。|是|
|自动完成|启用后，字词自动完成将在键入过程中选择第一个匹配项，而不会等待你选择一项或按 Ctrl+空格键   。|是|
|在未打开的命名空间中完成符号|选中后，可借助自动完成建议位于未打开的命名空间中的一个匹配符号，同时主动用对应的 `open` 语句将其完成。|是|
|生成代码元素|支持针对多种构造生成存根代码。|No|
|列表成员|键入成员访问运算符 (.) 时，显示某个类型的成员。|是|
|组织 Using/Open|组织 C# 中的 using 语句或 F# 中的 open 指令引用的命名空间   。|No|
|参数信息|在键入函数调用时，显示有关参数的有用信息。|是|
|快速信息|显示代码中任意标识符的完整声明。|是|
|自动大括号完成|以事务性方式自动完成 F# 类似大括号的语法构造。|是|

有关 IntelliSense 的常规信息，请参阅[使用 IntelliSense](using-intellisense.md)。

## <a name="debugging-features"></a>调试功能

下表总结了调试 F# 代码时的可用功能：

|功能|说明|受 F# 支持？|
|-------|-----------|----------------|
|“自动”窗口|显示自动或临时变量。|No|
|断点|支持在调试期间的特定点处暂停代码执行。|是|
|条件断点|支持用于测试条件（用于确定是否应暂停执行）的断点。|是|
|编辑并继续|支持在调试正在运行的程序期间修改和编译代码，而无需停止或重启调试程序。|No|
|表达式计算器|在运行时计算和执行代码。|否，但可以使用 C# 表达式计算器，前提是必须使用 C# 语法。|
|历史调试|支持单步执行以前执行的代码。|是|
|局部变量窗口|显示本地定义的值和变量。|是|
|运行到光标处|支持执行代码，直到到达包含光标的行。|是|
|逐语句|支持提前执行和移动到任何函数调用。|是|
|逐过程|支持在当前堆栈帧中提前执行和跳过任何函数调用。|是|

有关 Visual Studio 调试器的常规信息，请参阅[在 Visual Studio 中进行调试](../debugger/index.yml)。

## <a name="additional-tools"></a>其他工具

下表总结了 Visual Studio 工具中的 F# 支持。

|工具|说明|受 F# 支持？|
|----|-----------|----------------|
|调用层次结构|显示代码中的函数调用的嵌套结构。|No|
|代码度量|收集代码的相关信息，例如行计数。|No|
|类视图|提供项目中代码的基于类型的视图。|No|
|[“错误列表”窗口](reference/error-list-window.md)|显示代码中的错误列表。|是|
|[F# Interactive](/dotnet/fsharp/tutorials/fsharp-interactive/)|支持键入（或复制和粘贴）F# 代码并立即运行，不受项目的生成的影响。 F# 交互窗口是一个读取-求值-打印循环 (REPL)。|是|
|对象浏览器|支持查看程序集中的类型。|尽管 F# 类型会在已编译的程序集中出现，但不会在你对其进行创作时出现。 可以浏览 F# 类型的已编译表现形式，但不能在其显示在 F# 中时查看类型。|
|[“输出”窗口](reference/output-window.md)|显示生成输出。|是|
|性能分析|提供测量代码性能的工具。|是|
|“属性”窗口|显示具有焦点的开发环境中的对象的属性并支持编辑属性。|是|
|服务器资源管理器|提供与多种服务器资源进行交互的方式。|是|
|“解决方案资源管理器”|支持查看和管理项目和文件。|是|
|任务列表|支持管理与代码相关的工作项。|No|
|测试项目|提供有助于测试代码的功能。|No|
|工具箱|显示包含可拖动对象（如控件和部分文本或部分代码）的选项卡。|是|

## <a name="see-also"></a>请参阅

- [F# 指南 (.NET Framework)](/dotnet/fsharp/)
- [Visual Studio 中的 F# 入门](/dotnet/fsharp/get-started/get-started-visual-studio)