---
title: CA1308：将字符串规范化为大写 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c068fcda7d03ae91435c040d2110d632668d832a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538731"
---
# <a name="ca1308-normalize-strings-to-uppercase"></a>CA1308:将字符串规范化为大写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|NormalizeStringsToUppercase|
|CheckId|CA1308|
|Category|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 操作将字符串规范化为小写。

## <a name="rule-description"></a>规则描述
 字符串应正常化为大写字母。 将一小部分字符转换为小写字符后，不能进行往返。 若要进行往返，需将字符从一个区域设置转换为另一个表示字符数据的区域设置，然后从转换后的字符中准确检索原始字符。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将字符串转换为小写的操作，以便将字符串转换为大写形式。 例如，将 `String.ToLower(CultureInfo.InvariantCulture)` 更改为 `String.ToUpper(CultureInfo.InvariantCulture)`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果不是基于结果做出安全决策（例如，在用户界面中显示），则可以安全地禁止显示警告消息。

## <a name="see-also"></a>另请参阅
 [全球化警告](../code-quality/globalization-warnings.md)
