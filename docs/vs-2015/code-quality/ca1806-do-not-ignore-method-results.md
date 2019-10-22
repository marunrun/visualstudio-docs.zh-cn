---
title: CA1806：不要忽略方法结果 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1806
- DoNotIgnoreMethodResults
helpviewer_keywords:
- CA1806
- DoNotIgnoreMethodResults
ms.assetid: fd805687-0817-481e-804e-b62cfb3b1076
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f68ab71d9ce4fab1b0612f15d866c58e302a317e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671510"
---
# <a name="ca1806-do-not-ignore-method-results"></a>CA1806：不要忽略方法结果
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotIgnoreMethodResults|
|CheckId|CA1806|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 此警告有几个可能的原因：

- 创建了一个新的对象，但从未使用过。

- 将调用一个创建并返回一个新字符串的方法，并且永远不会使用新的字符串。

- COM 或 P/Invoke 方法，它返回从未使用过的 HRESULT 或错误代码。 规则说明

  不必要的对象创建和未使用对象的关联垃圾回收会降低性能。

  字符串是不可变的，ToUpper 返回字符串的新实例，而不是在调用方法中修改字符串的实例。

  忽略 HRESULT 或错误代码可能导致在错误情况下或资源不足的情况下出现意外的行为。

## <a name="how-to-fix-violations"></a>如何解决冲突
 如果方法 A 创建从未使用的 B 对象的新实例，则将该实例作为参数传递给另一个方法，或将该实例分配给一个变量。 如果不需要创建对象，则将其删除。-或-

 如果方法 A 调用方法 B，但不使用方法 B 返回的新字符串实例，则为。 将该实例作为参数传递给其他方法，并将该实例分配给一个变量。 如果不需要，则删除该调用。

 或

 如果方法 A 调用方法 B，但不使用该方法返回的 HRESULT 或错误代码，则为。 在条件语句中使用结果，将结果赋给变量，或将其作为参数传递给其他方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则发出的警告，除非创建对象的行为可用于实现某些目的。

## <a name="example"></a>示例
 下面的示例演示一个类，该类忽略调用字符串的结果。

<!-- TODO: review snippet reference  [!CODE [FxCop.Usage.DoNotIgnoreMethodResults#1](FxCop.Usage.DoNotIgnoreMethodResults#1)]  -->

## <a name="example"></a>示例
 下面的示例通过将字符串的结果赋给其在其上调用的变量来修复前面的冲突。

<!-- TODO: review snippet reference  [!CODE [FxCop.Usage.DoNotIgnoreMethodResults2#1](FxCop.Usage.DoNotIgnoreMethodResults2#1)]  -->

## <a name="example"></a>示例
 下面的示例演示不使用它创建的对象的方法。

> [!NOTE]
> 在 Visual Basic 中无法重现此冲突。

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/cpp/FxCop.Usage.DoNotIgnoreMethodResults3.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/cs/FxCop.Usage.DoNotIgnoreMethodResults3.cs#1)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/vb/FxCop.Usage.DoNotIgnoreMethodResults3.vb#1)]

## <a name="example"></a>示例
 下面的示例通过删除不必要的对象创建来修复以前的冲突。

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/cpp/FxCop.Usage.DoNotIgnoreMethodResults4.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/cs/FxCop.Usage.DoNotIgnoreMethodResults4.cs#1)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/vb/FxCop.Usage.DoNotIgnoreMethodResults4.vb#1)]

## <a name="example"></a>示例
 下面的示例演示了一个方法，该方法忽略本机方法 GetShortPathName 返回的错误代码。

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults5/cpp/FxCop.Usage.DoNotIgnoreMethodResults5.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults5/cs/FxCop.Usage.DoNotIgnoreMethodResults5.cs#1)]

## <a name="example"></a>示例
 下面的示例通过检查错误代码，并在调用失败时引发异常来修复以前的冲突。

 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults6/cpp/FxCop.Usage.DoNotIgnoreMethodResults6.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults6/cs/FxCop.Usage.DoNotIgnoreMethodResults6.cs#1)]