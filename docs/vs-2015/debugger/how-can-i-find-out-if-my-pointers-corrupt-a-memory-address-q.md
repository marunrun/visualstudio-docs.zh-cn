---
title: 如何查明指针是否损坏了内存地址？ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- addresses, pointers corrupting memory address
- memory, corruption
- pointers, corrupting memory addresses
- memory address corruption by pointers
- debugging [C++], memory corruption
- corrupted memory address
ms.assetid: a147c939-4fb1-415c-8410-cf303781e9e8
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 80947590215258521c3de5042bd981de7582fbda
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205477"
---
# <a name="how-can-i-find-out-if-my-pointers-corrupt-a-memory-address"></a>如何查明指针是否损坏了内存地址？
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

问题描述  
 我认为我的一个指针可能损坏了地址 0x00408000 处的内存。 如何查明该地址处所发生的情况？  
  
## <a name="solution"></a>解决方案  
  
#### <a name="check-for-heap-corruption"></a>检查堆损坏  
  
- 大多数内存损坏实际上是由堆损坏引起的。 尝试使用 Global Flags Utility (gflags.exe) 或 pageheap.exe。 请参阅[ http://support.microsoft.com/default.aspx?scid=kb; en-我们; 286470](http://support.microsoft.com/default.aspx?scid=kb;en-us;286470)。  
  
#### <a name="to-find-where-the-memory-address-is-modified"></a>若要查找内存地址改变的位置  
  
1. 在 0x00408000 处设置一个数据断点。 请参阅[设置数据更改断点（仅限本机 C++）](../debugger/using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus_only)。  
  
2. 当命中断点时，使用“内存”窗口，以查看从 0x00408000 开始的内存内容  。 有关详细信息，请参阅[内存窗口](../debugger/memory-windows.md)。  
  
## <a name="see-also"></a>请参阅  
 [调试本机代码常见问题](../debugger/debugging-native-code-faqs.md)   
 [调试本机代码](../debugger/debugging-native-code.md)
