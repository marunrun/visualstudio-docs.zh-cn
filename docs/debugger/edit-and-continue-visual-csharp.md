---
title: 编辑并继续 (Visual C#) | Microsoft Docs
ms.date: 10/11/2017
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Edit and Continue
- Edit and Continue [C#]
- debugging [C#], Edit and Continue
ms.assetid: 591bd1b7-ef10-4d10-817b-3f92ca4be006
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 972ad0d772eee9b876f43bc3e2fcd032d4b7e0ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62851017"
---
# <a name="edit-and-continue-visual-c"></a>编辑并继续 (Visual C#)
 使用 C# 的“编辑并继续”，可以一边进行调试一边在中断模式下更改代码。 不必停止并重新启动调试会话即可应用更改。 在运行模式下，源编辑器是只读的。

 “编辑并继续”支持在调试会话期间可能做出的大多数更改，但有某些例外。 有关详细信息，请参阅[受支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)。

 编辑并继续支持在 Windows 10 和 x86 和 x64 应用程序面向.NET Framework 4.6 的 UWP 桌面或更高版本 （.NET Framework 是桌面版）。

 > [!NOTE]
 > 不受支持的应用程序和平台包括 ASP.NET 5、 Silverlight 5 和 Windows 8.1。

 如果启用了“编辑并继续”，在使用调试器执行命令（如“继续”、“单步执行”、“设置下一语句”）或在调试器窗口中执行函数计算时，会自动应用受支持的更改。

 有关详细信息，请参阅[如何：使用“编辑并继续”(C#)](../debugger/how-to-use-edit-and-continue-csharp.md)。

## <a name="see-also"></a>请参阅
- [如何：使用“编辑并继续”(C#)](../debugger/how-to-use-edit-and-continue-csharp.md)
- [支持的代码更改（C# 和 Visual Basic）](../debugger/supported-code-changes-csharp.md)