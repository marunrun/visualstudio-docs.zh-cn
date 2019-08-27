---
title: 调试基础知识：寄存器窗口 |Microsoft Docs
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
- Registers window, about Registers window
- debugging [Visual Studio], Registers window
ms.assetid: ab354047-053e-4f94-8ac1-26e761442b6f
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c5c9380ccc9a21270da3c5832222976e4c7121e3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686720"
---
# <a name="debugging-basics-registers-window"></a>调试基础知识：寄存器窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

只有在“选项”对话框、“调试”节点中启用了地址级调试，“寄存器”窗口才可用。  
  
 寄存器是处理器（CPU）中的特殊区域，用于存储处理器当前正在处理的少量数据。 编译或解释源代码时会生成一些指令，这些指令根据需要将数据从内存移动到寄存器并再次移回。 相对于访问内存数据，访问寄存器数据的速度非常快，因此，比起需要处理器不断加载和卸载寄存器的代码，允许处理器将数据保留在寄存器并多次访问的代码的执行速度快得多。 为了更加便于编译器将数据保存在寄存器中并执行其他优化，应避免使用全局变量，而是尽可能地依靠局部变量。 以此方式编写的代码具有良好的引用局部性。 在某些语言中，如 C/C++ 中，程序员可以声明寄存器变量，该变量可指示编译器在任何时候尽量将变量保留在寄存器中。 有关详细信息，请参阅[寄存器关键字](https://msdn.microsoft.com/5b66905a-2f7f-4918-bb55-5e66d4bc50f9)。  
  
 寄存器可分为两类：通用寄存器和专用寄存器。 通用寄存器保存用于一般操作（如将两数相加或引用数组中的元素）的数据。 专用寄存器具有特定用途和专门的意义。 堆栈指针寄存器是一个好例子，处理器利用它跟踪程序的调用堆栈。 程序员可能不会直接处理堆栈指针，但它对于程序正确运行至关重要。 没有堆栈指针，处理器在函数调用完成后将不知道返回何处。  
  
 大多数通用寄存器只保存一个数据元素。 例如单个整数、浮点数或某一数组元素。 一些较新的处理器具有较大的寄存器，这种寄存器称为向量寄存器，可以保存一个较小的数据数组。 由于它们可以保存如此多的数据，向量寄存器对于涉及数组的运算处理得非常快。 向量寄存器最初是用在昂贵的高性能超级计算机上，但现在也可用于微处理器，此时它们在密集的图形操作中具有很大优势。  
  
 一个处理器通常有两组通用寄存器，一组针对浮点运算进行优化，一组针对整数运算进行优化。 因此，它们被称为浮点寄存器和整数寄存器。  
  
 托管代码在运行时被编译为用于访问微处理器的物理寄存器的本机代码。 “寄存器”窗口可以显示这些用于公共语言运行时或本机代码的物理寄存器。 “寄存器”窗口不显示用于脚本或 SQL 应用程序的寄存器信息，因为脚本和 SQL 都是不支持寄存器概念的语言。  
  
 有关显示“寄存器”窗口的详细信息，请参阅[使用寄存器窗口](../debugger/how-to-use-the-registers-window.md)。  
  
 当您查看**注册**窗口中，会看到如下面的示例条目：  
  
```  
EAX = 003110D8  
```  
  
 “=”号左边的符号是寄存器名称（这里是 EAX）。 符号“=”右边是寄存器内容。  
  
 “寄存器”窗口不仅可以看到寄存器的内容，还可以做更多事情。 当本机代码处于中断模式时，可以点击寄存器内容并编辑值。 此操作不应随意执行。 除非理解正在编辑的寄存器和它所包含的数据，草率编辑很可能导致程序崩溃或其他不良后果。 很遗憾，详细介绍各种 Intel 和 Intel 兼容处理器的寄存器组超出了本简介文章的范围。  
  
## <a name="register-groups"></a>寄存器组  
 为了减少混乱，“寄存器”窗口将寄存器组织成组。 右键单击“寄存器”窗口将看到包含一系列组的快捷菜单，可以根据需要显示或隐藏这些组。  
  
## <a name="see-also"></a>请参阅  
 [如何：使用“寄存器”窗口](../debugger/how-to-use-the-registers-window.md)   
 [调试器基础知识](../debugger/debugger-basics.md)
