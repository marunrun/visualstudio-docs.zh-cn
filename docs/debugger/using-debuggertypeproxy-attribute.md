---
title: 显示自定义类型使用 DebuggerTypeProxy |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- attributes [C#], debugger
- DebuggerTypeProxyAttribute class
- DebuggerTypeProxy attribute
ms.assetid: 943f3bb1-993e-4800-a47e-0af78b063014
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c379fbeb9d17f92dcc7067424ea06bb1a2805ed1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929639"
---
# <a name="tell-the-debugger-what-type-to-show-using-debuggertypeproxy-attribute-c-visual-basic-ccli"></a>让调试器在哪种类型来演示如何使用 DebuggerTypeProxy 特性 (C#，Visual Basic 中， C++/CLI)

<xref:System.Diagnostics.DebuggerTypeProxyAttribute> 指定类型的代理或替身，并更改类型在调试器窗口中的显示方式。 查看具有代理的变量时，代理将代替“显示”中的原始类型。 调试器变量窗口仅显示代理类型的公共成员。 不会显示私有成员。

此特性可应用于：

- 结构
- 类
- 程序集

> [!NOTE]
> 对于本机代码，此属性仅支持在C++/CLI 代码。

类型代理类必须具有一个构造函数，该函数采用代理将替换的类型的参数。 在每次需要显示目标类型的变量时，调试器都会创建类型代理类的一个新实例。 这会对性能产生一定影响。 因此，不应在构造函数中执行非必需的工作。

若要最大程度地减小性能损失，表达式计算器将不检查类型的显示代理上的特性，除非用户在调试器窗口中单击 + 符号或使用 <xref:System.Diagnostics.DebuggerBrowsableAttribute> 扩展该类型。 因此，不应将特性置于显示类型自身中。 特性可以且应该用于显示类型的正文中。

类型代理最好是作为特性目标类中的私有嵌套类。 这样，它便能轻松访问内部成员。

<xref:System.Diagnostics.DebuggerTypeProxyAttribute> 可以继承，因此如果基础类上指定类型代理，则它将适用于任何派生的类，除非这些派生的类指定其自身类型代理。

如果在程序集级别使用 <xref:System.Diagnostics.DebuggerTypeProxyAttribute>，则 `Target` 参数将指定代理要替换的类型。

有关如何使用与此特性的示例<xref:System.Diagnostics.DebuggerDisplayAttribute>并<xref:System.Diagnostics.DebuggerTypeProxyAttribute>，请参阅[使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)。

## <a name="using-generics-with-debuggertypeproxy"></a>将泛型与 DebuggerTypeProxy 一起使用

对泛型的支持是有限的。 对于 C#，`DebuggerTypeProxy` 只支持开放类型。 开放类型（也称作“非构造类型”）是一种还未使用其类型参数的自变量实例化的泛型类型。 不支持封闭类型（也称作“构造类型”）。

开放类型的语法类似于：

`Namespace.TypeName<,>`

如果使用泛型类型作为 `DebuggerTypeProxy` 中的目标，则必须使用该语法。 `DebuggerTypeProxy` 机制将为你推理类型参数。

C# 中的打开和关闭类型的详细信息请参阅[C# 语言规范](/dotnet/csharp/language-reference/language-specification)，第 20.5.2 节打开和关闭类型。

Visual Basic 没有开放类型语法，因此您无法在 Visual Basic 中执行同样的操作。 而必须使用开放类型名称的字符串表示形式。

`"Namespace.TypeName'2"`

## <a name="see-also"></a>请参阅

- [使用 DebuggerDisplay 特性](../debugger/using-the-debuggerdisplay-attribute.md)
- [创建 .managed 对象的自定义视图](../debugger/create-custom-views-of-dot-managed-objects.md)
- [使用调试器显示特性增强调试](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
