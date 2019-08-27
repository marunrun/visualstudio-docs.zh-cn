---
title: CA1301:避免快捷键重复 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1301
- AvoidDuplicateAccelerators
helpviewer_keywords:
- CA1301
- AvoidDuplicateAccelerators
ms.assetid: 20570a00-864b-459c-a1fa-a6e9db5f1001
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a2e992cfb648b9b7f84032abab2f96d3f7cb410d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686854"
---
# <a name="ca1301-avoid-duplicate-accelerators"></a>CA1301:避免快捷键重复
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidDuplicateAccelerators|
|CheckId|CA1301|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 类型扩展<xref:System.Windows.Forms.Control?displayProperty=fullName>和包含两个或多个具有相同的访问密钥存储在资源文件中的最高级别控件。

## <a name="rule-description"></a>规则说明
 访问键也称为快捷键，它通过使用 Alt 键来实现对控件的键盘访问。 如果多个控件具有重复的访问键，则访问键的行为定义不正确。 用户可能无法再访问目标的控件通过使用访问密钥，并且可能会启用旨在以外的控件。

 此规则的当前实现将忽略菜单项。 但是，相同的子菜单中的菜单项不应具有相同的访问密钥。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请定义所有控件的唯一访问的密钥。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个包含具有相同的访问键的两个控件的最小窗体。 在资源文件中，而不会显示; 存储的密钥但是，其值显示在注释掉`checkBox.Text`行。 可以通过交换检查的快捷键重复行为`checkBox.Text`具有对应的注释掉的行。 但是，在这种情况下，该示例不会生成警告规则。

 [!code-csharp[FxCop.Globalization.AvoidDuplicateAccels#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.AvoidDuplicateAccels/cs/FxCop.Globalization.AvoidDuplicateAccels.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Resources.ResourceManager?displayProperty=fullName> [桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
