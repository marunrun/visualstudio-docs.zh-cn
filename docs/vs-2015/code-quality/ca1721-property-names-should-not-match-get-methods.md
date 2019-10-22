---
title: CA1721：属性名称不应与 get 方法匹配 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
helpviewer_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
ms.assetid: 45a0e853-1f06-4688-af1b-cc634409e295
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 366932c83328c6810e0103308db1c73a3e3076cb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671611"
---
# <a name="ca1721-property-names-should-not-match-get-methods"></a>CA1721：属性名不应与 get 方法冲突
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PropertyNamesShouldNotMatchGetMethods|
|CheckId|CA1721|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护成员的名称以 "Get" 开头，否则与公共或受保护的属性的名称匹配。 例如，包含名为 "GetColor" 的方法和名为 "Color" 的属性的类型违反了此规则。

## <a name="rule-description"></a>规则说明
 Get 方法和属性的名称应能够明确区分其函数。

 命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了学习新软件库所需的时间，并使客户对库的开发更加自信，因为有开发托管代码的专业技能。

## <a name="how-to-fix-violations"></a>如何解决冲突
 更改名称，使其与前缀为 "Get" 的方法的名称不匹配。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

> [!NOTE]
> 如果 Get 方法是通过实现既也接口引起的，则可能排除此警告。

## <a name="example"></a>示例
 下面的示例包含违反此规则的方法和属性。

 [!code-csharp[FxCop.Naming.GetMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/cs/FxCop.Naming.GetMethod.cs#1)]
 [!code-vb[FxCop.Naming.GetMethod#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/vb/FxCop.Naming.GetMethod.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1024：在适用处使用属性](../code-quality/ca1024-use-properties-where-appropriate.md)
