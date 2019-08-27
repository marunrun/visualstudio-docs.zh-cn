---
title: CA1047:不要声明在密封类型中的受保护的成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareProtectedMembersInSealedTypes
- CA1047
helpviewer_keywords:
- CA1047
- DoNotDeclareProtectedMembersInSealedTypes
ms.assetid: 829033b5-a9d8-4f26-a719-45494c9dd035
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6d949a756dfe3ff22ba43d172078d35bfe706e14
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62535861"
---
# <a name="ca1047-do-not-declare-protected-members-in-sealed-types"></a>CA1047:不要在密封类型中声明受保护的成员
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDeclareProtectedMembersInSealedTypes|
|CheckId|CA1047|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 公共类型是`sealed`(`NotInheritable`在 Visual basic 中) 和声明受保护的成员或受保护的嵌套的类型。 此规则不会报告的冲突<xref:System.Object.Finalize%2A>必须遵循此模式的方法。

## <a name="rule-description"></a>规则说明
 类型声明受保护的成员，使继承类型可以访问或重写该成员。 根据定义，不能继承密封类型，不能调用这意味着，受保护的密封的类型上的方法。

 C# 编译器会发出此错误的警告。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复该规则的冲突，请将该成员的访问级别更改为私有的或创建该类型可继承。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 在其当前状态使类型可能会导致维护问题，它不提供任何权益。

## <a name="example"></a>示例
 下面的示例显示了与此规则冲突的类型。

 [!code-csharp[FxCop.Design.SealedNoProtected#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.SealedNoProtected/cs/FxCop.Design.SealedNoProtected.cs#1)]
 [!code-vb[FxCop.Design.SealedNoProtected#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.SealedNoProtected/vb/FxCop.Design.SealedNoProtected.vb#1)]
