---
title: CA1306：设置数据类型的区域设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1306
- SetLocaleForDataTypes
helpviewer_keywords:
- CA1306
- SetLocaleForDataTypes
ms.assetid: 104297b2-5806-4de0-a8d9-c589380a796c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 03344f0b19552aa00270c8a6fa760c6ba6ee75f4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661418"
---
# <a name="ca1306-set-locale-for-data-types"></a>CA1306：设置数据类型的区域设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SetLocaleForDataTypes|
|CheckId|CA1306|
|类别|Microsoft 全球化|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法或构造函数创建了一个或多个 <xref:System.Data.DataTable?displayProperty=fullName> 或 <xref:System.Data.DataSet?displayProperty=fullName> 实例，但未显式设置区域设置属性（<xref:System.Data.DataTable.Locale%2A?displayProperty=fullName> 或 <xref:System.Data.DataSet.Locale%2A?displayProperty=fullName>）。

## <a name="rule-description"></a>规则说明
 区域设置确定数据的区域性特定的表示法元素，例如用于数值、货币符号和排序顺序的格式设置。 创建 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 时，应显式设置区域设置。 默认情况下，这些类型的区域设置为当前区域性。 对于存储在数据库或文件中并且全局共享的数据，区域设置通常应设置为固定区域性（<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>）。 如果跨区域性共享数据，则使用默认区域设置可能导致 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 的内容被错误地显示或解释。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请显式设置 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 的区域设置。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果库或应用程序适用于受限制的本地用户、数据不共享或默认设置在所有支持的方案中生成所需的行为，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例创建两个 <xref:System.Data.DataTable> 实例。

 [!code-csharp[FxCop.Globalization.DataTable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DataTable/cs/FxCop.Globalization.DataTable.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Data.DataTable?displayProperty=fullName> <xref:System.Data.DataSet?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>
