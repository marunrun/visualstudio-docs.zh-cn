---
title: JIT 优化和调试 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], optimized code
- optimized code, debugging
ms.assetid: 19bfabf3-1a2e-49dc-8819-a813982e86fd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ae11860aaa64448cd4d23b5602cf4c2da1575ce3
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916231"
---
# <a name="jit-optimization-and-debugging"></a>JIT 优化和调试
如果尝试调试代码，则**不**会优化代码。 优化代码时，编译器和运行时对发出的 CPU 代码进行更改，使其运行速度更快，但与原始源代码的直接映射更少。 如果映射不太直接，则调试器通常无法告诉您本地变量的值，并且代码单步执行和断点可能无法按预期工作。

> [!NOTE]
> 有关 JIT （实时）调试的详细信息，请阅读[此文档](../debugger/debug-using-the-just-in-time-debugger.md)。

## <a name="how-optimizations-work-in-net"></a>.NET 中的优化的工作原理 
通常，发布版本配置会创建优化的代码，而调试生成配置则不会。 `Optimize` MSBuild 属性控制是否告诉编译器优化代码。

在 .NET 生态系统中，代码在两个步骤中按源到 CPU 的说明进行：首先， C#编译器将您键入的文本转换为名为 msil 的中间二进制格式，并将 MSIL 写入 .dll 文件。 稍后，.NET 运行时将此 MSIL 转换为 CPU 说明。 这两个步骤都可以优化到一定程度，但 .NET 运行时执行的第二个步骤会执行更重要的优化。

## <a name="the-suppress-jit-optimization-on-module-load-managed-only-option"></a>"在模块加载时取消 JIT 优化（仅限托管）" 选项
调试器公开一个选项，该选项控制在目标进程内启用了优化并加载已编译的 DLL 时所发生的情况。 如果未选中此选项（默认状态），则当 .NET 运行时将 MSIL 代码编译为 CPU 代码时，它将保持启用优化。 如果选中该选项，则调试器会请求禁用优化。

若要查找 "**在模块加载时取消 JIT 优化（仅限托管）** " 选项，请选择 "**工具**" > **选项**"，然后选择"**调试**"节点下的"**常规**"页。

![取消 JIT 优化](../debugger/media/suppress-jit-tool-options.png "取消 JIT 优化")

## <a name="when-should-you-check-the-suppress-jit-optimization-option"></a>何时应检查 "取消 JIT 优化" 选项？
当你从另一个源（如 nuget 包）下载 Dll，并且你想要调试此 DLL 中的代码时，请选中此选项。 为了使禁止显示工作，还必须找到此 DLL 的符号（.pdb）文件。

如果你只想调试要在本地生成的代码，最好将此选项保留为取消选中状态，例如，在某些情况下，启用此选项会显著降低调试速度。 此速度慢的原因有两个：

* 优化的代码运行速度更快。 如果要为多个代码关闭优化，则性能影响可能会增加。
* 如果已启用仅我的代码，则调试器甚至不会尝试为经过优化的 Dll 加载符号。 查找符号可能需要较长时间。

## <a name="limitations-of-the-suppress-jit-optimization-option"></a>"取消 JIT 优化" 选项的限制 
在以下两种情况下，启用此选项将**不**起作用：

1. 在将调试器附加到已在运行的进程的情况下，此选项将对附加调试器时已加载的模块无效。
2. 此选项不会影响已预先编译（ngen'ed）到本机代码的 Dll。 但是，您可以通过启动将环境变量 **"COMPlus_ReadyToRun"** 设置为 **"0"** 的进程来禁用预编译代码的使用。 这将告知 .NET Core 运行时禁用预编译的映像，并强制运行时 JIT 编译框架代码。 

    > [!IMPORTANT]
    > 如果针对的是 .NET Framework 或较早版本的 .NET Core （2.x 或更低版本），请添加环境变量 "COMPlus_ZapDisable" 并将其设置为 "1"

    **在 Visual Studio 中为 .NET Core 项目设置环境变量：**
    1. 在**解决方案资源管理器**中，**右键单击**项目文件并选择 "**属性**"。
    2. 导航到 "**调试**" 选项卡，然后在 "**环境变量**" 下单击 "**添加**" 按钮。
    3. 将名称（Key）设置为**COMPlus_ReadyToRun** ，并将值设置为**0**。

    ![设置 COMPlus_ReadyToRun 环境变量](../debugger/media/environment-variables-debug-menu.png "设置 COMPlus_ReadyToRun 环境变量")

## <a name="see-also"></a>另请参阅
- [如何调试 Dotnet Framework 源](../debugger/how-to-debug-dotnet-framework-source.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
- [使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [托管执行过程](/dotnet/standard/managed-execution-process)
