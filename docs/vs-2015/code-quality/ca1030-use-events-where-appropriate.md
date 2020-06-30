---
title: CA1030：在适当的位置使用事件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseEventsWhereAppropriate
- CA1030
helpviewer_keywords:
- CA1030
- UseEventsWhereAppropriate
ms.assetid: ea051367-deeb-40f9-9b65-eb818f1e133a
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1313c5ee79a7a13d3eb937a3431b13ea393857d1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544516"
---
# <a name="ca1030-use-events-where-appropriate"></a>CA1030:在适用处使用事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|UseEventsWhereAppropriate|
|CheckId|CA1030|
|Category|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 公共、受保护或私有方法名称以下列之一开头：

- 加载项

- RemoveOn

- Fire

- 提出

## <a name="rule-description"></a>规则描述
 该规则检测名称通常用于事件的方法。 事件遵循观察程序或发布-订阅设计模式;当必须将一个对象中的状态更改传递到其他对象时，使用它们。 如果调用方法以响应明确定义的状态更改，则应由事件处理程序调用方法。 调用该方法的对象应引发事件而不是直接调用该方法。

 事件的一些常见示例位于用户界面应用程序中，用户操作（例如单击按钮）会导致执行代码段。 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]事件模型并不局限于用户界面; 应在必须将状态更改传达给一个或多个对象的任何地方使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 如果在对象的状态发生更改时调用该方法，则应考虑将设计更改为使用 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 事件模型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果该方法不能与事件模型一起使用，则禁止显示此规则发出的警告 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。
