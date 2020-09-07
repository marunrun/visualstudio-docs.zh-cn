---
title: 托管代码的“全球化规则”规则集
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 3c4032ee-0805-4581-8c48-b1827cd6b213
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 2af6126c751d03968dc7ecd87693e3546376c12a
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2020
ms.locfileid: "89509856"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>托管代码的“全球化规则”规则集

使用 "Microsoft 全球化规则" 规则集将重点放在可能阻止应用程序中的数据在不同语言、区域设置和区域性中正确显示的问题。 如果你的应用程序已本地化、全球化，则应包含此规则集。

|规则|描述|
|----------|-----------------|
|[CA1303](../code-quality/ca1303.md)|请不要将文本作为本地化参数传递|
|[CA1304](../code-quality/ca1304.md)|指定 CultureInfo|
|[CA1305](../code-quality/ca1305.md)|指定 IFormatProvider|
|[CA1307](../code-quality/ca1307.md)|为清楚起见指定 StringComparison|
|[CA1308](../code-quality/ca1308.md)|将字符串规范化为大写|
|[CA1309](../code-quality/ca1309.md)|使用按顺序的 StringComparison|
|[CA1310](../code-quality/ca1310.md)|指定 StringComparison 是否正确|
|[CA2101](../code-quality/ca2101.md)|指定对 P/Invoke 字符串参数进行封送处理|
