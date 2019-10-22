---
title: CA1032：实现标准异常构造函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1032
- ImplementStandardExceptionConstructors
helpviewer_keywords:
- CA1032
- ImplementStandardExceptionConstructors
ms.assetid: a8623c56-273a-4c95-8d83-95911a042be7
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b471387db3ce52944ffad3841dc7e946c4d44873
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661880"
---
# <a name="ca1032-implement-standard-exception-constructors"></a>CA1032：实现标准异常构造函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ImplementStandardExceptionConstructors|
|CheckId|CA1032|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型 <xref:System.Exception?displayProperty=fullName> 扩展，不声明所有必需的构造函数。

## <a name="rule-description"></a>规则说明
 异常类型必须实现以下构造函数：

- public NewException （）

- public NewException （字符串）

- public NewException （string，Exception）

- protected 或 private NewException （SerializationInfo，StreamingContext）

  如果不能提供完整的构造函数集，要正确处理异常将变得比较困难。 例如，具有签名 `NewException(string, Exception)` 的构造函数用于创建由其他异常导致的异常。 如果不使用此构造函数，则不能创建和引发包含内部（嵌套）异常的自定义异常的实例，在这种情况下，托管代码应执行此操作。 前三个异常构造函数按约定公开。 第四个构造函数在非密封类中受保护，在密封类中是私有的。 有关详细信息，请参阅[CA2229：实现序列化构造函数](../code-quality/ca2229-implement-serialization-constructors.md)

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将缺少的构造函数添加到异常，并确保它们具有正确的可访问性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果冲突是通过对公共构造函数使用不同访问级别引起的，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例包含违反此规则的异常类型以及正确实现的异常类型。

 [!code-csharp[FxCop.Design.ExceptionMultipleCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionMultipleCtors/cs/FxCop.Design.ExceptionMultipleCtors.cs#1)]
