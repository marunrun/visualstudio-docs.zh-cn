---
title: 调试时解编译 .NET 代码 |微软文档
ms.date: 2/2/2020
ms.topic: conceptual
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
ms.openlocfilehash: d63c05120842d52dd54359e128d0cc5f2a195817
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508740"
---
# <a name="generate-source-code-from-net-assemblies-while-debugging"></a>调试时从 .NET 程序集生成源代码

调试 .NET 应用程序时，您可能会发现要查看没有的源代码。 例如，打破异常或使用调用堆栈导航到源位置。

> [!NOTE]
> * 源代码生成（解编译）仅适用于 .NET 应用程序，并且基于开源[ILSpy](https://github.com/icsharpcode/ILSpy)项目。
> * 解编译仅在 Visual Studio 2019 16.5 及更高版本中提供。
> * 将["禁止 Ildasm 属性"属性](https://docs.microsoft.com/dotnet/api/system.runtime.compilerservices.suppressildasmattribute)应用于程序集或模块可防止 Visual Studio 尝试取消编译。

## <a name="generate-source-code"></a>生成源代码

当您正在调试且没有源代码可用时，Visual Studio 将显示 **"源未找到"** 文档，或者如果没有程序集的符号"**已加载无符号"** 文档。 这两个文档都有一个 **"去编译"源代码**选项，用于生成当前位置的 C# 代码。 然后，可以使用生成的 C# 代码，就像使用任何其他源代码一样。 您可以查看代码、检查变量、设置断点等。

### <a name="no-symbols-loaded"></a>未加载符号

下图显示了 **"无符号加载"** 消息。

![无符号加载文档的屏幕截图](media/decompilation-no-symbol-found.png)

### <a name="source-not-found"></a>未找到源

下图显示了 **"未找到源"** 消息。

![未找到源文档的屏幕截图](media/decompilation-no-source-found.png)

## <a name="generate-and-embed-sources-for-an-assembly"></a>生成和嵌入程序集的源

除了为特定位置生成源代码外，还可以为给定的 .NET 程序集生成所有源代码。 为此，请转到**模块**窗口和 .NET 程序集的上下文菜单，然后选择 **"去编译源代码**"命令。 Visual Studio 为程序集生成符号文件，然后将源嵌入到符号文件中。 在后面的步骤中，可以[提取](#extract-and-view-the-embedded-source-code)嵌入的源代码。

![具有取消编译源命令的模块窗口中程序集上下文菜单的屏幕截图。](media/decompilation-decompile-source-code.png)

## <a name="extract-and-view-the-embedded-source-code"></a>提取和查看嵌入的源代码

您可以使用 **"模块"** 窗口的上下文菜单中的 **"提取源代码"** 命令提取嵌入在符号文件中的源文件。

![具有数据提取源命令的模块窗口中程序集上下文菜单的屏幕截图。](media/decompilation-extract-source-code.png)

提取的源文件将作为[杂项文件](../ide/reference/miscellaneous-files.md)添加到解决方案中。 默认情况下，在 Visual Studio 中，杂项文件功能处于关闭状态。 您可以在 **"工具** > **选项** > **环境** > **Documents**文档 > **在解决方案资源管理器"复选框中显示"杂项文件**"中启用此功能。 如果不启用此功能，您将无法打开提取的源代码。

![启用了"杂项文件"选项的工具选项页的屏幕截图。](media/decompilation-tools-options-misc-files.png)

提取的源文件将显示在**解决方案资源管理器**中的杂项文件中。

![包含杂项文件的解决方案资源管理器的屏幕截图。](media/decompilation-solution-explorer.png)

## <a name="known-limitations"></a>已知的限制

### <a name="requires-break-mode"></a>需要中断模式

仅当调试器处于中断模式且应用程序暂停时，才可能使用解编译生成源代码。 例如，Visual Studio 在达到断点或异常时进入中断模式。 您可以使用"**全部中断"** 命令（断开所有图标![](media/decompilation-break-all.png)）轻松触发 Visual Studio 以在下次运行代码时中断代码。

### <a name="decompilation-limitations"></a>取消编译限制

从 .NET 程序集中使用的中间格式 （IL） 生成源代码有一些固有的限制。 因此，生成的源代码看起来不像原始源代码。 大多数差异是在运行时不需要原始源代码中的信息的地方。 例如，运行时不需要空格、注释和局部变量的名称等信息。 我们建议您使用生成的源来了解程序的执行方式，而不是作为原始源代码的替换。

### <a name="debug-optimized-or-release-assemblies"></a>调试优化或释放程序集

调试从使用编译器优化编译的程序集中解编译的代码时，可能会遇到以下问题：
- 断点可能并不总是绑定到匹配的采购位置。
- 步进可能并不总是步进到正确的位置。
- 局部变量可能没有准确的名称。
- 某些变量可能可用于评估。

更多详细信息请参阅 GitHub 问题[：ICSharpCode.De编译器集成到 VS 调试器](https://github.com/icsharpcode/ILSpy/issues/1901)中。

### <a name="decompilation-reliability"></a>取消编译可靠性

相对较少的取消编译尝试可能会导致失败。 这是由于 ILSpy 中的序列点 null 引用错误。  我们通过抓住这些问题并优雅地失败删除编译尝试来减轻失败。

更多详细信息请参阅 GitHub 问题[：ICSharpCode.De编译器集成到 VS 调试器](https://github.com/icsharpcode/ILSpy/issues/1901)中。

### <a name="limitations-with-async-code"></a>不同步代码的限制

使用异步/等待代码模式取消编译模块的结果可能不完整或完全失败。 只部分实现了异步/await 和屈服状态机的 ILSpy 实现。 

更多详细信息可在 GitHub 问题中找到[：PDB 生成器状态](https://github.com/icsharpcode/ILSpy/issues/1422)。

### <a name="just-my-code"></a>仅我的代码

["仅我的代码 （JMC）"](https://docs.microsoft.com/visualstudio/debugger/just-my-code)设置允许 Visual Studio 跨跨系统、框架、库和其他非用户呼叫。 在调试会话期间，"**模块"** 窗口显示调试器将哪些代码模块视为"我的代码"（用户代码）。

取消编译优化或发布模块会产生非用户代码。 例如，如果调试器在已编译的非用户代码中中断，则会出现 **"无源"** 窗口。 要禁用"仅我的代码"，请导航到 **"工具** > **选项**"（或**调试** > **选项**）>**调试** > **常规**，然后取消选择**仅启用我的代码**。

### <a name="extracted-sources"></a>提取的源

从程序集中提取的源代码具有以下限制：
- 生成的文件的名称和位置不可配置。
- 这些文件是临时的，将由 Visual Studio 删除。
- 这些文件放置在单个文件夹中，并且不使用原始源的任何文件夹层次结构。
- 每个文件的文件名包含文件的校验和哈希。

### <a name="generated-code-is-c-only"></a>生成的代码仅为 C#
解编译仅在 C# 中生成源代码文件。 没有以任何其他语言生成文件的选项。
