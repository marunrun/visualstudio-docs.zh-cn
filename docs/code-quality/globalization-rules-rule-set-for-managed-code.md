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
ms.openlocfilehash: 4a4aa987c58ace1bb2fa8c0a2dfac3c0aecd87d7
ms.sourcegitcommit: 08c144d290da373df841f04fc799e3133540a541
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2019
ms.locfileid: "72535862"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>托管代码的“全球化规则”规则集

使用 "Microsoft 全球化规则" 规则集将重点放在可能阻止应用程序中的数据在不同语言、区域设置和区域性中正确显示的问题。 如果你的应用程序已本地化、全球化，则应包含此规则集。

|规则|描述|
|----------|-----------------|
|[CA1300](../code-quality/ca1300.md)|指定 MessageBoxOptions|
|[CA1301](../code-quality/ca1301.md)|避免快捷键重复|
|[CA1302](../code-quality/ca1302.md)|不要对区域设置特定的字符串进行硬编码|
|[CA1303](../code-quality/ca1303.md)|请不要将文本作为本地化参数传递|
|[CA1304](../code-quality/ca1304.md)|指定 CultureInfo|
|[CA1305](../code-quality/ca1305.md)|指定 IFormatProvider|
|[CA1306](../code-quality/ca1306.md)|设置数据类型的区域设置|
|[CA1307](../code-quality/ca1307.md)|指定 StringComparison|
|[CA1308](../code-quality/ca1308.md)|将字符串规范化为大写|
|[CA1309](../code-quality/ca1309.md)|使用按顺序的 StringComparison|
|[CA2101](../code-quality/ca2101.md)|指定对 P/Invoke 字符串参数进行封送处理|
