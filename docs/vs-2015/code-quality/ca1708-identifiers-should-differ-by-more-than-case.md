---
title: CA1708：标识符的差别应超过大小写 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldDifferByMoreThanCase
- CA1708
helpviewer_keywords:
- CA1708
- IdentifiersShouldDifferByMoreThanCase
ms.assetid: dac0f01d-dd21-484d-add1-c8cd2bf6969f
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f611cb899a2386c47e1370214a74c2a5da52584f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669204"
---
# <a name="ca1708-identifiers-should-differ-by-more-than-case"></a>CA1708：标识符不应仅以大小写进行区分
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldDifferByMoreThanCase|
|CheckId|CA1708|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 当两个类型、成员、参数或完全限定的命名空间的名称转换为小写时，它们的名称相同。

## <a name="rule-description"></a>规则说明
 不能仅通过大小写区分命名空间、类型、成员和参数的标识符，因为针对公共语言运行时的语言不需要区分大小写。 例如，[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 是一种广泛使用的不区分大小写的语言。

 此规则仅对公共可见成员触发。

## <a name="how-to-fix-violations"></a>如何解决冲突
 选择一个唯一的名称，当与其他标识符进行比较时，该名称不区分大小写。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 库可能无法用于 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 中的所有可用语言。

## <a name="example-of-a-violation"></a>冲突示例
 下面的示例演示违反此规则的情况。

 [!code-csharp[FxCop.Naming.IdentifiersShouldDifferByMoreThanCase#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldDifferByMoreThanCase/cs/FxCop.Naming.IdentifiersShouldDifferByMoreThanCase.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA1709：标识符的大小写应当正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
