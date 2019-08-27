---
title: CA1050:在命名空间中声明类型 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f13684df70db7026e874bc8edb6282faca2cf98d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200545"
---
# <a name="ca1050-declare-types-in-namespaces"></a>CA1050:在命名空间中声明类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DeclareTypesInNamespaces|
|CheckId|CA1050|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 命名的命名空间范围内定义了一个公共或受保护的类型。

## <a name="rule-description"></a>规则说明
 在命名空间，以防止名称冲突，并作为一种方法来组织对象层次结构中的相关的类型声明类型。 任何命名的命名空间之外的类型是不能在代码中引用全局命名空间中。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，将类型置于一个命名空间中。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 虽然永远不会需要禁止显示此规则的警告，是安全地执行此操作时将程序集将永远不与其他程序集一起使用。

## <a name="example"></a>示例
 下面的示例演示具有类型外部命名空间中，未正确声明一个库和具有相同名称的命名空间中声明的类型。

 [!code-csharp[FxCop.Design.TypesLiveInNamespaces#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/cs/FxCop.Design.TypesLiveInNamespaces.cs#1)]
 [!code-vb[FxCop.Design.TypesLiveInNamespaces#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/vb/FxCop.Design.TypesLiveInNamespaces.vb#1)]

## <a name="example"></a>示例
 下面的应用程序使用以前已定义的库。 请注意，外部命名空间声明的类型时，将创建名称`Test`未由命名空间限定。 另请注意，若要访问`Test`中键入`Goodspace`，命名空间名称是必需的。

 [!code-csharp[FxCop.Design.TestTypesLive#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/cs/FxCop.Design.TestTypesLive.cs#1)]
 [!code-vb[FxCop.Design.TestTypesLive#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/vb/FxCop.Design.TestTypesLive.vb#1)]
