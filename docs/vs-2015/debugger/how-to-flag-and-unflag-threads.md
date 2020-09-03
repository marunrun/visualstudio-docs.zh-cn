---
title: 如何：标记线程和取消标记线程 | Microsoft Docs
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
- treads, switching [debugging]
ms.assetid: 952d579d-6911-413e-b3e5-54e7e797e70c
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b6d6a49dd9b90172686a90d92e6b630dd70b5cf0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189440"
---
# <a name="how-to-flag-and-unflag-threads"></a>如何：标记线程和取消标记线程
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以通过使用 " **线程**"、" **并行堆栈**"、" **并行监视**" 和 " **GPU 线程** " 窗口中的图标来标记要特别注意的线程。 此图标有助于您和其他人将标记的线程与其他线程区别开来。  
  
 标记线程还会在 "**调试位置**" 工具栏上的 "**线程**" 列表中接收特殊处理。 此列表可以显示所有线程或仅显示标记的线程。 标记线程时， **线程** 列表会自动切换为仅显示标记的线程，但您可以将其切换回以显示所有线程。  
  
### <a name="to-flag-or-unflag-a-thread-by-using-the-threads-window"></a>使用“线程”窗口标记或取消标记线程  
  
- 在 " **线程** " 窗口中，找到感兴趣的线程，并单击标志图标以选择或清除标志。  
  
### <a name="to-unflag-all-threads"></a>取消标记所有线程  
  
- 在“线程”窗口中右击任意线程，然后单击“取消标志所有线程” 。  
  
### <a name="to-display-only-flagged-threads"></a>仅显示标记的线程  
  
- 在调试窗口选择标记按钮。  
  
### <a name="to-flag-just-my-code"></a>标记“仅我的代码”  
  
1. 在“线程”窗口顶部的工具栏中，单击标志图标。  
  
2. 在下拉列表中，单击“标记‘仅我的代码’”。  
  
### <a name="to-flag-threads-that-are-associated-with-selected-modules"></a>标记与选定模块关联的线程  
  
1. 在“线程”窗口的工具栏中，单击标志图标。  
  
2. 在下拉列表中，单击“标记自定义模块选择”。  
  
3. 在“选择模块”对话框中，选择需要的模块。  
  
4. （可选）在“搜索”框中，键入用于搜索特定模块的字符串。  
  
5. 单击 **“确定”** 。  
  
## <a name="see-also"></a>另请参阅  
 [调试多线程应用程序](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [演练：调试多线程应用程序](../debugger/walkthrough-debugging-a-multithreaded-application.md)
