---
title: CA1030:在适用处使用事件 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 9d00db6f9a00a273198cc50704d65ed6d2e4bb33
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157704"
---
# <a name="ca1030-use-events-where-appropriate"></a>CA1030:在适用处使用事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseEventsWhereAppropriate|
|CheckId|CA1030|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 公共、 受保护或私有方法名称以与以下项之一：

- AddOn

- RemoveOn

- 激发

- 引发

## <a name="rule-description"></a>规则说明
 该规则检测名称通常用于事件的方法。 事件遵循观察者或发布-订阅设计模式;一个对象的状态更改必须传递给其他对象时使用它们。 如果调用的方法获取响应明确定义的状态更改，应通过事件处理程序调用该方法。 调用该方法的对象应引发事件而不是直接调用该方法。

 在用户界面应用程序的用户操作，例如单击按钮会导致要执行的代码段中找到事件的一些常见示例。 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]事件模型并不局限于用户界面; 应使用任何位置您必须进行通信的状态更改为一个或多个对象。

## <a name="how-to-fix-violations"></a>如何解决冲突
 如果对象的状态发生更改时调用该方法，则应考虑更改设计以确保使用[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]事件模型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果该方法并不适用于禁止显示此规则的警告[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]事件模型。
