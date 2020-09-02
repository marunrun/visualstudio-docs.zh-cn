---
title: 如何：在托管代码中设置线程名称 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Thread.Name property
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c0c4d74a-0314-4b71-81c9-b0b019347ab8
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b800fbd2f39d75f110a059c70b87a203eb72e7d6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157669"
---
# <a name="how-to-set-a-thread-name-in-managed-code"></a>如何：在托管代码中设置线程名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 的任何版本中都可以使用线程命名功能。 线程命名功能对跟踪“线程”窗口中的线程非常有用。 由于 " **线程** " 窗口在 Visual Studio Express 版本中不可用，因此线程命名在 Express 版本中没有实用程序。  
  
 若要在托管代码中设置线程名称，请使用 <xref:System.Threading.Thread.Name%2A> 属性。  
  
## <a name="example"></a>示例  
  
```  
Public Class Needle  
    ' This method will be called when the thread is started.  
    Sub Baz()  
        Console.WriteLine("Needle Baz is running on another thread")  
    End Sub  
End Class  
  
Sub Main()  
    Console.WriteLine("Thread Simple Sample")  
    Dim oNeedle As New Needle()  
   ' Create a Thread object.   
    Dim oThread As New System.Threading.Thread(AddressOf oNeedle.Baz)  
    ' Set the Thread name to "MainThread".  
    oThread.Name = "MainThread"  
    ' Starting the thread invokes the ThreadStart delegate  
    oThread.Start()  
End Sub  
```  
  
## <a name="see-also"></a>另请参阅  
 [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [如何：在本机代码中设置线程名称](../debugger/how-to-set-a-thread-name-in-native-code.md)
