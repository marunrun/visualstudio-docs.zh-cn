---
title: CA2101:指定对 P-invoke 字符串参数封送处理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyMarshalingForPInvokeStringArguments
- CA2101
helpviewer_keywords:
- CA2101
- SpecifyMarshalingForPInvokeStringArguments
ms.assetid: 9d1abfc3-d320-41e0-9f6e-60cefe6ffe1b
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 11916609f2efa9c0b6e208548ba51795bd276015
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154392"
---
# <a name="ca2101-specify-marshaling-for-pinvoke-string-arguments"></a>CA2101:指定对 P/Invoke 字符串参数进行封送处理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SpecifyMarshalingForPInvokeStringArguments|
|CheckId|CA2101|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 平台调用成员允许部分受信任调用方具有一个字符串参数，并且不显式封送字符串。

## <a name="rule-description"></a>规则说明
 当你从 Unicode 转换为 ANSI 时，就可以不是所有 Unicode 字符，可以都表示特定的 ANSI 代码页。 *最佳匹配映射*尝试解决此问题，只需替换不能表示的字符的字符。 此功能的使用可能导致潜在的安全漏洞，因为您无法控制选择的字符。 例如，恶意代码会有意创建一个包含在特定代码页中，找不到该文件系统的特殊字符会转换为的字符的 Unicode 字符串 '..' 或 /。 另请注意的特殊字符的安全检查经常发生之前将字符串转换为 ANSI。

 对于非托管的转换，mb 的磁盘到 WChar 默认值为最佳的映射。 除非显式禁用最佳的映射，你的代码可能包含可利用的安全漏洞，由于此问题。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，显式封送字符串数据类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个方法，违反了此规则，并展示了如何解决冲突。

 [!code-csharp[FxCop.Security.PinvokeAnsiUnicode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PinvokeAnsiUnicode/cs/FxCop.Security.PinvokeAnsiUnicode.cs#1)]
