---
title: 如何：使用查找程序工具 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Window Finder Tool
ms.assetid: 5841926b-08c3-4e43-88bd-4223d04f9aef
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 00535fd336f504afcebdd24a4d009a10f7f6ff33
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440308"
---
# <a name="how-to-use-the-finder-tool"></a>如何：使用查找程序工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用中查找程序工具**查找窗口**对话框以显示窗口属性或消息。 查找程序工具还可以找到已禁用的子窗口，并识别哪个窗口以突出显示如果禁用子级窗口重叠。  
  
 ![Spy&#43; &#43;窗口中查找对话框](../debugger/media/icon-spy-find.png "Icon_Spy + + （_f)")  
在查找窗口对话框中查找程序工具  
  
 在下面的步骤 3 后上, 图显示查找窗口对话框。  
  
### <a name="to-display-window-properties-or-messages"></a>若要显示窗口属性或消息  
  
1. 排列窗口，以便 Spy + + 和目标窗口中可见。  
  
2. 从**Spy**菜单中，选择**查找窗口**。  
  
     [查找窗口对话框](../debugger/find-window-dialog-box.md)随即打开。  
  
3. 拖动**查找程序工具**通过目标窗口。  
  
     拖动该工具中，**查找窗口**对话框显示有关所选的窗口的详细信息。  
  
     - 或 -  
  
     如果有你想要检查 （例如，复制从调试器） 窗口的句柄，则键入到**处理**文本框。  
  
    > [!TIP]
    > 若要减少屏幕混乱，请选择**隐藏 Spy**选项。 此选项将隐藏主 Spy + + 窗口中，并仅留下**查找窗口**对话框显示在其他应用程序的前面。 Spy + + 主窗口将还原时，单击**确定**或**取消**，或如果清除**隐藏 Spy + +** 选项。  
  
4. 下**显示**，选择**属性**或**消息**。  
  
5. 按“确定”。  
  
     如果所选**属性**，则[窗口属性对话框](../debugger/window-properties-dialog-box.md)随即打开。 如果所选**消息**即[消息视图](../debugger/messages-view.md)窗口随即打开。  
  
## <a name="see-also"></a>请参阅  
 [Spy++ 视图](../debugger/spy-increment-views.md)   
 [使用 Spy++](../debugger/using-spy-increment.md)   
 [Spy++ 参考](../debugger/spy-increment-reference.md)
