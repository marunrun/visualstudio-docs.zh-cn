---
title: “高级生成设置”对话框 (C#)
ms.date: 08/05/2019
ms.technology: vs-ide-compile
ms.topic: reference
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 917ef4ff685c243fa271a0966a931151cb12ed2b
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418842"
---
# <a name="advanced-build-settings-dialog-box-c"></a>“高级生成设置”对话框 (C#)

使用“项目设计器”的“高级生成设置”对话框可指定项目的高级生成配置属性   。 此对话框仅适用于 C# 项目。

## <a name="general"></a>常规

通过以下选项可以设置常规高级设置。

**语言版本**

::: moniker range=">=vs-2019"

指向 [/langversion（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option)的链接，它提供有关如何根据项目的目标框架选择默认语言版本的信息。

::: moniker-end

::: moniker range="vs-2017"

指定要使用的语言版本。 每个版本中的功能集是不同的，因此，可使用此选项强制编译器仅允许已实现功能的子集，或仅启用与现有标准兼容的功能。

默认值是 C# 7.0。

::: moniker-end

**内部编译器错误报告**

指定是否向 Microsoft 报告编译器错误。 如果设置为“提示”  （默认），则在发生内部编译器错误时将收到提示，可以选择向 Microsoft 发送电子版错误报告。 如果设置为“发送”  ，则将自动发送错误报告。 如果设置为“队列”  ，则错误报告将排入队列。 如果设置为“无”  ，将仅在编译器的文本输出中报告错误。 有关详细信息，请参阅 [/errorreport（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option)。

**检查运算上溢/下溢**

指定不在 [checked](/dotnet/csharp/language-reference/keywords/checked) 或 [unchecked](/dotnet/csharp/language-reference/keywords/unchecked) 关键字范围内且生成的值超出数据类型范围的整数算法语句是否会导致运行时异常抛出。 有关详细信息，请参阅 [/checked（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option)。

**不引用 mscorlib.dll**

指定是否将 mscorlib.dll 导入程序，同时定义整个 <xref:System> 命名空间。 如果想要定义或创建自己的 <xref:System> 命名空间和对象，请选中此框。 有关详细信息，请参阅 [/nostdlib（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option)。

## <a name="output"></a>输出

使用以下选项可以指定高级输出选项。

**调试信息**

指定编译器生成的调试信息的类型。 有关如何配置应用程序的调试性能的信息，请参阅[令映像更易于调试](/dotnet/framework/debug-trace-profile/making-an-image-easier-to-debug)。 此设置具有以下选项：

- **none**

   指定不会生成任何调试信息。

- **full**

   允许将调试器附加到正在运行的程序。

- **pdbonly**

   允许在调试器中启动程序时进行源代码调试，但仅在正在运行的程序附加到调试器时才显示汇编程序。

- **portable**

   生成 .PDB 文件，这是一种未特定于任何平台的可移植符号文件，可提供其他工具（尤其是调试器）、主可执行文件内容的相关信息及其生成方式。 有关详细信息，请参阅 [Portable PDB](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md)（可移植 PDB）。

- **embedded**

   将可移植符号信息嵌入程序集。 不会生成任何外部 .PDB 文件。

有关详细信息，请参阅 [/debug (C# 编译器选项)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)。

**文件对齐**

指定输出文件中各节的大小。 有效值为 **512**、**1024**、**2048**、**4096** 和 **8192**。 这些值以字节为单位。 每一节都在边界（此值的倍数）上对齐，这会影响输出文件的大小。 有关详细信息，请参阅 [/filealign（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option)。

**库基址**

指定要加载 DLL 的首选基址。 DLL 的默认基址由 .NET Framework 公共语言运行时设置。 有关详细信息，请参阅 [/baseaddress（C# 编译器选项）](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option)。

## <a name="see-also"></a>另请参阅

- [C# 编译器选项](/dotnet/csharp/language-reference/compiler-options/index)
- [项目设计器的“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)
