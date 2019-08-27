---
title: CA1715:标识符应具有正确的前缀 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1715
- IdentifiersShouldHaveCorrectPrefix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectPrefix
- CA1715
ms.assetid: cf45f8df-6855-4cb6-a4e2-7cfed714cf2f
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 37c8193a166849f1361a66c640b1a414d3900fca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189129"
---
# <a name="ca1715-identifiers-should-have-correct-prefix"></a>CA1715:标识符应具有正确的前缀
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 的最新文档，请参阅[CA1715:标识符应具有正确的前缀](https://docs.microsoft.com/visualstudio/code-quality/ca1715-identifiers-should-have-correct-prefix)。  
  
|||  
|-|-|  
|TypeName|IdentifiersShouldHaveCorrectPrefix|  
|CheckId|CA1715|  
|类别|Microsoft.Naming|  
|是否重大更改|是-如果在接口上引发。<br /><br /> 无间断-引发泛型类型参数上时。|  
  
## <a name="cause"></a>原因  
 外部可见的接口的名称不以大写 I 开头。  
  
 或  
  
 上的外部可见类型或方法的泛型类型参数的名称不会启动包含大写 ' T '。  
  
## <a name="rule-description"></a>规则说明  
 某些编程元素的名称按照约定，由特定前缀开头。  
  
 接口名称应以大写字母 I 后跟另一个大写字母开头。 此规则报告接口名称，例如 MyInterface 和 IsolatedInterface 的冲突。  
  
 泛型类型参数名称应以开头大写 ' T 和 （可选） 可以跟随另一个大写字母。 此规则报告泛型类型参数名称，例如 V 和 Type 的冲突。  
  
 命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。  
  
## <a name="how-to-fix-violations"></a>如何解决冲突  
 重命名标识符，以便它正确的前缀。  
  
## <a name="when-to-suppress-warnings"></a>何时禁止显示警告  
 不禁止显示此规则发出的警告。  
  
## <a name="example"></a>示例  
 **下面的示例显示了不正确命名的接口。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix.vb#1)]  
  
## <a name="example"></a>示例  
 **下面的示例通过带 'I' 前缀接口修复了上一冲突。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2.vb#1)]  
  
## <a name="example"></a>示例  
 **下面的示例演示一个未正确命名的泛型类型参数。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3.vb#1)]  
  
## <a name="example"></a>示例  
 **下面的示例通过前缀与 T 的泛型类型参数修复了上一冲突。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4.vb#1)]  
  
## <a name="related-rules"></a>相关的规则  
 [CA1722:标识符应采用正确的前缀](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)
