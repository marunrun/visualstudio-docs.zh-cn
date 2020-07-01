---
title: CA1026：不应使用默认参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
helpviewer_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
ms.assetid: 09643415-36ef-4d0f-9411-5721e14e2512
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a63d6e788dd1722d0c593469b225a4f1aeb4738d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548432"
---
# <a name="ca1026-default-parameters-should-not-be-used"></a>CA1026:不应使用默认形参
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|Category|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见类型包含使用默认参数的外部可见方法。

## <a name="rule-description"></a>规则描述
 在公共语言规范（CLS）下允许使用默认参数的方法;但是，CLS 允许编译器忽略分配给这些参数的值。 为忽略默认参数值的编译器编写的代码必须为每个默认参数显式提供参数。 若要跨编程语言维护所需的行为，则应使用提供默认参数的方法重载替换使用默认参数的方法。

 编译器在访问托管代码时，将忽略 c + + 的托管扩展的默认参数值。 Visual Basic 编译器支持具有使用[可选](https://msdn.microsoft.com/library/4571ce88-a539-4115-b230-54eb277c6aa7)关键字的默认参数的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将使用默认参数的方法替换为提供默认参数的方法重载。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个使用默认参数的方法，以及提供等效功能的重载方法。

 [!code-vb[FxCop.Design.DefaultParameters#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DefaultParameters/vb/FxCop.Design.DefaultParameters.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1025:用形参数组替换重复的实参](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## <a name="see-also"></a>另请参阅
 [语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
