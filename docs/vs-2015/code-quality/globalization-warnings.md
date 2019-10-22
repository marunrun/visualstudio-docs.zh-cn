---
title: 全球化警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.globalizationrules
helpviewer_keywords:
- warnings, globalization
- globalization warnings
- globalization [Visual Studio], warnings
- managed code analysis warnings, globalization warnings
ms.assetid: a8d12d41-14bf-4b43-af24-168312d7c390
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7db942f410b9a6a8c2f12a044d0e48ad1ad19950
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667587"
---
# <a name="globalization-warnings"></a>全球化警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

全球化警告支持世界通用库和应用程序。

## <a name="in-this-section"></a>本节内容

|规则|描述|
|----------|-----------------|
|[CA1300：指定 MessageBoxOptions](../code-quality/ca1300-specify-messageboxoptions.md)|为了让使用从右到左阅读顺序的文化区域正确显示消息框，必须将 MessageBoxOptions 枚举的 RightAlign 和 RtlReading 成员传递给 Show 方法。|
|[CA1301：避免快捷键重复](../code-quality/ca1301-avoid-duplicate-accelerators.md)|访问键也称为快捷键，它通过使用 Alt 键来实现对控件的键盘访问。 如果多个控件具有重复的访问键，则访问键的行为定义不正确。|
|[CA1302：请不要对区域设置特定的字符串进行硬编码](../code-quality/ca1302-do-not-hardcode-locale-specific-strings.md)|System.Environment.SpecialFolder 枚举包含表示特殊系统文件夹的成员。 对于不同的操作系统，这些文件夹的位置可能具有不同的值；用户也可能会更改某些位置；或者这些位置已经进行了本地化。 Environment.GetFolderPath 方法返回与 Environment.SpecialFolder 枚举关联、经过本地化且与当前正在运行的计算机相应的位置。|
|[CA1303：不要将文本作为本地化参数传递](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|某外部可见的方法将一个字符串作为参数传递给 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类库中的构造函数或方法，该字符串应该是可本地化的。|
|[CA1304：指定 CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)|某方法或构造函数调用的成员有一个接受 System.Globalization.CultureInfo 参数的重载，但该方法或构造函数没有调用接受 CultureInfo 参数的重载。 如果未提供 CultureInfo 或 System.IFormatProvider 对象，则重载成员提供的默认值可能不会在所有区域设置中产生您想要的效果。|
|[CA1305：指定 IFormatProvider](../code-quality/ca1305-specify-iformatprovider.md)|某方法或构造函数调用的一个或多个成员有接受 System.IFormatProvider 参数的重载，但该方法或构造函数没有调用接受 IFormatProvider 参数的重载。 如果未提供 System.Globalization.CultureInfo 或 IFormatProvider 对象，则重载成员提供的默认值可能不会在所有区域设置中产生您想要的效果。|
|[CA1306：设置数据类型的区域设置](../code-quality/ca1306-set-locale-for-data-types.md)|区域设置决定数据的区域性特定显示元素，例如，数值、货币符号和排序顺序所用的格式。 在创建 DataTable 或 DataSet 时，应显式设置区域设置。|
|[CA1307：指定 StringComparison](../code-quality/ca1307-specify-stringcomparison.md)|字符串比较运算使用不设置 StringComparison 参数的方法重载。|
|[CA1308：将字符串规范化为大写](../code-quality/ca1308-normalize-strings-to-uppercase.md)|字符串应正常化为大写字母。 少量字符转换为小写字母后不能再转换回来。|
|[CA1309：使用序号 StringComparison](../code-quality/ca1309-use-ordinal-stringcomparison.md)|非语义的字符串比较运算不会将 StringComparison 参数设置为 Ordinal 或 OrdinalIgnoreCase。 因此，通过将参数显式设置为 StringComparison.Ordinal 或 StringComparison.OrdinalIgnoreCase，通常可以提高代码的速度、正确性和可靠性。|
|[CA2101：指定对 P/Invoke 字符串参数进行封送处理](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|平台调用成员允许部分受信任的调用方，具有字符串参数，并不显式封送字符串。 这可能导致潜在的安全漏洞。|
