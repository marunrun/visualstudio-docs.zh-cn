---
title: CA1308:将字符串规范化为大写 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1308
- NormalizeStringsToUppercase
helpviewer_keywords:
- NormalizeStringsToUppercase
- CA1308
ms.assetid: 7e9a7457-3f93-4938-ac6f-1389fba8d9cc
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8385839ce7029ef0676225fd443582ba750b618b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200391"
---
# <a name="ca1308-normalize-strings-to-uppercase"></a>CA1308:将字符串规范化为大写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|NormalizeStringsToUppercase|
|CheckId|CA1308|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 操作将规范化为小写的字符串。

## <a name="rule-description"></a>规则说明
 字符串应正常化为大写字母。 字符，当它们转换为小写，不能进行一次往返过程时一小组。 若要进行往返行程意味着若要将字符转换的区域设置到另一个区域设置的方式不同，表示的字符数据，再到准确地检索从已转换的字符的原始字符。

## <a name="how-to-fix-violations"></a>如何解决冲突
 更改操作将字符串转换为小写，以便将字符串转换为改为大写。 例如，将 `String.ToLower(CultureInfo.InvariantCulture)` 更改为 `String.ToUpper(CultureInfo.InvariantCulture)`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它是安全地禁止显示一条警告消息，当您不需要安全决策基于结果 （例如，当在 UI 中显示时）。

## <a name="see-also"></a>请参阅
 [全球化警告](../code-quality/globalization-warnings.md)
