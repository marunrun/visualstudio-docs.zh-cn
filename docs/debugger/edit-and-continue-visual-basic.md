---
title: 编辑并继续 (Visual Basic) |Microsoft Docs
ms.date: 10/11/2017
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue, 64-bit
- Edit and Continue [Visual Basic]
- debugging [Visual Basic], Edit and Continue
- Visual Basic, Edit and Continue
- 64-bit Edit and Continue
ms.assetid: 7e90f34f-e699-45ab-a4c9-a4b527c498c8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f73b67ac4268c04dfa9ff7ab020891623f528f9b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62851256"
---
# <a name="edit-and-continue-visual-basic"></a>编辑并继续 (Visual Basic)
“编辑并继续”是 [!INCLUDE [vbprvb](../code-quality/includes/vbprvb_md.md)] 调试中的一项功能，可让你在中断模式下在代码运行时更改代码。 在应用代码编辑后，可以继续执行新编辑过的代码并观察效果。

 每次进入中断模式时都可以使用“编辑并继续”功能。 在中断模式下，指令指针（ 源窗口中的黄色箭头）指向包含方法或属性中下一步将被执行的语句的行。

 “编辑并继续”支持在调试会话期间可能做出的大多数更改，但有某些例外。 有关详细信息，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

 如果进行了未经授权的编辑，则所做更改会被加上紫色波浪下划线标记，并且会在任务列表中显示一个任务。 如果要继续使用“编辑并继续”功能，必须撤消未经授权的编辑。 在“编辑并继续”之外，可能允许执行某些未经授权的编辑。 如果要保留这种未经授权的编辑的结果，必须停止调试并重新启动应用程序。

 编辑并继续支持适用于 Windows 10 UWP 应用和面向.NET Framework 4.6 的 x86 和 x64 应用程序在桌面或更高版本 （.NET Framework 是桌面版）。

 > [!NOTE]
 > 不受支持的应用程序和平台包括 ASP.NET 5、 Silverlight 5 和 Windows 8.1。

 使用 **附加到进程** 启动的调试不支持“编辑并继续”。 优化代码或混合代码（托管和原生）不支持“编辑并继续”。 有关详细信息，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

 本节中各个主题提供的详细信息涉及：如何使用此功能，允许进行哪些类型的更改。

## <a name="in-this-section"></a>本节内容
 [如何：应用在中断模式下使用编辑并继续编辑](../debugger/how-to-apply-edits-in-break-mode-with-edit-and-continue.md)介绍了如何将应用在中断模式下编辑代码。

 [支持代码更改 (C#和 Visual Basic)](../debugger/supported-code-changes-csharp.md)描述的编辑的类型不能为在执行[!INCLUDE [vb_current_short](../debugger/includes/vb_current_short_md.md)]编辑并继续。

## <a name="related-sections"></a>相关章节
 [编辑并继续](../debugger/edit-and-continue.md)上编辑并继续提供主题的列表。
