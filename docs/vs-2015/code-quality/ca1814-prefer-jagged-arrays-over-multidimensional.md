---
title: CA1814:通过多维首选使用交错的数组 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
helpviewer_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
ms.assetid: b1ccf563-2ec8-42e5-b89c-731a9de1ea1d
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 73b20ef9a93e59f3fae30407deda8d21befc57f5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201705"
---
# <a name="ca1814-prefer-jagged-arrays-over-multidimensional"></a>CA1814:与多维数组相比，首选使用交错数组
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PreferJaggedArraysOverMultidimensional|
|CheckId|CA1814|
|类别|Microsoft.Performance|
|是否重大更改|重大|

## <a name="cause"></a>原因
 成员被声明为多维数组。

## <a name="rule-description"></a>规则说明
 交错数组是元素为数组的数组。 构成元素的数组可以是不同的大小，以减少某些数据集的浪费空间。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改到交错数组多维数组。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 禁止显示此规则的警告，如果多维数组不会浪费空间。

## <a name="example"></a>示例
 下面的示例演示了交错和多维数组的声明。

 [!code-csharp[FxCop.Performance.JaggedArrays#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.JaggedArrays/cs/FxCop.Performance.JaggedArrays.cs#1)]
 [!code-vb[FxCop.Performance.JaggedArrays#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.JaggedArrays/vb/FxCop.Performance.JaggedArrays.vb#1)]
