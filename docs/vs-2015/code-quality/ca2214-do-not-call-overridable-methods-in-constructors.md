---
title: CA2214：不要在构造函数中调用可重写的方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotCallOverridableMethodsInConstructors
- CA2214
helpviewer_keywords:
- CA2214
- DoNotCallOverridableMethodsInConstructors
ms.assetid: 335b57ca-a6e8-41b4-a20e-57ee172c97c3
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 78702298bab484a95bb8108150415ec0b31ede7d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662909"
---
# <a name="ca2214-do-not-call-overridable-methods-in-constructors"></a>CA2214：不要在构造函数中调用可重写的方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotCallOverridableMethodsInConstructors|
|CheckId|CA2214|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 未密封类型的构造函数将调用在其类中定义的虚方法。

## <a name="rule-description"></a>规则说明
 调用虚方法时，在运行时之前不会选择执行方法的实际类型。 当构造函数调用虚方法时，调用方法的实例的构造函数可能未执行。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请不要从该类型的构造函数内调用类型的虚拟方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 应对构造函数进行重新设计，以消除对虚拟方法的调用。

## <a name="example"></a>示例
 下面的示例演示违反此规则的效果。 测试应用程序创建 `DerivedType` 的实例，这将导致其基类（`BadlyConstructedType`）构造函数执行。 `BadlyConstructedType` 的构造函数错误地调用了虚方法 `DoSomething`。 如输出所示，`DerivedType.DoSomething()` 执行，在 `DerivedType` 的构造函数执行之前执行此操作。

 [!code-csharp[FxCop.Usage.CtorVirtual#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CtorVirtual/cs/FxCop.Usage.CtorVirtual.cs#1)]
 [!code-vb[FxCop.Usage.CtorVirtual#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CtorVirtual/vb/FxCop.Usage.CtorVirtual.vb#1)]

 本示例生成以下输出。

 **调用基 .ctor。** 
**派生的 DoSomething 称为 "已初始化"？没有** **调用派生的 ctor 的 
。**
