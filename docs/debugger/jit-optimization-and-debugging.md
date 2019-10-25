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
ms.openlocfilehash: 12752acf75da70fa30666f9b1780256c94bde859
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72731626"
---
# <a name="jit-optimization-and-debugging"></a>JIT 优化和调试
**.Net 中的优化的工作原理：** 如果尝试调试代码，则**不**会优化代码。 这是因为当对代码进行优化时，编译器和运行时对发出的 CPU 代码进行更改，使其运行速度更快，但与原始源代码的直接映射更少。 这意味着，调试程序经常无法告诉您本地变量的值，并且代码单步执行和断点可能无法按预期工作。

通常，发布版本配置会创建优化的代码，而调试生成配置则不会。 @No__t_0 MSBuild 属性控制是否告诉编译器优化代码。

在 .NET 生态系统中，代码在两个步骤中按源到 CPU 的说明进行：首先， C#编译器将您键入的文本转换为名为 MSIL 的中间二进制格式，并将其写入 .dll 文件。 稍后，.NET 运行时将此 MSIL 转换为 CPU 说明。 这两个步骤都可以优化到一定程度，但 .NET 运行时执行的第二个步骤会执行更重要的优化。

**"在模块加载时取消 JIT 优化（仅限托管）" 选项：** 调试器公开一个选项，该选项控制在目标进程内启用了优化并加载已编译的 DLL 时所发生的情况。 如果未选中此选项（默认状态），则当 .NET 运行时将 MSIL 代码编译为 CPU 代码时，它将保持启用优化。 如果选中该选项，则调试器会请求禁用优化。

若要查找 "**在模块加载时取消 JIT 优化（仅限托管）** " 选项，请选择 "**工具**"  > **选项**"，然后选择"**调试**"节点下的"**常规**"页。

**应在何时选中此选项：** 当你从另一个源（如 nuget 包）下载 Dll，并且你想要调试此 DLL 中的代码时，请选中此选项。 为了使其正常工作，你还必须找到此 DLL 的符号（.pdb）文件。

如果你只想调试要在本地生成的代码，最好将此选项保留为取消选中状态，例如，在某些情况下，启用此选项会显著降低调试速度。 此速度慢的原因有两个：

* 优化的代码运行速度更快。 如果要为多个代码关闭优化，则性能影响可能会增加。
* 如果已启用仅我的代码，则调试器甚至不会尝试加载已优化的 Dll 的符号。 查找符号可能需要较长时间。

**此选项的限制：** 在以下两种情况下，此选项将**不**起作用：

1. 在将调试器附加到已在运行的进程的情况下，此选项将对附加调试器时已加载的模块无效。
2. 此选项不会影响已预先编译（ngen'ed）到本机代码的 Dll。 但是，您可以通过启动将环境变量 "COMPlus_ZapDisable" 设置为 "1" 的进程来禁用预编译代码的使用。

## <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
- [使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [托管执行过程](/dotnet/standard/managed-execution-process)
