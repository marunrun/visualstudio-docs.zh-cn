---
title: 如何：使用寄存器窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.registers
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
- registers, debugging
- register contents
- flags, Registers window
- register groups
- debugging [Visual Studio], Registers window
- Registers window
ms.assetid: 2918ffa2-562f-40d6-9053-ef321bbeb767
caps.latest.revision: 42
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 233092af638824c462a6d9a47865a1c6f5fd9397
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697465"
---
# <a name="how-to-use-the-registers-window"></a>如何：使用寄存器窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

寄存器窗口是在启用了地址级调试时才可用**选项**对话框中，**调试**节点，**常规**类别。  
  
 **注册**窗口显示寄存器内容。 如果将保留**注册**窗口打开状态，因为单步执行应用程序，可以看到寄存器值发生更改，在代码执行。 最近更改过的值显示为红色。 您可以编辑寄存器的值。 有关详细信息，请参阅[如何：编辑寄存器值](../debugger/how-to-edit-a-register-value.md)。  
  
 为了减少混乱，“寄存器”窗口将寄存器组织成组，具体情况随平台和处理器类型的不同而不同。 可以根据需要显示或隐藏组。 有关详细信息，请参阅[如何：显示和隐藏寄存器组](../debugger/how-to-display-and-hide-register-groups.md)。  
  
 有关寄存器和寄存器窗口背后概念的简要介绍，请参阅[调试基础知识：寄存器窗口](../debugger/debugging-basics-registers-window.md)。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### <a name="to-display-the-registers-window"></a>显示“寄存器”窗口  
  
- 上**调试**菜单中，选择**Windows**，然后选择**注册**。  
  
     调试器必须正在运行或处于中断模式。  
  
    > [!NOTE]
    > 寄存器信息对于脚本或 SQL 应用程序不可用。  
  
## <a name="see-also"></a>请参阅  
 [调试基础知识：寄存器窗口](../debugger/debugging-basics-registers-window.md)   
 [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)   
 [调试基础知识：“寄存器”窗口](../debugger/debugging-basics-registers-window.md)
