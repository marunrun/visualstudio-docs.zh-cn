---
title: CA1001:可释放的字段应该是可释放类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
helpviewer_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
ms.assetid: c85c126c-2b16-4505-940a-b5ddf873fb22
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 98be3bafb582e4d48560108625be911e53acf664
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62562310"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001:具有可释放字段的类型应该是可释放的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||  
|-|-|  
|TypeName|TypesThatOwnDisposableFieldsShouldBeDisposable|  
|CheckId|CA1001|  
|类别|Microsoft.Design|  
|是否重大更改|无间断-如果类型不是程序集外部可见。<br /><br /> 是-如果该类型是在程序集外可见。|  
  
## <a name="cause"></a>原因  
 一个类声明并实现是实例字段<xref:System.IDisposable?displayProperty=fullName>类型和类不实现<xref:System.IDisposable>。  
  
## <a name="rule-description"></a>规则说明  
 一个类实现<xref:System.IDisposable>接口来释放它拥有的非托管资源。 是的实例字段<xref:System.IDisposable>类型指示该字段拥有非托管的资源。 声明的类<xref:System.IDisposable>字段间接拥有非托管的资源，应实现<xref:System.IDisposable>接口。 如果类不直接拥有任何非托管的资源，它不应实现终结器。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 若要修复此规则的冲突，请实现<xref:System.IDisposable>来回<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>方法调用<xref:System.IDisposable.Dispose%2A>字段的方法。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 不禁止显示此规则发出的警告。  
  
## <a name="example"></a>示例  
 下面的示例演示与规则冲突的类和类，用以通过实现来满足该规则<xref:System.IDisposable>。 类不实现终结器，因为类直接拥有任何非托管的资源。  
  
 [!code-csharp[FxCop.Design.DisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/cs/FxCop.Design.DisposableFields.cs#1)]
 [!code-vb[FxCop.Design.DisposableFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/vb/FxCop.Design.DisposableFields.vb#1)]  
  
## <a name="related-rules"></a>相关的规则  
 [CA2213：应释放可释放的字段](../code-quality/ca2213-disposable-fields-should-be-disposed.md)  
  
 [CA2216:可释放类型应声明终结器](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)  
  
 [CA2215:方法应调用基类 dispose](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)  
  
 [CA1049:拥有本机资源的类型应是可释放的](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)
