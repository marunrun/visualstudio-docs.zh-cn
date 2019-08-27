---
title: CA1064:异常应该是公共 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1064
- ExceptionsShouldBePublic
helpviewer_keywords:
- ExceptionsShouldBePublic
- CA1064
ms.assetid: 83eb224c-2456-4368-acf4-3b3378e67759
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 00d188188f722907c2bac20e84cb9291ef8bc0fe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200430"
---
# <a name="ca1064-exceptions-should-be-public"></a>CA1064:异常应该是公共的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ExceptionsShouldBePublic|
|CheckId|CA1064|
|类别|Microsoft.Design|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 非公共异常直接派生<xref:System.Exception>， <xref:System.SystemException>，或<xref:System.ApplicationException>。

## <a name="rule-description"></a>规则说明
 内部异常才会显示在其自己的内部范围内。 当异常超出内部范围后，只能使用基异常来捕获该异常。 如果内部异常继承自<xref:System.Exception>， <xref:System.SystemException>，或<xref:System.ApplicationException>，外部代码将没有足够的信息来了解应如何处理异常。

 但是，如果代码具有更高版本用于在基础内部异常的公共异常，则根据常理来假设代码进一步扩展将能够执行某些与基异常智能操作。 公共异常将具有比通过 T:System.Exception、 T:System.SystemException 或 T:System.ApplicationException 提供的功能的详细信息。

## <a name="how-to-fix-violations"></a>如何解决冲突
 公开异常或派生中不是公共异常的内部异常<xref:System.Exception>， <xref:System.SystemException>，或<xref:System.ApplicationException>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果您确信在所有情况下将其自己内部的作用域内捕获到专用的异常，禁止显示此规则的消息。

## <a name="example"></a>示例
 因为异常类直接派生自异常，内部，则将触发此规则在第一个示例方法，FirstCustomException。 因为尽管也直接从异常派生类，该类被声明为公共规则不会激发 SecondCustomException 类上。 第三个类也不会触发该规则，因为它不直接从派生<xref:System.Exception?displayProperty=fullName>， <xref:System.SystemException?displayProperty=fullName>，或<xref:System.ApplicationException?displayProperty=fullName>。

 [!code-csharp[FxCop.Design.ExceptionsShouldBePublic.CA1064#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.design.exceptionsshouldbepublic.ca1064/cs/ca1064 - exceptionsshouldbepublic.cs#1)]
