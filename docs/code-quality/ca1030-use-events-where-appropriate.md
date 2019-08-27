---
title: CA1030:在适用处使用事件
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- UseEventsWhereAppropriate
- CA1030
helpviewer_keywords:
- CA1030
- UseEventsWhereAppropriate
ms.assetid: ea051367-deeb-40f9-9b65-eb818f1e133a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ad0659241e75c862b3d82c64a7e8b2ad3ccada21
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547674"
---
# <a name="ca1030-use-events-where-appropriate"></a>CA1030:在适用处使用事件

|||
|-|-|
|TypeName|UseEventsWhereAppropriate|
|CheckId|CA1030|
|类别|Microsoft.Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因

方法名称以下列之一开头:

- AddOn
- RemoveOn
- 火灾
- 提出

默认情况下, 此规则仅查看外部可见方法, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

该规则检测名称通常用于事件的方法。 事件遵循观察程序或发布-订阅设计模式;当必须将一个对象中的状态更改传递到其他对象时, 使用它们。 如果调用方法以响应明确定义的状态更改, 则应由事件处理程序调用方法。 调用该方法的对象应引发事件而不是直接调用该方法。

事件的一些常见示例位于用户界面应用程序中, 用户操作 (例如单击按钮) 会导致执行代码段。 .NET 事件模型并不局限于用户界面。 应在必须将状态更改传达给一个或多个对象的任何位置使用它。

## <a name="how-to-fix-violations"></a>如何解决冲突

如果在对象的状态发生更改时调用方法, 请考虑将设计更改为使用 .NET 事件模型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果此方法无法与 .NET 事件模型一起使用, 则禁止显示此规则发出的警告。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 editorconfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca1030.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (设计) 配置此选项。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。
