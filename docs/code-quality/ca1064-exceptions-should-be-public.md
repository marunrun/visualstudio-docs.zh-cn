---
title: CA1064:异常应该是公共的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1064
- ExceptionsShouldBePublic
helpviewer_keywords:
- ExceptionsShouldBePublic
- CA1064
ms.assetid: 83eb224c-2456-4368-acf4-3b3378e67759
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b17ccfe66875588ac19c587ff6fcbd889d1e6a44
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922320"
---
# <a name="ca1064-exceptions-should-be-public"></a>CA1064:异常应该是公共的

|||
|-|-|
|TypeName|ExceptionsShouldBePublic|
|CheckId|CA1064|
|类别|Microsoft.Design|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
非公共异常直接<xref:System.Exception>派生自、 <xref:System.SystemException>或<xref:System.ApplicationException>。

## <a name="rule-description"></a>规则说明
内部异常仅在其自己的内部范围内可见。 当异常超出内部范围后，只能使用基异常来捕获该异常。 如果内部异常继承自<xref:System.Exception>， <xref:System.SystemException>，或<xref:System.ApplicationException>，外部代码将没有足够的信息来了解应如何处理异常。

但是, 如果代码有一个公共异常, 稍后将其用作内部异常的基, 则假设代码更进一步的操作将能够使用基本异常进行智能化。 公共异常将提供比、 <xref:System.Exception> <xref:System.SystemException>或<xref:System.ApplicationException>提供的信息更多的信息。

## <a name="how-to-fix-violations"></a>如何解决冲突
使异常成为公共异常, 或从非<xref:System.Exception>、 <xref:System.SystemException>或<xref:System.ApplicationException>的公共异常派生内部异常。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果你确定在其自己的内部范围内将捕获私有异常, 则禁止显示此规则的消息。

## <a name="example"></a>示例
此规则在第一个示例方法 FirstCustomException 上激发, 因为 exception 类直接从 Exception 派生, 并且是 internal。 此规则不会在 SecondCustomException 类上激发, 因为尽管类也直接派生自异常, 但该类声明为公共类。 第三个类还不会激发规则, 因为它不是直接从<xref:System.Exception?displayProperty=fullName>、 <xref:System.SystemException?displayProperty=fullName>或<xref:System.ApplicationException?displayProperty=fullName>派生的。

[!code-csharp[FxCop.Design.ExceptionsShouldBePublic.CA1064#1](../code-quality/codesnippet/CSharp/ca1064-exceptions-should-be-public_1.cs)]
