---
title: DA0001：使用 StringBuilder 进行串联 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0001
- vs.performance.rules.DAUseStringBuilder
- vs.performance.1
- vs.performance.rules.DA0001
ms.assetid: a7cc7613-ad5f-48c8-bd2b-56372cc12dfc
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cb8da704832031d69156eee8863b689e7956f025
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295953"
---
# <a name="da0001-use-stringbuilder-for-concatenations"></a>DA0001：使用 StringBuilder 进行串联
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅[DA0001：使用 StringBuilder 进行串联](https://docs.microsoft.com/visualstudio/profiling/da0001-use-stringbuilder-for-concatenations)。  
  
|||  
|-|-|  
|规则 ID|DA0001|  
|类别|.NET Framework 使用情况|  
|分析方法|采样<br /><br /> 检测|  
|消息|请考虑使用 StringBuilder 进行字符串串联|  
|消息类型|警告|  
  
## <a name="cause"></a>原因  
 对 System.String.Concat 的调用是分析数据的重要组成部分。 请考虑使用 <xref:System.Text.StringBuilder> 类从多个段构造字符串。  
  
## <a name="rule-description"></a>规则说明  
 <xref:System.String> 对象是不可变的。 因此，对字符串进行任何修改都将创建新的字符串对象并对原始对象进行垃圾回收。 无论显式调用 String.Concat 或使用字符串串联运算符（如 + 或 +=），此行为都是相同的。 如果频繁调用这些方法，如以紧密循环地方式将字符添加到字符串，则会导致程序性能降低。  
  
 StringBuilder 类是可变的对象，与 System.String 不同，StringBuilder 上修改此类的实例的大多数方法都将返回对该相同实例的引用。 可以插入字符或将文本追加到 StringBuilder 实例，并删除或替换实例中的字符，而无需分配新的实例和删除原始实例。  
  
## <a name="how-to-investigate-a-warning"></a>如何调查警告  
 双击“错误列表”窗口中的消息，导航到采样分析数据的[函数详细信息视图](../profiling/function-details-view.md)。 查找程序中使用字符串串联最频繁的部分。 请对复杂的字符串操作使用 StringBuilder 类，包括频繁使用的字符串串联操作。  
  
 若要深入了解如何使用字符串，请参阅 Microsoft 模式和做法库中[第 5 章 - 提高托管代码性能](https://go.microsoft.com/fwlink/?LinkId=177816)的[字符串操作](https://go.microsoft.com/fwlink/?LinkId=177817)部分。
