---
title: 托管代码的 "全球化规则" 规则集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 3c4032ee-0805-4581-8c48-b1827cd6b213
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1630769b5150d9cef7b00e575ac9c555f5bc5be1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667609"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>托管代码的“全球化规则”规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 "Microsoft 全球化规则" 规则集来重点关注可能阻止应用程序中的数据在不同语言、区域设置和区域性中正确显示的问题。 如果你的应用程序已本地化、全球化，则应包含此规则集。

|规则|描述|
|----------|-----------------|
|[CA1300](../code-quality/ca1300-specify-messageboxoptions.md)|指定 MessageBoxOptions|
|[CA1301](../code-quality/ca1301-avoid-duplicate-accelerators.md)|避免快捷键重复|
|[CA1302](../code-quality/ca1302-do-not-hardcode-locale-specific-strings.md)|请不要对区域设置特定的字符串进行硬编码|
|[CA1303](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|请不要将文本作为本地化参数传递|
|[CA1304](../code-quality/ca1304-specify-cultureinfo.md)|指定 CultureInfo|
|[CA1305](../code-quality/ca1305-specify-iformatprovider.md)|指定 IFormatProvider|
|[CA1306](../code-quality/ca1306-set-locale-for-data-types.md)|设置数据类型的区域设置|
|[CA1307](../code-quality/ca1307-specify-stringcomparison.md)|指定 StringComparison|
|[CA1308](../code-quality/ca1308-normalize-strings-to-uppercase.md)|将字符串规范化为大写|
|[CA1309](../code-quality/ca1309-use-ordinal-stringcomparison.md)|使用按顺序的 StringComparison|
|[CA2101](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|指定对 P/Invoke 字符串参数进行封送处理|
