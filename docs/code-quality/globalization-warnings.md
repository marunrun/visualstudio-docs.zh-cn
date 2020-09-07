---
title: 全球化警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.globalizationrules
helpviewer_keywords:
- warnings, globalization
- globalization warnings
- globalization [Visual Studio], warnings
- managed code analysis warnings, globalization warnings
ms.assetid: a8d12d41-14bf-4b43-af24-168312d7c390
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd215a8b5c8dfb5905117638883d94d09268ce3d
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2020
ms.locfileid: "89509843"
---
# <a name="globalization-warnings"></a>全球化警告
全球化警告支持世界通用库和应用程序。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA1303:请不要将文本作为本地化参数传递](../code-quality/ca1303.md)|外部可见方法将字符串文本作为参数传递给 .NET 构造函数或方法，并且该字符串应可本地化。|
|[CA1304:指定 CultureInfo](../code-quality/ca1304.md)|某方法或构造函数调用的成员有一个接受 System.Globalization.CultureInfo 参数的重载，但该方法或构造函数没有调用接受 CultureInfo 参数的重载。 如果未提供 CultureInfo 或 System.IFormatProvider 对象，则重载成员提供的默认值可能不会在所有区域设置中产生您想要的效果。|
|[CA1305:指定 IFormatProvider](../code-quality/ca1305.md)|某方法或构造函数调用的一个或多个成员有接受 System.IFormatProvider 参数的重载，但该方法或构造函数没有调用接受 IFormatProvider 参数的重载。 如果未提供 System.Globalization.CultureInfo 或 IFormatProvider 对象，则重载成员提供的默认值可能不会在所有区域设置中产生您想要的效果。|
|[CA1306:设置数据类型的区域设置](../code-quality/ca1306.md)|区域设置决定数据的区域性特定显示元素，例如，数值、货币符号和排序顺序所用的格式。 在创建 DataTable 或 DataSet 时，应显式设置区域设置。|
|[CA1307:为了清晰起见，请指定 StringComparison](../code-quality/ca1307.md)|字符串比较运算使用不设置 StringComparison 参数的方法重载。|
|[CA1308:将字符串规范化为大写](../code-quality/ca1308.md)|字符串应正常化为大写字母。 少量字符转换为小写字母后不能再转换回来。|
|[CA1309:使用按顺序的 StringComparison](../code-quality/ca1309.md)|非语义的字符串比较运算不会将 StringComparison 参数设置为 Ordinal 或 OrdinalIgnoreCase。 因此，通过将参数显式设置为 StringComparison.Ordinal 或 StringComparison.OrdinalIgnoreCase，通常可以提高代码的速度、正确性和可靠性。|
|[CA1310：为了确保正确，请指定 StringComparison](../code-quality/ca1310.md)|在默认情况下，字符串比较操作使用未设置 StringComparison 参数并使用特定于区域性的字符串比较的方法重载。|
|[CA2101：为 P/Invoke 字符串参数指定封送处理](../code-quality/ca2101.md)|平台调用成员允许部分受信任的调用方，具有字符串参数，并不显式封送字符串。 这可能导致潜在的安全漏洞。|
