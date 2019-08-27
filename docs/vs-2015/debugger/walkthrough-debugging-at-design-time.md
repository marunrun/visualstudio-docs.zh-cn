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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149419"
---
# <a name="walkthrough-debugging-at-design-time"></a>演练：在设计时调试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用 Visual Studio**即时**窗口在你的应用程序未运行时执行函数或子例程。 如果函数或子例程包含断点，Visual Studio 将在相应的点中断执行。 随后即可使用调试器窗口检查程序状态。 此功能称为在设计时调试。  
  
 下面的过程演示如何使用此功能。  
  
### <a name="to-hit-breakpoints-from-the-immediate-window"></a>以命中断点，从即时窗口  
  
1. 将以下代码粘贴到 Visual Basic 控制台应用程序：  
  
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
  
2. 在读取时，在行上设置断点`s="Add BreakPoint Here"`。  
  
3. 键入以下内容中的**即时**窗口： `?MyFunction<enter>`  
  
4. 验证命中断点和调用堆栈准确。  
  
5. 上**调试**菜单上，单击**继续**，并验证是否仍处于设计模式。  
  
6. 键入以下内容中的**即时**窗口： `?MyFunction<enter>`  
  
7. 键入以下内容中的**即时**窗口： `?MySub<enter>`  
  
8. 验证是否命中了断点，并检查静态变量的值`i`中**局部变量**窗口。 它应具有的值为 3。  
  
9. 验证调用堆栈准确。  
  
10. 上**调试**菜单上，单击**继续**，并验证是否仍处于设计模式。  
  
## <a name="see-also"></a>请参阅  
 [调试器安全](../debugger/debugger-security.md)   
 [调试器基础知识](../debugger/debugger-basics.md)
