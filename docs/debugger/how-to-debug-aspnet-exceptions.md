---
title: 如何：调试 ASP.NET 异常 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], ASP.NET exceptions
- ASP.NET, exceptions
- exceptions, ASP.NET
ms.assetid: 1810096e-de8c-435e-be3d-f365d0cd0a6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 9f8391d355b2f540db4e38486b8992d940336464
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733787"
---
# <a name="how-to-debug-aspnet-exceptions"></a>如何：调试 ASP.NET 异常
调试异常是开发可靠的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 应用程序的重要一步。 有关如何调试异常的常规信息，请参阅[使用调试器管理异常](../debugger/managing-exceptions-with-the-debugger.md)。

 若要调试未处理的 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 异常，必须确保调试器能够在发生这些异常时停止。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 运行时有一个顶级异常处理程序。 因此，默认情况下，调试器绝不会在未经处理的异常中中断。 若要在引发异常时中断调试器，必须在“异常”对话框中为该特定异常选择“发生以下异常时中断:引发的异常”设置。

 如果启用了“仅我的代码”，则当 .NET 方法或其他系统代码中引发异常时，“发生以下异常时中断:引发的异常”不会导致调试器立即中断。 执行将继续，直至调试器命中非系统代码时才中断。 因此，不必在发生异常时逐句通过系统代码。

 “仅我的代码”提供了另一个可能更有用的选项：“发生以下异常时中断:用户未处理的异常”。 如果为异常选择此设置，则调试器将在用户代码中中断执行，但是仅当异常没有被用户代码捕获和处理时，它才这样做。 此设置会使顶级 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 异常处理程序不起作用，因为该处理程序位于非用户代码中。

### <a name="to-enable-debugging-of-aspnet-exceptions-with-just-my-code"></a>启用 ASP.NET 异常调试和“仅我的代码”

1. 在“调试”菜单上，单击“异常” 。

     随即会出现“异常”对话框。

2. 在“公共语言运行时异常”行上，选择“引发”或“用户未处理的异常”  。

     若要使用“用户未处理的异常”设置，必须启用“仅我的代码” 。

### <a name="to-use-best-practices-for-aspnet-exception-handling"></a>采用 ASP.NET 异常处理的最佳做法

- 在可能引发您知道如何处理的可预见异常的代码周围放置 `try ... catch` 块。 例如，如果应用程序调用 XML Web services 或直接调用 SQL Server，则应将该代码置于 try … catch 块中，因为此过程中可能会发生大量异常。

## <a name="see-also"></a>请参阅
- [调试 ASP.NET 应用程序](../debugger/how-to-enable-debugging-for-aspnet-applications.md)