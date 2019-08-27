---
title: CA1306:设置区域设置的数据类型 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 75e67cdd058939837441bd969ac8629a6fc65dcc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200359"
---
# <a name="ca1306-set-locale-for-data-types"></a>CA1306:设置数据类型的区域设置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SetLocaleForDataTypes|
|CheckId|CA1306|
|类别|Microsoft.Globalization|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 方法或构造函数创建一个或多个<xref:System.Data.DataTable?displayProperty=fullName>或<xref:System.Data.DataSet?displayProperty=fullName>实例和未显式设置区域设置属性 (<xref:System.Data.DataTable.Locale%2A?displayProperty=fullName>或<xref:System.Data.DataSet.Locale%2A?displayProperty=fullName>)。

## <a name="rule-description"></a>规则说明
 区域设置决定数据，如所用的数值、 货币符号和排序顺序格式区域性特定显示的元素。 当您创建<xref:System.Data.DataTable>或<xref:System.Data.DataSet>，应显式设置的区域设置。 默认情况下，这些类型的区域设置为当前区域性。 对于存储在数据库或文件中，全局共享的数据，区域设置应通常设置为固定区域性 (<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>)。 在各个区域性共享数据，使用默认区域设置可能会引起的内容<xref:System.Data.DataTable>或<xref:System.Data.DataSet>要显示或不正确解释。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请显式设置的区域设置<xref:System.Data.DataTable>或<xref:System.Data.DataSet>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，当库或应用程序适用于有限的本地用户，不共享的数据，或默认设置可以生成在所有支持的方案所需的行为。

## <a name="example"></a>示例
 下面的示例创建两个<xref:System.Data.DataTable>实例。

 [!code-csharp[FxCop.Globalization.DataTable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DataTable/cs/FxCop.Globalization.DataTable.cs#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Data.DataTable?displayProperty=fullName> <xref:System.Data.DataSet?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>
