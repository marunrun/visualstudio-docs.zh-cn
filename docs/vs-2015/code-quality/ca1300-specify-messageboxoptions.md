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
ms.openlocfilehash: 3e21866fce69f768d927882d3ddd47ae3e431265
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663611"
---
# <a name="ca1300-specify-messageboxoptions"></a>CA1300：指定 MessageBoxOptions
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SpecifyMessageBoxOptions|
|CheckId|CA1300|
|类别|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法调用 <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> 方法的重载，该重载不采用 <xref:System.Windows.Forms.MessageBoxOptions?displayProperty=fullName> 参数。

## <a name="rule-description"></a>规则说明
 若要为使用从右到左读取顺序的区域性正确显示消息框，<xref:System.Windows.Forms.MessageBoxOptions> 枚举的 <xref:System.Windows.Forms.MessageBoxOptions> 和 <xref:System.Windows.Forms.MessageBoxOptions> 成员必须传递到 <xref:System.Windows.Forms.MessageBox.Show%2A> 方法。 检查包含控件的 <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName> 属性，确定是否使用从右到左的读取顺序。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请调用采用 <xref:System.Windows.Forms.MessageBoxOptions> 参数的 <xref:System.Windows.Forms.MessageBox.Show%2A> 方法的重载。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果代码库不是使用从右到左读取顺序的区域性进行本地化，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个方法，该方法显示一个消息框，该消息框具有适用于区域性读取顺序的选项。 生成示例需要一个不显示的资源文件。 按照示例中的注释生成没有资源文件的示例，并测试从右到左的功能。

 [!code-csharp[FxCop.Globalization.SpecifyMBOptions#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/cs/FxCop.Globalization.SpecifyMBOptions.cs#1)]
 [!code-vb[FxCop.Globalization.SpecifyMBOptions#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/vb/FxCop.Globalization.SpecifyMBOptions.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Resources.ResourceManager?displayProperty=fullName>[桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
