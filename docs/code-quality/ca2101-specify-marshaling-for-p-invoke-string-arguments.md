---
title: CA2101:指定对 P-Invoke 字符串自变量进行封送处理
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SpecifyMarshalingForPInvokeStringArguments
- CA2101
helpviewer_keywords:
- CA2101
- SpecifyMarshalingForPInvokeStringArguments
ms.assetid: 9d1abfc3-d320-41e0-9f6e-60cefe6ffe1b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f49c9dfdac1d8d8aec8ec32df7374b5ae0a28e92
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233028"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101:指定对 P/Invoke 字符串参数进行封送处理

|||
|-|-|
|TypeName|SpecifyMarshalingForPInvokeStringArguments|
|CheckId|CA2101|
|类别|Microsoft.Globalization|
|重大更改|不间断|

## <a name="cause"></a>原因
平台调用成员允许部分受信任的调用方，具有字符串参数，并不显式封送字符串。

## <a name="rule-description"></a>规则说明
从 Unicode 转换为 ANSI 时，可能并非所有 Unicode 字符都可以在特定 ANSI 代码页中表示。 *最佳映射*尝试通过将不能表示的字符替换为字符来解决此问题。 使用此功能可能会导致潜在的安全漏洞，因为您无法控制所选的字符。 例如，恶意代码可能会有意创建一个 Unicode 字符串，其中包含在特定代码页中找不到的字符，这些字符将转换为文件系统特殊字符，如 ".." 或 "/"。 另请注意，在将字符串转换为 ANSI 之前，通常会检查是否存在特殊字符。

最佳映射是非托管转换的默认值，WChar 到 Mb。 除非显式禁用最佳映射，否则，由于此问题，你的代码可能包含可利用的安全漏洞。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请显式封送字符串数据类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反此规则的方法，并演示如何修复冲突。

[!code-csharp[FxCop.Security.PinvokeAnsiUnicode#1](../code-quality/codesnippet/CSharp/ca2101-specify-marshaling-for-p-invoke-string-arguments_1.cs)]