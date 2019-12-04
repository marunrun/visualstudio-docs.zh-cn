---
title: 了解内存分配数据值和对象生存期数据值
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .NET memory profiling method
- Profiling Tools, .NET memory method
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 6eec0c4bc5fc27e07bc04a8445ca14ce538ac376
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779995"
---
# <a name="understand-memory-allocation-and-object-lifetime-data-values"></a>了解内存分配数据值和对象生存期数据值

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具的 *.NET 内存分配*分析工具收集有关在分配中创建或在垃圾回收中销毁的对象大小和数量的信息，并收集事件发生时有关函数*调用堆栈*的其他信息。 调用堆栈  是一种动态结构，用于存储有关在处理器中执行的函数的信息。

.NET 内存分配分析方法在被分析的应用程序中每次分配 .NET Framework 对象时都中断计算机处理器。 同时收集对象生存期数据时，探查器会在每个 .NET Framework 垃圾回收之后中断处理器。 会为每个分析的函数以及每种类型的对象聚合数据。

## <a name="allocation-data"></a>分配数据

内存事件发生时，会递增分配或销毁的内存对象的总计数和大小。

内存分配事件发生时，探查器会递增调用堆栈中每个函数的样本计数。 收集数据时，调用堆栈上只有一个函数当前在执行自己函数体中的代码。 堆栈上的其他函数是函数调用层次结构中的父级，在等待它们调用的函数返回。

- 对于分配事件，探查器会递增当前在执行其指令的函数的独占  样本计数。 因为独占样本也是函数的总计（非独占  ）样本的一部分，所以前处于活动状态的函数的非独占样本计数也会递增。

- 探查器会递增调用堆栈上所有其他函数的非独占样本计数。

## <a name="lifetime-data"></a>生存期数据

.NET Framework 的垃圾回收器会为应用程序管理内存的分配和释放。 为优化垃圾回收器的性能，将托管堆分为三代：第 0 代、第 1 代和第 2 代。 运行时的垃圾回收器将新对象存储在第 0 代中。 未回收的对象将会升级并存储在第 1 代和第 2 代中。

垃圾回收器通过释放整个代的对象来回收内存。 对于分析的应用程序创建的对象，“对象生存期”视图显示对象的数量和大小以及回收它们时的代。
