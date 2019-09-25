---
title: CA1300:指定 MessageBoxOptions
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SpecifyMessageBoxOptions
- CA1300
helpviewer_keywords:
- SpecifyMessageBoxOptions
- CA1300
ms.assetid: 9357a724-026e-4a3d-a03a-f14635064ec6
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 746475e60bbe72c4ebfc51f13d0b2d4d0552ff62
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235192"
---
# <a name="ca1300-specify-messageboxoptions"></a>CA1300:指定 MessageBoxOptions

|||
|-|-|
|TypeName|SpecifyMessageBoxOptions|
|CheckId|CA1300|
|类别|Microsoft.Globalization|
|重大更改|不间断|

## <a name="cause"></a>原因

方法调用不<xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> <xref:System.Windows.Forms.MessageBoxOptions?displayProperty=fullName>采用参数的方法的重载。

## <a name="rule-description"></a>规则说明

若要为使用从右到左读取顺序的区域性正确显示消息框，请将[MessageBoxOptions](<xref:System.Windows.Forms.MessageBoxOptions.RightAlign>)和[RtlReading](<xref:System.Windows.Forms.MessageBoxOptions.RtlReading>) <xref:System.Windows.Forms.MessageBox.Show%2A>字段传递给方法。 检查包含控件的属性，以确定是否使用从右到左的读取顺序。<xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请调用<xref:System.Windows.Forms.MessageBox.Show%2A> <xref:System.Windows.Forms.MessageBoxOptions>采用参数的方法的重载。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果代码库不是使用从右到左读取顺序的区域性进行本地化，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示一个方法，该方法显示一个消息框，该消息框具有适用于区域性读取顺序的选项。 生成示例需要一个不显示的资源文件。 按照示例中的注释生成没有资源文件的示例，并测试从右到左的功能。

[!code-vb[FxCop.Globalization.SpecifyMBOptions#1](../code-quality/codesnippet/VisualBasic/ca1300-specify-messageboxoptions_1.vb)]
[!code-csharp[FxCop.Globalization.SpecifyMBOptions#1](../code-quality/codesnippet/CSharp/ca1300-specify-messageboxoptions_1.cs)]

## <a name="see-also"></a>请参阅

- <xref:System.Resources.ResourceManager?displayProperty=fullName>
- [桌面应用中的资源 (.NET Framework)](/dotnet/framework/resources/index)