---
title: CA1801：查看未使用的参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnusedParameters
- CA1801
- ReviewUnusedParameters
helpviewer_keywords:
- CA1801
- ReviewUnusedParameters
ms.assetid: 5d73545c-e153-4b7c-a7b2-be6bf5aca5be
caps.latest.revision: 31
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c87836f99684c7e16c022e3e9f15bf546ba82d62
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547779"
---
# <a name="ca1801-review-unused-parameters"></a>CA1801:检查未使用的参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

有关 Visual Studio 的最新文档，请参阅 [CA1801：检查未使用的参数](/visualstudio/code-quality/ca1801-review-unused-parameters)。

|项|值|
|-|-|
|TypeName|ReviewUnusedParameters|
|CheckId|CA1801|
|类别|Microsoft. 使用情况|
|是否重大更改|无间断-如果该成员在程序集外部不可见，不管你进行了何种更改。<br /><br /> 不换行-如果将成员更改为在其主体中使用参数，则为。<br /><br /> 如果删除参数，则该参数在程序集外可见。|

## <a name="cause"></a>原因
 方法签名包含一个没有在方法体中使用的参数。 此规则不检查以下方法：

- 委托引用的方法。

- 用作事件处理程序的方法。

- 用 `abstract` `MustOverride` Visual Basic) 修饰符中的 (声明的方法。

- 用 `virtual` `Overridable` Visual Basic) 修饰符中的 (声明的方法。

- 用 `override` `Overrides` Visual Basic) 修饰符中的 (声明的方法。

- 用 `extern` `Declare` Visual Basic) 修饰符中的 (语句声明的方法。

## <a name="rule-description"></a>规则描述
 查看未在方法体中使用的非虚方法中的参数，以确保不存在任何访问这些参数的正确性。 未使用的参数会产生维护和性能成本。

 有时，违反此规则可能会指向方法中的实现 bug。 例如，参数应已在方法体中使用。 如果由于向后兼容性而必须存在该参数，请禁止显示此规则的警告。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请删除未使用的参数 (重大更改) 或使用方法体中的参数 (非重大更改) 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 对于以前发布的代码，可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了两种方法。 一个方法违反了规则，另一个方法满足规则。

 [!code-csharp[FxCop.Usage.ReviewUnusedParameters#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ReviewUnusedParameters/cs/FxCop.Usage.ReviewUnusedPerameters.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1811:避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1812:避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1804:移除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)
