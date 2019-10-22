---
title: CA1301：避免重复快捷键 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 647fef2968971cddb6a14cc19e53eed979b9c151
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661520"
---
# <a name="ca1301-avoid-duplicate-accelerators"></a>CA1301：避免快捷键重复
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidDuplicateAccelerators|
|CheckId|CA1301|
|类别|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型扩展 <xref:System.Windows.Forms.Control?displayProperty=fullName>，并包含两个或多个具有存储在资源文件中的相同访问键的顶级控件。

## <a name="rule-description"></a>规则说明
 访问键也称为快捷键，它通过使用 Alt 键来实现对控件的键盘访问。 如果多个控件具有重复的访问键，则访问键的行为定义不正确。 用户可能不能使用访问键和控件（而不是可能启用的控件）访问目标控件。

 此规则的当前实现忽略菜单项。 但是，同一子菜单中的菜单项不应具有相同的访问键。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请为所有控件定义唯一的访问密钥。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个包含两个具有相同访问键的控件的最小形式。 密钥存储在不显示的资源文件中;但是，它们的值显示在注释掉的 `checkBox.Text` 行中。 可以通过将 `checkBox.Text` 行与注释掉的对应项交换来检查重复快捷键的行为。 但是，在这种情况下，该示例不会从规则生成警告。

 [!code-csharp[FxCop.Globalization.AvoidDuplicateAccels#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.AvoidDuplicateAccels/cs/FxCop.Globalization.AvoidDuplicateAccels.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Resources.ResourceManager?displayProperty=fullName>[桌面应用中的资源](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
