---
title: CA1801:检查未使用的参数 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0efbec121e08d026145d8762b574847fbd4a2b88
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143127"
---
# <a name="ca1801-review-unused-parameters"></a>CA1801:检查未使用的参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[CA1801:检查未使用的参数](https://docs.microsoft.com/visualstudio/code-quality/ca1801-review-unused-parameters)。  
  
|||  
|-|-|  
|TypeName|ReviewUnusedParameters|  
|CheckId|CA1801|  
|类别|Microsoft.Usage|  
|是否重大更改|无间断-如果该成员不可见程序集外部的而不考虑更改进行。<br /><br /> 无间断-如果您更改要使用其主体中的参数的成员。<br /><br /> 是-如果删除参数，它是程序集外部可见。|  
  
## <a name="cause"></a>原因  
 方法签名包含一个没有在方法体中使用的参数。 此规则不检查以下方法：  
  
- 由委托所引用的方法。  
  
- 用作事件处理程序方法。  
  
- 方法声明为具有`abstract`(`MustOverride`在 Visual Basic 中) 修饰符。  
  
- 方法声明为具有`virtual`(`Overridable`在 Visual Basic 中) 修饰符。  
  
- 方法声明为具有`override`(`Overrides`在 Visual Basic 中) 修饰符。  
  
- 方法声明为具有`extern`(`Declare`在 Visual Basic 中的语句) 修饰符。  
  
## <a name="rule-description"></a>规则说明  
 查看不用于方法体中请确保没有正确性存在应该对其进行访问的非虚拟方法中的参数。 未使用的参数会产生维护和性能成本。  
  
 有时该规则的冲突可以指向该方法中实现错误。 例如，参数应该具有已使用的方法体中。 如果该参数必须存在由于向后兼容性，禁止显示此规则的警告。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 若要修复此规则的冲突，请删除未使用的参数 （重大更改） 或者 （非重大更改） 的方法体中使用的参数。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 它可以安全地禁止显示以前发布的代码的修复程序将为其在一项重大更改此规则的警告。  
  
## <a name="example"></a>示例  
 下面的示例演示两种方法。 一种方法与该规则冲突和另一种方法满足该规则。  
  
 [!code-csharp[FxCop.Usage.ReviewUnusedParameters#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ReviewUnusedParameters/cs/FxCop.Usage.ReviewUnusedPerameters.cs#1)]  
  
## <a name="related-rules"></a>相关的规则  
 [CA1811:避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)  
  
 [CA1812:避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)  
  
 [CA1804:删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)
