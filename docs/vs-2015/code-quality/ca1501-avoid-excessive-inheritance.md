---
title: CA1501：避免过多的继承 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1501
- AvoidExcessiveInheritance
helpviewer_keywords:
- AvoidExcessiveInheritance
- CA1501
ms.assetid: 9e934746-1a4d-492a-91e4-085201abafa4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: cf797ad67b7df2eb1f3ba1246e965ed6ebbd586d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547857"
---
# <a name="ca1501-avoid-excessive-inheritance"></a>CA1501:避免过度继承
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|AvoidExcessiveInheritance|
|CheckId|CA1501|
|类别|Microsoft 可维护性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型在继承层次结构中的深度超过四级。

## <a name="rule-description"></a>规则描述
 深度嵌套的类型层次结构可能很难遵循、理解和维护。 此规则将分析限制为同一个模块中的层次结构。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请从继承层次结构中不太深层的基类型派生类型，或消除某些中间基类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 可以安全地禁止显示此规则发出的警告。 但代码可能更难以维护。 请注意，根据基类型的可见性，解决此规则的冲突可能会造成重大更改。 例如，删除公共基类型是一项重大更改。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。

 [!code-csharp[FxCop.Maintainability.ExcessiveInheritance#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.ExcessiveInheritance/cs/FxCop.Maintainability.ExcessiveInheritance.cs#1)]
 [!code-vb[FxCop.Maintainability.ExcessiveInheritance#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.ExcessiveInheritance/vb/FxCop.Maintainability.ExcessiveInheritance.vb#1)]
