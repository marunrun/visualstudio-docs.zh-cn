---
title: CA1023:索引器不应是多维的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IndexersShouldNotBeMultidimensional
- CA1023
helpviewer_keywords:
- CA1023
- IndexersShouldNotBeMultidimensional
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 08a45219eb2fceeaa9c58a140990ea577c941ff7
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923041"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023:索引器不应是多维的

|||
|-|-|
|TypeName|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
公共或受保护类型包含一个使用多个索引的公共或受保护索引器。

## <a name="rule-description"></a>规则说明
索引器 (即索引属性) 应使用单个索引。 多维索引器可能会显著降低库的可用性。 如果设计需要多个索引, 请重新考虑该类型是否表示逻辑数据存储区。 否则, 请使用方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将设计更改为使用单独的整数或字符串索引, 或使用方法而不是索引器。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
仅在仔细考虑非标准索引器的需求之后, 禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示一个类型, `DayOfWeek03`该类型具有与规则冲突的多维索引器。 索引器可被视为一种类型的转换, 因此更适合作为方法公开。 此类型在中`RedesignedDayOfWeek03`进行了重新设计, 以满足规则。

[!code-vb[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/VisualBasic/ca1023-indexers-should-not-be-multidimensional_1.vb)]
[!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CPP/ca1023-indexers-should-not-be-multidimensional_1.cpp)]
[!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CSharp/ca1023-indexers-should-not-be-multidimensional_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1043将整型或字符串参数用于索引器](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

[CA1024使用适当的属性](../code-quality/ca1024-use-properties-where-appropriate.md)