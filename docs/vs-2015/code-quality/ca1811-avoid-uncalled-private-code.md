---
title: CA1811:避免使用未调用的私有代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUncalledPrivateCode
- CA1811
helpviewer_keywords:
- CA1811
- AvoidUncalledPrivateCode
ms.assetid: aadbba74-7821-475f-8980-34d17c0a0a8b
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 373ccaa6552079a8995d61ef09bf6e0845c299d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157970"
---
# <a name="ca1811-avoid-uncalled-private-code"></a>CA1811:避免使用未调用的私有代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidUncalledPrivateCode|
|CheckId|CA1811|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 私有或内部 （程序集级别） 成员在程序集中没有调用方、 由公共语言运行时，不调用和不由委托调用。 此规则不检查下列成员：

- 显式接口成员。

- 静态构造函数。

- 序列化构造函数。

- 使用标记方法<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName>或<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>。

- 是重写的成员。

## <a name="rule-description"></a>规则说明
 此规则会报告误报入口点会发生，如果当前未标识由规则逻辑。 此外，编译器可能将不可调用的代码发出到程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，删除不可调用的代码或添加调用它的代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告。

## <a name="related-rules"></a>相关的规则
 [CA1812:避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801:检查未使用的参数](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804:删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)
