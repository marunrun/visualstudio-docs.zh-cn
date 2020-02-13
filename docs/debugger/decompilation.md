---
title: 调试时反编译 .NET 代码 |Microsoft Docs
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
ms.openlocfilehash: 5087c439533aa447708d0f1bfae653054fd16089
ms.sourcegitcommit: a86ee68e3ec23869b6eaaf6c6b7946b1d9a88d01
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2020
ms.locfileid: "77144790"
---
# <a name="generate-source-code-from-net-assemblies-while-debugging"></a>在调试时从 .NET 程序集生成源代码

调试 .NET 应用程序时，您可能会发现您要查看没有的源代码。 例如，中断异常或使用调用堆栈导航到源位置。

> [!NOTE]
> * 源代码生成（ilspy）仅适用于 .NET 应用程序，并且基于开源[ILSpy](https://github.com/icsharpcode/ILSpy)项目。
> * Ilspy 仅适用于 Visual Studio 2019 16.5 及更高版本。

## <a name="generate-source-code"></a>生成源代码

调试时，如果没有可用的源代码，Visual Studio 会显示 "**找不到源**" 文档，如果没有程序集的符号，则不会**加载任何符号**。 这两个文档都有一个**反编译**的C#源代码选项，该选项可为当前位置生成代码。 然后， C#可以像使用任何其他源代码一样使用生成的代码。 您可以查看代码、检查变量、设置断点等。

### <a name="no-symbols-loaded"></a>未加载任何符号

下图显示了 "**未加载任何符号**" 消息。

![未加载符号的屏幕截图文档](media/decompilation-no-symbol-found.png)

### <a name="source-not-found"></a>找不到源

下图显示了 "**找不到源**" 消息。

![找不到源文档的屏幕截图](media/decompilation-no-source-found.png)

## <a name="generate-and-embed-sources-for-an-assembly"></a>为程序集生成和嵌入源

除了生成特定位置的源代码以外，您还可以生成给定 .NET 程序集的所有源代码。 为此，请从 .NET 程序集的上下文菜单中转到 "**模块**" 窗口，然后选择 "**反编译的源代码**" 命令。 Visual Studio 将生成程序集的符号文件，然后将该源嵌入到符号文件中。 在后面的步骤中，您可以[提取](#extract-and-view-the-embedded-source-code)嵌入的源代码。

![带有反编译源命令的 "模块" 窗口中的程序集上下文菜单的屏幕截图。](media/decompilation-decompile-source-code.png)

## <a name="extract-and-view-the-embedded-source-code"></a>提取和查看嵌入的源代码

您可以使用 "**模块**" 窗口的上下文菜单中的 "**提取源代码**" 命令提取嵌入到符号文件中的源文件。

![带有提取源命令的 "模块" 窗口中的程序集上下文菜单的屏幕截图。](media/decompilation-extract-source-code.png)

提取的源文件作为[杂项文件](../ide/reference/miscellaneous-files.md)添加到解决方案中。 默认情况下，Visual Studio 中的 "杂项文件" 功能处于关闭状态。 你可以从 "**工具**" > **选项**" >  > **环境**中启用此**功能 > ** **在解决方案资源管理器中显示杂项文件**" 复选框。 如果不启用此功能，将无法打开提取的源代码。

![启用了杂项文件选项的工具选项页的屏幕截图。](media/decompilation-tools-options-misc-files.png)

提取的源文件显示在**解决方案资源管理器**的杂项文件中。

![包含杂项文件的解决方案资源管理器的屏幕截图。](media/decompilation-solution-explorer.png)

## <a name="known-limitations"></a>已知限制

### <a name="requires-break-mode"></a>需要中断模式

仅当调试器处于中断模式且应用程序已暂停时，才可以使用 ilspy 生成源代码。 例如，当 Visual Studio 命中断点或异常时，它将进入中断模式。 通过使用 "**全部中断**" 命令（!["全部中断" 图标](media/decompilation-break-all.png)），可以轻松触发 Visual Studio 在下一次运行代码时中断。

### <a name="decompilation-limitations"></a>Ilspy 限制

从 .NET 程序集中使用的中间格式（IL）生成源代码有一些固有的限制。 因此，生成的源代码看起来不像原始源代码。 大多数差别在于在运行时不需要原始源代码中的信息的位置。 例如，在运行时不需要空白、注释和局部变量的名称等信息。 建议使用生成的源来了解程序的执行方式，而不是原始源代码的替代方法。

### <a name="debug-optimized-or-release-assemblies"></a>调试优化或发布程序集

调试使用编译器优化编译的程序集中反编译的代码时，可能会遇到以下问题：
- 断点并非始终绑定到匹配的采购位置。
- 单步执行可能并不总是单步执行到正确的位置。
- 局部变量的名称可能不正确。
- 某些变量可能不可用于计算。

有关更多详细信息，请参阅 GitHub 问题：[反编译程序集成到 VS 调试器中 IChsarpCompiler。](https://github.com/icsharpcode/ILSpy/issues/1901)

### <a name="decompilation-reliability"></a>Ilspy 可靠性

相对较小的 ilspy 尝试百分比可能会导致失败。 这是由于 ILSpy 中的序列点为空引用错误引起的。  我们缓解了这些问题，并在 ilspy 尝试中进行了正确的故障转移。

有关更多详细信息，请参阅 GitHub 问题：[反编译程序集成到 VS 调试器中 IChsarpCompiler。](https://github.com/icsharpcode/ILSpy/issues/1901)

### <a name="limitations-with-async-code"></a>异步代码的限制

具有 async/await 代码模式的反编译模块的结果可能不完整或完全失败。 Async/await 和 yield 状态的 ILSpy 实现仅部分实现。 

有关更多详细信息，请参阅 GitHub 问题： [PDB 生成器状态](https://github.com/icsharpcode/ILSpy/issues/1422)。

### <a name="just-my-code"></a>仅我的代码

[仅我的代码（JMC）](https://docs.microsoft.com/visualstudio/debugger/just-my-code)设置允许 Visual Studio 逐过程执行系统、框架、库和其他非用户调用。 在调试会话期间，"**模块**" 窗口将显示调试器处理为 "我的代码" 的代码模块（用户代码）。

优化或发布模块的 ilspy 生成非用户代码。 例如，如果调试器在反编译非用户代码中中断，则不会显示 "**无源**" 窗口。 若要禁用仅我的代码，请导航到 "**工具**" > **选项**"（或"**调试** > **选项**"） >**调试** > "**常规**"，然后取消选择"**启用仅我的代码**"。

### <a name="extracted-sources"></a>提取的源

从程序集提取的源代码具有以下限制：
- 生成的文件的名称和位置不可配置。
- 文件是临时文件，将被 Visual Studio 删除。
- 这些文件放在一个文件夹中，并在原始源中未使用任何文件夹层次结构。
- 每个文件的文件名包含文件的校验和哈希。

### <a name="generated-code-is-c-only"></a>生成的C#代码仅
Ilspy 仅在中C#生成源代码文件。 没有用于生成任何其他语言文件的选项。