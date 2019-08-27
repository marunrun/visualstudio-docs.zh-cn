---
title: CA1806:不要忽略方法结果 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 117e26fca367c8cf00604bebe01a00f4df58a0ee
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63437401"
---
# <a name="ca1806-do-not-ignore-method-results"></a>CA1806:不要忽略方法结果
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||  
|-|-|  
|TypeName|DoNotIgnoreMethodResults|  
|CheckId|CA1806|  
|类别|Microsoft.Usage|  
|是否重大更改|非重大更改|  
  
## <a name="cause"></a>原因  
 有多种原因引起此警告：  
  
- 一个新的对象将创建但从未使用过。  
  
- 创建并返回新字符串的方法称为，从未使用过的新字符串。  
  
- 永远不会使用返回的 HRESULT 或错误代码的 COM 或 P/Invoke 方法。 规则说明  
  
  不必要的对象的创建和未使用的对象的关联的垃圾回收会降低性能。  
  
  字符串是固定不变，并等 String.ToUpper 方法返回的字符串，而非修改实例时调用的方法中字符串的新实例。  
  
  忽略 HRESULT 或错误代码可能会导致错误条件中出现意外行为或资源不足的情况。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 如果一个方法创建从未使用过的 B 对象的新实例，将实例作为参数传递给另一种方法，或将此实例赋给变量。 如果对象创建不必要，请删除它。-或-  
  
 如果方法 A 调用 B，方法，但不使用新方法 B 返回的字符串实例。 将该实例作为参数传递给另一种方法，将实例分配给一个变量。 或者，如果不需要移除此调用。  
  
 或  
  
 如果方法 A 调用 B，方法，但不会使用相应的 HRESULT 或错误代码，该方法返回。 使用中的条件语句的结果、 将结果分配给一个变量，或将其作为参数传递给另一种方法。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 除非创建对象的操作有特定的用途，否则不要禁止显示此规则的警告。  
  
## <a name="example"></a>示例  
 下面的示例演示将忽略调用 String.Trim 结果的类。  
  
<!-- TODO: review snippet reference  [!CODE [FxCop.Usage.DoNotIgnoreMethodResults#1](FxCop.Usage.DoNotIgnoreMethodResults#1)]  -->  
  
## <a name="example"></a>示例  
 下面的示例通过将 String.Trim 结果赋回给调用它的变量中修复了上一冲突。  
  
<!-- TODO: review snippet reference  [!CODE [FxCop.Usage.DoNotIgnoreMethodResults2#1](FxCop.Usage.DoNotIgnoreMethodResults2#1)]  -->  
  
## <a name="example"></a>示例  
 下面的示例演示不使用它创建的对象的方法。  
  
> [!NOTE]
> 无法在 Visual Basic 中重现此冲突。  
  
 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/cpp/FxCop.Usage.DoNotIgnoreMethodResults3.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/cs/FxCop.Usage.DoNotIgnoreMethodResults3.cs#1)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults3#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults3/vb/FxCop.Usage.DoNotIgnoreMethodResults3.vb#1)]  
  
## <a name="example"></a>示例  
 下面的示例通过删除不必要创建对象修复了上一冲突。  
  
 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/cpp/FxCop.Usage.DoNotIgnoreMethodResults4.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/cs/FxCop.Usage.DoNotIgnoreMethodResults4.cs#1)]
 [!code-vb[FxCop.Usage.DoNotIgnoreMethodResults4#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults4/vb/FxCop.Usage.DoNotIgnoreMethodResults4.vb#1)]  
  
## <a name="example"></a>示例  
 下面的示例演示将忽略本机方法 GetShortPathName 返回的错误代码的方法。  
  
 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults5/cpp/FxCop.Usage.DoNotIgnoreMethodResults5.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults5#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults5/cs/FxCop.Usage.DoNotIgnoreMethodResults5.cs#1)]  
  
## <a name="example"></a>示例  
 下面的示例通过检查错误代码和调用失败时引发异常来解决问题的上一冲突。  
  
 [!code-cpp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults6/cpp/FxCop.Usage.DoNotIgnoreMethodResults6.cpp#1)]
 [!code-csharp[FxCop.Usage.DoNotIgnoreMethodResults6#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DoNotIgnoreMethodResults6/cs/FxCop.Usage.DoNotIgnoreMethodResults6.cs#1)]