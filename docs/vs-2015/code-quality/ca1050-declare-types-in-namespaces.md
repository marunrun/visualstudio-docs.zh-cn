---
title: CA1050：声明命名空间中的类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1050
- DeclareTypesInNamespaces
helpviewer_keywords:
- DeclareTypesInNamespaces
- CA1050
ms.assetid: 1002748d-ac8d-404f-85dd-7a12d1ad3e05
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a0a4dcc53fac7dc9b7e189686a3b32e2fb4fd030
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539589"
---
# <a name="ca1050-declare-types-in-namespaces"></a>CA1050:在命名空间中声明类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DeclareTypesInNamespaces|
|CheckId|CA1050|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 在命名命名空间的范围外定义公共或受保护类型。

## <a name="rule-description"></a>规则描述
 类型是在命名空间中声明的，以防止名称冲突，并作为在对象层次结构中组织相关类型的一种方法。 位于任何命名命名空间之外的类型位于无法在代码中引用的全局命名空间中。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将类型置于命名空间中。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 尽管你不必禁止显示此规则发出的警告，但当程序集绝不会与其他程序集一起使用时，可以安全地执行此操作。

## <a name="example"></a>示例
 下面的示例演示了一个类型不正确地在命名空间外声明的库，以及一个在命名空间中声明了相同名称的类型。

 [!code-csharp[FxCop.Design.TypesLiveInNamespaces#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/cs/FxCop.Design.TypesLiveInNamespaces.cs#1)]
 [!code-vb[FxCop.Design.TypesLiveInNamespaces#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/vb/FxCop.Design.TypesLiveInNamespaces.vb#1)]

## <a name="example"></a>示例
 以下应用程序使用之前定义的库。 请注意，当名称未 `Test` 由命名空间限定时，将创建在命名空间外部声明的类型。 另请注意，若要访问 `Test` 中的类型 `Goodspace` ，需要命名空间名称。

 [!code-csharp[FxCop.Design.TestTypesLive#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/cs/FxCop.Design.TestTypesLive.cs#1)]
 [!code-vb[FxCop.Design.TestTypesLive#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/vb/FxCop.Design.TestTypesLive.vb#1)]
