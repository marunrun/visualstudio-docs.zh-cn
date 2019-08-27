---
title: CA1719:参数名不应与成员名称 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ParameterNamesShouldNotMatchMemberNames
- CA1719
helpviewer_keywords:
- CA1719
- ParameterNamesShouldNotMatchMemberNames
ms.assetid: c6fea690-1659-4ee7-a1c5-125ad6754525
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: daaa856ccbc5915bcaad937a504ea2600a089c1d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68189100"
---
# <a name="ca1719-parameter-names-should-not-match-member-names"></a>CA1719:参数名不应与成员名冲突
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ParameterNamesShouldNotMatchMemberNames|
|CheckId|CA1719|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见成员的名称匹配，不区分大小写的比较，其参数之一的名称中。

## <a name="rule-description"></a>规则说明
 参数名称应传达参数的含义，成员名称应传达成员的含义。 两者相同的设计非常少见。 使参数与其成员同名会导致不直观的效果，会使库难以使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 选择成员名称不匹配的参数名称。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 对于新开发，没有已知情况下，必须在此禁止显示此规则的警告。 发布库，您可能需要禁止显示此规则的警告。

## <a name="related-rules"></a>相关的规则
 [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707:标识符不应包含下划线](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)
