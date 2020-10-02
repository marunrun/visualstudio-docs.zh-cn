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
ms.openlocfilehash: 0c3b899ec8e19160d9ee4a307a86c576d217004c
ms.sourcegitcommit: c025a5e2013c4955ca685092b13e887ce64aaf64
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91658537"
---
# <a name="globalization-rules-rule-set-for-managed-code"></a>托管代码的“全球化规则”规则集

使用 "Microsoft 全球化规则" 规则集将重点放在可能阻止应用程序中的数据在不同语言、区域设置和区域性中正确显示的问题。 如果你的应用程序已本地化、全球化，则应包含此规则集。

|规则|描述|
|----------|-----------------|
|[CA1303](/dotnet/fundamentals/code-analysis/quality-rules/ca1303)|请不要将文本作为本地化参数传递|
|[CA1304](/dotnet/fundamentals/code-analysis/quality-rules/ca1304)|指定 CultureInfo|
|[CA1305](/dotnet/fundamentals/code-analysis/quality-rules/ca1305)|指定 IFormatProvider|
|[CA1307](/dotnet/fundamentals/code-analysis/quality-rules/ca1307)|为清楚起见指定 StringComparison|
|[CA1308](/dotnet/fundamentals/code-analysis/quality-rules/ca1308)|将字符串规范化为大写|
|[CA1309](/dotnet/fundamentals/code-analysis/quality-rules/ca1309)|使用按顺序的 StringComparison|
|[CA1310](/dotnet/fundamentals/code-analysis/quality-rules/ca1310)|指定 StringComparison 是否正确|
|[CA2101](/dotnet/fundamentals/code-analysis/quality-rules/ca2101)|指定对 P/Invoke 字符串参数进行封送处理|
