---
title: CA1026:不应使用默认参数 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 7c20bfce7dd7fe3b2e116b982408afa813ebab25
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704186"
---
# <a name="ca1026-default-parameters-should-not-be-used"></a>CA1026:不应使用默认形参
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见类型包含外部可见方法使用的默认参数。

## <a name="rule-description"></a>规则说明
 使用默认参数的方法允许在公共语言规范 (CLS);但是，CLS 允许编译器忽略分配给这些参数的值。 忽略默认参数值的编译器编写的代码必须显式提供每个默认参数的参数。 若要维护跨编程语言所需的行为，使用默认参数的方法应替换提供的默认参数的方法重载。

 编译器忽略托管扩展插件的默认参数值C++它访问托管的代码时。 Visual Basic 编译器支持具有使用的默认参数的方法[可选](https://msdn.microsoft.com/library/4571ce88-a539-4115-b230-54eb277c6aa7)关键字。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请替换默认参数使用提供的默认参数的方法重载的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示使用默认参数的方法并提供等效功能的重载的方法。

 [!code-vb[FxCop.Design.DefaultParameters#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DefaultParameters/vb/FxCop.Design.DefaultParameters.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1025:用形参数组替换重复的实参](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## <a name="see-also"></a>请参阅
 [语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
