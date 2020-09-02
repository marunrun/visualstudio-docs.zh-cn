---
title: “高级生成设置”对话框 (C#) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.AdvancedBuildSettings
helpviewer_keywords:
- Build options [C#], advanced
ms.assetid: 141f2dee-1563-4ce6-ba37-32920b082519
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 38f4d233c8804bec91d2f7dfd2dc34c6879e8be9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651726"
---
# <a name="advanced-build-settings-dialog-box-c"></a>“高级生成设置”对话框 (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用“项目设计器”**** 的“高级生成设置”**** 对话框来指定项目的高级生成配置属性。 此对话框仅适用于 [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 项目。

## <a name="general"></a>常规
 通过以下选项可以设置常规高级设置。

 **语言版本** 指定要使用的语言版本。 每个版本中的功能集是不同的，因此，可使用此选项强制编译器仅允许已实现功能的子集，或仅启用与现有标准兼容的功能。 此设置具有以下选项：

- **ISO-1**

   面向 ISO-1 标准功能。

- **default**

   面向当前版本。

  有关详细信息，请参阅 [/langversion (c # 编译器选项) ](https://msdn.microsoft.com/library/3fb00b05-a0ff-4782-b313-13a4c0f62d94)。

  **内部编译器错误报告** 指定是否向 Microsoft 报告编译器错误。 如果设置为“提示”****（默认），则在发生内部编译器错误时将收到提示，可以选择向 Microsoft 发送电子版错误报告。 如果设置为“发送”****，则将自动发送错误报告。 如果设置为“队列”****，则错误报告将排入队列。 如果设置为“无”****，将仅在编译器的文本输出中报告错误。 有关详细信息，请参阅 [/errorreport (c # 编译器选项) ](https://msdn.microsoft.com/library/bd0e7493-b79d-4369-9c3f-ba26ebdfbedf)。

  **检查算术上溢/下溢** 指定整数算法语句是否不在 [选中](https://msdn.microsoft.com/library/718a1194-988d-48a3-b089-d6ee8bd1608d) 或 [未选中](https://msdn.microsoft.com/library/0c021f7c-923f-4b3d-a58f-55336f5ac27e) 关键字的作用域中，导致超出数据类型范围的值将导致运行时异常。有关详细信息，请参阅 [/checked (c # 编译器选项) ](https://msdn.microsoft.com/library/fb7475d3-e6a6-4e6d-b86c-69e7a74c854b)。

  **不引用 mscorlib.dll** 指定是否将 mscorlib.dll 导入程序，从而定义整个 <xref:System> 命名空间。 如果想要定义或创建自己的 <xref:System> 命名空间和对象，请选中此框。 有关详细信息，请参阅 [/nostdlib (c # 编译器选项) ](https://msdn.microsoft.com/library/ec197989-fa49-4725-a455-e06b551eb65f)。

## <a name="output"></a>输出
 使用以下选项可以指定高级输出选项。

 **调试信息** 指定编译器生成的调试信息的类型。 有关如何配置应用程序的调试性能的信息，请参阅[令映像更易于调试](https://msdn.microsoft.com/library/7d90ea7a-150f-4f97-98a7-f9c26541b9a3)。 此设置具有以下选项：

- **无**

   指定不会生成任何调试信息

- **full**

   允许将调试器附加到正在运行的程序。

- **pdbonly**

   允许在调试器中启动程序时进行源代码调试，但仅在正在运行的程序附加到调试器时才显示汇编程序。

  有关详细信息，请参阅 [/debug (c # 编译器选项) ](https://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969)。

  **文件对齐** 指定输出文件中各节的大小。 有效值为 **512**、 **1024**、 **2048**、 **4096**和 **8192**。 这些值以字节为单位。 每一节都在边界（此值的倍数）上对齐，这会影响输出文件的大小。 有关详细信息，请参阅 [/filealign (c # 编译器选项) ](https://msdn.microsoft.com/library/15cf1c98-3798-4ced-9f08-60619308a073)。

  **DLL 基址** 指定加载 DLL 的首选基址。 DLL 的默认基址由 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 公共语言运行时设置。 有关详细信息，请参阅 [/baseaddress (c # 编译器选项) ](https://msdn.microsoft.com/library/ce13c965-dfe4-4433-94f5-63b476e3a608)。

## <a name="see-also"></a>另请参阅
 [C# 编译器选项](https://msdn.microsoft.com/library/d3403556-1816-4546-a782-e8223a772e44) [生成页、项目设计器 (C#)](../../ide/reference/build-page-project-designer-csharp.md)
