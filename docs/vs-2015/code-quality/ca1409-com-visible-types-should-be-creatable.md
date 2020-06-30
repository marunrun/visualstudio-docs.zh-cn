---
title: CA1409： Com 可见类型应该是可创建的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
helpviewer_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
ms.assetid: 9f59569b-de15-4a38-b7cb-cff152972243
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 180a8d6bbc7f035fa0ae2eeafaa4e2c884cddc8d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547324"
---
# <a name="ca1409-com-visible-types-should-be-creatable"></a>CA1409:COM 可见类型应该是可创建的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ComVisibleTypesShouldBeCreatable|
|CheckId|CA1409|
|Category|Microsoft. 互操作性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 特别标记为对组件对象模型（COM）可见的引用类型包含公共参数化构造函数，但不包含公共默认（无参数）构造函数。

## <a name="rule-description"></a>规则描述
 COM 客户端不能创建没有公共默认构造函数的类型。 但是，COM 客户端仍然可以访问该类型，如果另一种方法可用于创建类型并将其传递给客户端（例如，通过方法调用的返回值）。

 规则将忽略派生自的类型 <xref:System.Delegate?displayProperty=fullName> 。

 默认情况下，以下是对 COM 可见的：程序集、公共类型、公共类型中的公共实例成员以及公共值类型的所有成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请添加一个公共的默认构造函数或 <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> 从该类型中删除。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果提供了其他方法来创建对象并将其传递给 COM 客户端，则可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
 [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>另请参阅
 为[与非托管代码互](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)[操作的互操作提供 .Net 类型的资格](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)
