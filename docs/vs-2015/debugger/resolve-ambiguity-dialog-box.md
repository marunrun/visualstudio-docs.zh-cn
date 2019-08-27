---
title: 解析多义性对话框的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.Disambig
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Resolve Ambiguity dialog box
- debugger, Resolve Ambiguity dialog box
- debugging [C++], resolving ambiguity
ms.assetid: d9f47455-a116-4c84-8bad-2dfbf4d77f74
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b35d305bbd011adc02692cd7c9c687ac0bfc7d45
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148794"
---
# <a name="resolve-ambiguity-dialog-box"></a>“解析多义性”对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当调试器无法选择要显示的位置时，将显示 `Resolve Ambiguity` 对话框。 例如，如果正在使用 C++ 模板，则可以从一个函数模板中创建多个函数。 如果调试器在模板的源位置停止，并且选择了 `Go To Disassembly`，则调试器会有多个选项。 从模板创建的每个函数都有它自己的反汇编代码，而调试器不知道需要查看哪些代码。 利用 `Resolve Ambiguity` 对话框，您可以从所有对应位置的列表中选择所需的位置。  
  
 `Choose the specific location`  
 列出与命令对应的所有位置。  
  
 `Address`  
 显示每个函数的内存地址。  
  
 `Function`  
 显示每个函数的名称。  
  
 `Module`  
 显示包含函数对象代码的模块（EXE 或 DLL）。  
  
## <a name="see-also"></a>请参阅  
 [调试器中的表达式](../debugger/expressions-in-the-debugger.md)
