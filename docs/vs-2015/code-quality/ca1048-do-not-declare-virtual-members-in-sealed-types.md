---
title: CA1048：不要在密封类型中声明虚拟成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareVirtualMembersInSealedTypes
- CA1048
helpviewer_keywords:
- DoNotDeclareVirtualMembersInSealedTypes
- CA1048
ms.assetid: 5dcf4a30-6f98-48a8-b8cc-7b89ea757262
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9f843efe0aa17b6e87fdb047e1f98a3715ae11af
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603316"
---
# <a name="ca1048-do-not-declare-virtual-members-in-sealed-types"></a>CA1048：不要在密封类型中声明虚拟成员
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDeclareVirtualMembersInSealedTypes|
|CheckId|CA1048|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共类型是密封的并声明一个方法，该方法既是 `virtual` 的（`Overridable` 在 Visual Basic 中），也不是最终的。 此规则不报告委托类型的冲突，必须遵循此模式。

## <a name="rule-description"></a>规则说明
 类型将方法声明为虚方法，使继承类型可以重写虚方法的实现。 按照定义，不能从密封类型继承，使虚方法在密封类型上无意义。

 Visual Basic .NET 和C#编译器不允许类型违反此规则。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将该方法设置为非虚拟方法，或使该类型可继承。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 使类型保持当前状态可能会导致维护问题，而且不会带来任何好处。

## <a name="example"></a>示例
 下面的示例演示违反此规则的类型。

 [!code-cpp[FxCop.Design.SealedVirtual#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.SealedVirtual/cpp/FxCop.Design.SealedVirtual.cpp#1)]
