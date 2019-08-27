---
title: 托管代码的“全球化规则”规则集
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 3c4032ee-0805-4581-8c48-b1827cd6b213
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ffba6b69e1f67b369f3d99c1b54a88448df8a41b
ms.sourcegitcommit: b83fefa8177c5554cbe2c59c4d102cbc534f7cc6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2019
ms.locfileid: "69584979"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>托管代码的“全球化规则”规则集

使用 "Microsoft 全球化规则" 规则集将重点放在可能阻止应用程序中的数据在不同语言、区域设置和区域性中正确显示的问题。 如果你的应用程序已本地化、全球化, 则应包含此规则集。

|规则|描述|
|----------|-----------------|
|[CA1300](../code-quality/ca1300-specify-messageboxoptions.md)|指定 MessageBoxOptions|
|[CA1301](../code-quality/ca1301-avoid-duplicate-accelerators.md)|避免快捷键重复|
|[CA1302](../code-quality/ca1302-do-not-hardcode-locale-specific-strings.md)|不要对区域设置特定的字符串进行硬编码|
|[CA1303](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|请不要将文本作为本地化参数传递|
|[CA1304](../code-quality/ca1304-specify-cultureinfo.md)|指定 CultureInfo|
|[CA1305](../code-quality/ca1305-specify-iformatprovider.md)|指定 IFormatProvider|
|[CA1306](../code-quality/ca1306-set-locale-for-data-types.md)|设置数据类型的区域设置|
|[CA1307](../code-quality/ca1307-specify-stringcomparison.md)|指定 StringComparison|
|[CA1308](../code-quality/ca1308-normalize-strings-to-uppercase.md)|将字符串规范化为大写|
|[CA1309](../code-quality/ca1309-use-ordinal-stringcomparison.md)|使用按顺序的 StringComparison|
|[CA2101](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|指定对 P/Invoke 字符串参数进行封送处理|