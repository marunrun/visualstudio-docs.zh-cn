---
title: CA1040:避免使用空接口 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: bc785967b4e27599b4a04aeb7740b53b5076938d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62559735"
---
# <a name="ca1040-avoid-empty-interfaces"></a>CA1040:避免使用空接口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidEmptyInterfaces|
|CheckId|CA1040|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 接口不声明任何成员，也不实现两个或多个其他接口。

## <a name="rule-description"></a>规则说明
 接口定义提供某个行为或使用协定的成员。 接口所描述的功能可以被任何类型采用，而不管该类型出现在继承层次结构中的哪个位置。 类型通过实现接口的成员来实现接口。 空接口不定义任何成员。 因此，它不定义可以实现的协定。

 如果您的设计包括空类型的接口需要实现，可能使用接口作为一个标记或可以识别的一组类型。 如果此标识出现在运行时，若要实现此目的的正确方法是使用自定义属性。 使用存在或缺少属性或该属性的属性以确定目标类型。 如果该标识必须出现在编译时，它是可接受使用空接口。

## <a name="how-to-fix-violations"></a>如何解决冲突
 移除该接口或向其添加成员。 如果空接口用于标签的一组类型，替换为该接口的自定义属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，该接口用于在编译时标识一组类型时。

## <a name="example"></a>示例
 下面的示例显示了一个空接口。

 [!code-cpp[FxCop.Design.InterfacesNotEmpty#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cpp/FxCop.Design.InterfacesNotEmpty.cpp#1)]
 [!code-csharp[FxCop.Design.InterfacesNotEmpty#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cs/FxCop.Design.InterfacesNotEmpty.cs#1)]
 [!code-vb[FxCop.Design.InterfacesNotEmpty#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/vb/FxCop.Design.InterfacesNotEmpty.vb#1)]
