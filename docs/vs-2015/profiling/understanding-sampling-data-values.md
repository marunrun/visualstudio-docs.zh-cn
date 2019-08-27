---
title: 了解采样数据值 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method
- Profiling Tools, sampling
ms.assetid: fad540a8-24b6-4ff9-91ce-e67e9a58399d
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 91a4a50ecc745c0b56167d6a5dbb1932af7ed2bf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145423"
---
# <a name="understanding-sampling-data-values"></a>了解采样数据值
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 分析工具的采样  分析方法按设置的间隔中断计算机处理器并收集函数调用堆栈。 调用堆栈  是一种动态结构，用于存储有关在处理器中执行的函数的信息。  
  
 **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  探查器分析确定处理器是否在执行目标进程中的代码。 如果处理器未执行目标进程中的代码，则丢弃样本。  
  
  如果处理器在执行目标代码，探查器会递增调用堆栈中每个函数的样本计数。 获取样本时，调用堆栈上只有一个函数当前在执行代码。 堆栈上的其他函数是函数调用层次结构中的父级，在等待其子级返回。  
  
  对于样本事件，探查器会递增当前在执行其指令的函数的独占  样本计数。 因为独占样本也是函数的总计（非独占  ）样本的一部分，所以前处于活动状态的函数的非独占样本计数也会递增。  
  
  探查器会递增调用堆栈上所有其他函数的非独占样本计数。  
  
## <a name="inclusive-samples"></a>非独占样本数  
 在目标函数执行过程中收集的样本总数。  
  
 这包括在函数代码直接执行过程中收集的样本以及在目标函数调用的子函数执行过程中收集的样本。  
  
## <a name="exclusive-samples"></a>独占样本数  
 在目标函数指令直接执行过程中收集的样本数。  
  
 独占样本数不包括在目标函数调用的函数执行过程中收集的样本。  
  
## <a name="inclusive-percent"></a>非独占百分比  
 函数或数据范围的非独占样本数占分析运行中的非独占样本数总数的百分比。  
  
## <a name="exclusive-percent"></a>独占百分比  
 函数或数据范围的独占样本数占分析运行中的独占样本数总数的百分比。  
  
## <a name="see-also"></a>请参阅  
 [如何：选择收集方法](../profiling/how-to-choose-collection-methods.md)   
 [分析性能工具数据](../profiling/analyzing-performance-tools-data.md)
