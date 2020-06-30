---
title: CA1300：指定 MessageBoxOptions |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyMessageBoxOptions
- CA1300
helpviewer_keywords:
- SpecifyMessageBoxOptions
- CA1300
ms.assetid: 9357a724-026e-4a3d-a03a-f14635064ec6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: af0017a7ee6918a80a93ca90c7cf3de78885d61f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539186"
---
# <a name="ca1300-specify-messageboxoptions"></a>CA1300:指定 MessageBoxOptions
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|SpecifyMessageBoxOptions|
|CheckId|CA1300|
|Category|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法调用不 <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> 采用参数的方法的重载 <xref:System.Windows.Forms.MessageBoxOptions?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 若要为使用从右到左读取顺序的区域性正确地显示消息框，则 <xref:System.Windows.Forms.MessageBoxOptions> <xref:System.Windows.Forms.MessageBoxOptions> <xref:System.Windows.Forms.MessageBoxOptions> 必须将枚举的和成员传递给 <xref:System.Windows.Forms.MessageBox.Show%2A> 方法。 检查 <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName> 包含控件的属性，以确定是否使用从右到左的读取顺序。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请调用 <xref:System.Windows.Forms.MessageBox.Show%2A> 采用参数的方法的重载 <xref:System.Windows.Forms.MessageBoxOptions> 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果代码库不是使用从右到左读取顺序的区域性进行本地化，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个方法，该方法显示一个消息框，该消息框具有适用于区域性读取顺序的选项。 生成示例需要一个不显示的资源文件。 按照示例中的注释生成没有资源文件的示例，并测试从右到左的功能。

 [!code-csharp[FxCop.Globalization.SpecifyMBOptions#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/cs/FxCop.Globalization.SpecifyMBOptions.cs#1)]
 [!code-vb[FxCop.Globalization.SpecifyMBOptions#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/vb/FxCop.Globalization.SpecifyMBOptions.vb#1)]

## <a name="see-also"></a>另请参阅
 <xref:System.Resources.ResourceManager?displayProperty=fullName> [桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
