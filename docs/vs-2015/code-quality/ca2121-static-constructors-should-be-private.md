---
title: CA2121：静态构造函数应为私有Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2121
- StaticConstructorsShouldBePrivate
helpviewer_keywords:
- CA2121
- StaticConstructorsShouldBePrivate
ms.assetid: ee93c620-8fc1-4e47-866c-d389c3ca9f2e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7f95b33e1391ca755a6c0df261fa2bd05bd3c7a0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544308"
---
# <a name="ca2121-static-constructors-should-be-private"></a>CA2121:静态构造函数应为私有
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|StaticConstructorsShouldBePrivate|
|CheckId|CA2121|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型具有非私有的静态构造函数。

## <a name="rule-description"></a>规则描述
 静态构造函数（也称为类构造函数）用于初始化类型。 系统在创建第一个类型实例或引用任何静态成员之前调用静态构造函数。 用户无法控制何时调用静态构造函数。 如果静态构造函数不是私有，则系统以外的代码可以调用它。 根据构造函数中执行的操作，这可能导致意外行为。

 此规则由 c # 和 Visual Basic .NET 编译器强制执行。

## <a name="how-to-fix-violations"></a>如何解决冲突
 冲突通常由下列操作之一引起：

- 你为类型定义了静态构造函数，但未将其设为私有。

- 编程语言编译器向类型添加了默认静态构造函数，但未将其设为私有。

  若要修复第一种冲突，请将静态构造函数设为私有。 若要修复第二种类型，请将专用静态构造函数添加到您的类型中。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示这些冲突。 如果软件设计需要显式调用静态构造函数，则可能是由于设计出现严重缺陷并且应该查看。
