---
title: CA1040：避免空接口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1040
- AvoidEmptyInterfaces
helpviewer_keywords:
- AvoidEmptyInterfaces
- CA1040
ms.assetid: 120a741b-5fd1-4836-8453-7857e0cd0380
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 50a36281edb144ddb949899fa24e0b5088080220
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668315"
---
# <a name="ca1040-avoid-empty-interfaces"></a>CA1040：避免使用空接口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidEmptyInterfaces|
|CheckId|CA1040|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 接口不声明任何成员或实现两个或更多个其他接口。

## <a name="rule-description"></a>规则说明
 接口定义提供某个行为或使用协定的成员。 接口所描述的功能可以被任何类型采用，而不管该类型出现在继承层次结构中的哪个位置。 类型通过实现接口的成员来实现接口。 空接口不定义任何成员。 因此，它不定义可以实现的协定。

 如果您的设计包含类型应实现的空接口，则您可能会将接口用作标记或标识一组类型的方式。 如果在运行时进行此标识，则完成此工作的正确方法是使用自定义属性。 使用特性的存在或缺少特性，以标识目标类型。 如果标识必须在编译时出现，则可以使用空接口。

## <a name="how-to-fix-violations"></a>如何解决冲突
 删除接口或向其添加成员。 如果使用空接口来标记一组类型，请将接口替换为自定义特性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 当接口用于在编译时标识一组类型时，可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个空接口。

 [!code-cpp[FxCop.Design.InterfacesNotEmpty#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cpp/FxCop.Design.InterfacesNotEmpty.cpp#1)]
 [!code-csharp[FxCop.Design.InterfacesNotEmpty#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cs/FxCop.Design.InterfacesNotEmpty.cs#1)]
 [!code-vb[FxCop.Design.InterfacesNotEmpty#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/vb/FxCop.Design.InterfacesNotEmpty.vb#1)]
