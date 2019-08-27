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
ms.openlocfilehash: 7346b6fd8fbd483021437638f9e134ead88a0b93
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62846318"
---
# <a name="jit-optimization-and-debugging"></a>JIT 优化和调试
**如何优化适用于.NET:** 如果想要调试的代码，更加容易时，代码都**不**优化。 这是因为时代码进行了优化，编译器和运行时更改到发出的 CPU 代码以使它运行速度更快，但有的不太直接映射到原始源代码。 这意味着调试器是经常无法告诉您的本地变量的值和代码单步执行和断点可能无法按预期工作。

通常情况下发布生成配置创建优化的代码并调试生成配置却没有。 `Optimize` MSBuild 属性控制是否被告知编译器优化代码。

.NET 生态系统，在打开的代码是从源到 CPU 中两个步骤的说明进行操作： 首先，C#编译器将键入的文本转换为调用 MSIL 的中间二进制形式并将此写出到.dll 文件。 更高版本，.NET 运行时将此 MSIL 转换为的 CPU 指令。 这两个步骤可以优化某种程度上，但它由.NET 运行时执行的第二步执行更重要的优化。

**在模块加载 （仅限托管） 时取消 JIT 优化选项中：** 调试器将显示一个选项，用于控制目标进程内部加载启用优化进行编译的 DLL 时，会发生什么情况。 如果未选中此选项 （默认状态），则当.NET 运行时编译到 CPU 的代码的 MSIL 代码，则会使已启用的优化。 如果选中此选项，调试器请求，禁用优化。

若要查找**在模块加载 （仅限托管） 时取消 JIT 优化**选项，选中**工具** > **选项**，然后选择**常规**页上下**调试**节点。

**当应选中此选项：** 从其他源，nuget 包，例如下载 Dll 并将你想要调试此 DLL 中的代码时，请选中此选项。 为了使此功能，还必须为此 DLL 中查找符号 (.pdb) 文件。

如果只想调试本地生成的代码，最好将此选项保留未选中，因为在某些情况下，启用此选项将会显著降低调试。 有两个原因降低：

* 优化的代码运行速度更快。 如果您正在关闭的大量代码优化，最多可以添加对性能的影响。
* 如果必须启用仅我的代码，则调试器将甚至不尝试并进行了优化的 dll 加载符号。 查找符号可能需要长时间。

**此选项的限制：** 有两种情况下，此选项会将**不**工作：

1. 在其中将调试器附加到已运行的进程的情况下，此选项不会影响在已附加调试器时已经加载的模块。
2. 此选项不起作用于 Dll 已预编译为本机代码 （即进行 ngen 处理）。 但是，您可以通过使用环境变量 COMPlus_ZapDisable 设置为"1"启动进程禁用预编译代码的使用情况。

## <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
- [使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [托管执行过程](/dotnet/standard/managed-execution-process)
