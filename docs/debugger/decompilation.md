---
title: 在调试时反向编译 .NET 代码 | Microsoft Docs
ms.date: 2/2/2020
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- decompilation, debugger, exception
- debugging [Visual Studio], decompilation, source not found
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.openlocfilehash: b7d9ed2f2ceeae21b85fdb8227e65715cb07bc8b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350558"
---
# <a name="generate-source-code-from-net-assemblies-while-debugging"></a>在调试时从 .NET 程序集生成源代码

调试 .NET 应用程序时，可能会发现要查看你没有的源代码。 例如，中断异常或使用调用堆栈导航到源位置。

> [!NOTE]
> * 源代码生成（反向编译）仅适用于 .NET 应用程序，并且基于开放源代码 [ILSpy](https://github.com/icsharpcode/ILSpy) 项目。
> * 反向编译功能仅在 Visual Studio 2019 16.5 及更高版本中提供。
> * 将 [SuppressIldasmAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.compilerservices.suppressildasmattribute) 属性应用于程序集或模块可防止 Visual Studio 进行反向编译尝试。

## <a name="generate-source-code"></a>生成源代码

进行调试但没有可用的源代码时，Visual Studio 会显示“找不到源代码”文档，或者，如果没有用于程序集的符号，则显示“未加载任何符号”文档 。 这两个文档都有一个“反向编译源代码”选项，该选项可针对当前位置生成 C# 代码。 然后，可以像使用任何其他源代码一样使用生成的 C# 代码。 你可以查看代码、检查变量、设置断点等等。

### <a name="no-symbols-loaded"></a>未加载任何符号

下图显示了“未加载任何符号”消息。

![“未加载任何符号”文档的屏幕截图](media/decompilation-no-symbol-found.png)

### <a name="source-not-found"></a>找不到源代码

下图显示了“找不到源代码”消息。

![“找不到源代码”文档的屏幕截图](media/decompilation-no-source-found.png)

## <a name="generate-and-embed-sources-for-an-assembly"></a>为程序集生成和嵌入源代码

除了针对特定位置生成源代码之外，还可以针对给定的 .NET 程序集生成所有源代码。 为此，请转到“模块”窗口，然后在 .NET 程序集的上下文菜单中，选择“反向编译源代码”命令 。 Visual Studio 为程序集生成一个符号文件，然后将源代码嵌入到该符号文件中。 在后续步骤中，可以[提取](#extract-and-view-the-embedded-source-code)嵌入的源代码。

![“模块”窗口中包含“反向编译源代码”命令的程序集上下文菜单的屏幕截图。](media/decompilation-decompile-source-code.png)

## <a name="extract-and-view-the-embedded-source-code"></a>提取和查看嵌入的源代码

可使用“模块”窗口内上下文菜单中的“提取源代码”命令来提取嵌入在符号文件中的源文件 。

![“模块”窗口包含“提取源代码”命令的程序集上下文菜单的屏幕截图。](media/decompilation-extract-source-code.png)

提取的源文件将作为[杂项文件](../ide/reference/miscellaneous-files.md)添加到解决方案中。 在 Visual Studio 中，杂项文件功能默认处于关闭状态。 可通过“工具” > “选项” > “环境” > “文档” > “在解决方案资源管理器中显示杂项文件”复选框来启用此功能    。 如果不启用此功能，则将无法打开提取的源代码。

![已启用“杂项文件”选项的工具选项页面的屏幕截图。](media/decompilation-tools-options-misc-files.png)

提取的源文件将显示在“解决方案资源管理器”的“杂项文件”中。

![包含“杂项文件”的“解决方案资源管理器”的屏幕截图。](media/decompilation-solution-explorer.png)

## <a name="known-limitations"></a>已知限制

### <a name="requires-break-mode"></a>需要中断模式

仅当调试器处于中断模式并且应用程序暂停时，才可以使用反向编译功能生成源代码。 例如，Visual Studio 遇到断点或异常时会进入中断模式。 通过使用“全部中断”命令（![全部中断图标](media/decompilation-break-all.png)），可以轻松触发 Visual Studio 在下次运行代码时中断。

### <a name="decompilation-limitations"></a>反向编译的限制

从 .NET 程序集中使用的中间格式 (IL) 生成源代码有一些固有的限制。 因此，生成的源代码看起来与原始源代码不同。 大多数存在差异的地方都在于运行时不需要原始源代码中的信息。 例如，运行时不需要空格、注释和局部变量名称等信息。 建议使用生成的源代码来了解程序的执行方式，而不是用于替代原始源代码。

### <a name="debug-optimized-or-release-assemblies"></a>调试优化或发布的程序集

在调试从使用编译器优化功能编译的程序集反向编译的代码时，可能会遇到以下问题：
- 断点可能并不总是绑定到匹配的源位置。
- 单步执行可能并不总是进行到正确的位置。
- 局部变量的名称可能不正确。
- 某些变量可能无法求值。

可在 GitHub 问题中找到更多详细信息：[ICSharpCode.Decompiler 与 VS 调试器集成](https://github.com/icsharpcode/ILSpy/issues/1901)。

### <a name="decompilation-reliability"></a>反向编译的可靠性

反向编译尝试失败的概率相对较小。 反向编译失败是由于 ILSpy 中的序列点 NULL 引用错误。  我们通过捕获这些问题并重现失败过程来减少反向编译失败。

可在 GitHub 问题中找到更多详细信息：[ICSharpCode.Decompiler 与 VS 调试器集成](https://github.com/icsharpcode/ILSpy/issues/1901)。

### <a name="limitations-with-async-code"></a>异步代码的限制

使用异步/等待代码模式反向编译模块的结果可能不完整或完全失败。 异步/等待和暂停状态机的 ILSpy 实现仅部分实现。 

可在 GitHub 问题中找到更多详细信息：[PDB 生成器状态](https://github.com/icsharpcode/ILSpy/issues/1422)。

### <a name="just-my-code"></a>仅我的代码

[仅我的代码 (JMC)](https://docs.microsoft.com/visualstudio/debugger/just-my-code) 设置使 Visual Studio 可以单步跳过系统、框架、库和其他非用户调用。 在调试会话期间，“模块”窗口会显示调试器将哪些代码模块视为“我的代码”（用户代码）。

对优化或发布模块进行反向编译会生成非用户代码。 例如，如果调试器中断了反向编译的非用户代码，则会显示“无源代码”窗口。 要禁用“仅我的代码”，请导航至“工具” > “选项”（或“调试” > “选项”）>“调试” > “常规”，然后取消选择“启用仅我的代码”      。

### <a name="extracted-sources"></a>提取的源代码

从程序集中提取的源代码具有以下限制：
- 所生成文件的名称和位置不可配置。
- 这些文件是临时文件，Visual Studio 会将其删除。
- 这些文件放在单个文件夹中，并且不使用原始源文件的任何文件夹层次结构。
- 每个文件的文件名都包含该文件的校验和哈希。

### <a name="generated-code-is-c-only"></a>生成的代码仅采用 C#
反向编译仅生成 C# 源代码文件。 没有以任何其他语言生成文件的选项。
