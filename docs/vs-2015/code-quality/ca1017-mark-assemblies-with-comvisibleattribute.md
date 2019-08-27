---
title: CA1017:用 ComVisibleAttribute 标记程序集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1017
- MarkAssembliesWithComVisible
helpviewer_keywords:
- MarkAssembliesWithComVisible
- CA1017
ms.assetid: 4842cb49-8dd8-4e5d-a2d6-ceeaf6c6cf8e
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1ccd9de3f93ff08952c3a8d53423cb4f6d6261cb
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704211"
---
# <a name="ca1017-mark-assemblies-with-comvisibleattribute"></a>CA1017:用 ComVisibleAttribute 标记程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkAssembliesWithComVisible|
|CheckId|CA1017|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 程序集不具有<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>特性应用于它。

## <a name="rule-description"></a>规则说明
 <xref:System.Runtime.InteropServices.ComVisibleAttribute>属性确定 COM 客户端如何访问托管的代码。 合理的设计指出程序集将显式指示 COM 可见性。 可设置整个程序集 COM 可见性，且然后重写各个类型和类型成员。 如果该属性不存在，该程序集的内容会在向 COM 客户端可见。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请将属性添加到该程序集。 如果不想要向 COM 客户端可见的程序集，应用该特性并将其值设置为`false`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 如果你想要显示的程序集，应用该特性并将其值设置为`true`。

## <a name="example"></a>示例
 下面的示例演示具有的程序集<xref:System.Runtime.InteropServices.ComVisibleAttribute>应用以防止它看不到 COM 客户端属性。

 [!code-cpp[FxCop.Design.AssembliesCom#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/cpp/FxCop.Design.AssembliesCom.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesCom#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/cs/FxCop.Design.AssembliesCom.cs#1)]
 [!code-vb[FxCop.Design.AssembliesCom#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCom/vb/FxCop.Design.AssembliesCom.vb#1)]

## <a name="see-also"></a>请参阅
 [与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)[为互操作限定.NET 类型](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)
