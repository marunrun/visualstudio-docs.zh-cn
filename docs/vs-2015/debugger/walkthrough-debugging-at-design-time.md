---
title: 演练：在设计时调试 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], design-time
- breakpoints, design-time debugging
- Immediate window, design-time debugging
- design-time debugging
ms.assetid: 35bfdd2c-6f60-4be1-ba9d-55fce70ee4d8
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 54466cc3561c194199bbad2b35cd00433da2b0f3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149419"
---
# <a name="walkthrough-debugging-at-design-time"></a>演练：在设计时调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当应用程序未运行时，可以使用 Visual Studio 的 " **即时** " 窗口来执行函数或子例程。 如果函数或子例程包含断点，则 Visual Studio 将在适当的点中断执行。 随后即可使用调试器窗口检查程序状态。 此功能称为“在设计时调试”。  
  
 下面的过程演示如何使用此功能。  
  
### <a name="to-hit-breakpoints-from-the-immediate-window"></a>从 "即时" 窗口命中断点  
  
1. 将以下代码粘贴到 Visual Basic 控制台应用程序中：  
  
    ```  
    Module Module1  
  
        Sub Main()  
            MySub()  
        End Sub  
  
        Function MyFunction() As Decimal  
            Static i As Integer  
            i = i + 1  
            Dim s As String  
  
            s = "Add Breakpoint here"  
            Return 4  
        End Function  
  
        Sub MySub()  
            MyFunction()  
        End Sub  
    End Module  
    ```  
  
2. 在读取、的行上设置断点 `s="Add BreakPoint Here"` 。  
  
3. 在 " **即时** " 窗口中键入以下内容： `?MyFunction<enter>`  
  
4. 验证是否命中了断点，以及调用堆栈是否准确。  
  
5. 在 " **调试** " 菜单上，单击 " **继续**"，然后验证是否仍处于设计模式。  
  
6. 在 " **即时** " 窗口中键入以下内容： `?MyFunction<enter>`  
  
7. 在 " **即时** " 窗口中键入以下内容： `?MySub<enter>`  
  
8. 验证是否已命中断点，并检查 `i` " **局部变量** " 窗口中静态变量的值。 它的值应为3。  
  
9. 验证调用堆栈是否准确。  
  
10. 在 " **调试** " 菜单上，单击 " **继续**"，然后验证是否仍处于设计模式。  
  
## <a name="see-also"></a>另请参阅  
 [调试器安全性](../debugger/debugger-security.md)   
 [调试器基础知识](../debugger/debugger-basics.md)
