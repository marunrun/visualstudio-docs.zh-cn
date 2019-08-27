---
title: 如何：编辑寄存器值 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.register.edit
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
- Registers window, editing register values
- register values
ms.assetid: e27b6bd8-e6d4-4f1d-8a86-9f4047bb1167
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7f0cd04b054d51119f6f6c1b0275c4f781656bff
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63438306"
---
# <a name="how-to-edit-a-register-value"></a>如何：编辑寄存器值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

只有在“选项”对话框中的“调试”节点下启用了地址级调试后，“寄存器”窗口才可用。  
  
### <a name="to-change-the-value-of-a-register"></a>更改寄存器值  
  
1. 在“寄存器”窗口中，使用 Tab 或鼠标可以将插入点移到要更改的值的位置。 在开始键入之前，光标必须位于要覆盖的值之前。  
  
2. 键入新值。  
  
    > [!CAUTION]
    > 更改寄存器值（特别是 EIP 和 EBP 寄存器中的值）可能会影响程序的执行。  
  
    > [!CAUTION]
    > 编辑浮点值时，由于要将小数部分从十进制转换为二进制，因此所得的结果可能存在微小误差。 甚至看起来无关紧要的编辑都能引起浮点变量中某些最不重要的数据位发生变化。  
  
## <a name="see-also"></a>请参阅  
 [如何：使用“寄存器”窗口](../debugger/how-to-use-the-registers-window.md)
