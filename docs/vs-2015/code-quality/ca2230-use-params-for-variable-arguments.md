---
title: CA2230:自变量使用 params |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseParamsForVariableArguments
- CA2230
helpviewer_keywords:
- CA2230
- UseParamsForVariableArguments
ms.assetid: bf98b733-4855-4110-9f16-eba5a9e79421
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8b833f520c574c32f90ff1ec5e20a9671184b78a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65685104"
---
# <a name="ca2230-use-params-for-variable-arguments"></a>CA2230:对可变数量的参数使用 params
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseParamsForVariableArguments|
|CheckId|CA2230|
|类别|Microsoft.Usage|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护类型包含公共或受保护的方法使用`VarArgs`调用约定。

## <a name="rule-description"></a>规则说明
 `VarArgs`调用约定用于采用可变数量参数的某些方法定义。 方法使用`VarArgs`调用约定不是公共语言规范 (CLS) 符合和不能访问各种编程语言。

 在 C# 中，`VarArgs`方法的参数列表结尾时，调用约定使用`__arglist`关键字。 Visual Basic 不支援`VarArgs`调用约定和视觉对象C++使用椭圆的非托管代码中仅允许其使用`...`表示法。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要在 C# 中修复该规则的冲突，请使用[params](https://msdn.microsoft.com/library/1690815e-b52b-4967-8380-5780aff08012)关键字而不是`__arglist`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示两种方法，一个与该规则冲突，一个满足该规则。

 [!code-csharp[FxCop.Usage.UseParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.UseParams/cs/FxCop.Usage.UseParams.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Reflection.CallingConventions?displayProperty=fullName> [语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
