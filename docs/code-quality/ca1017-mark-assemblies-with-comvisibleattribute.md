---
title: CA1017:用 ComVisibleAttribute 标记程序集
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1017
- MarkAssembliesWithComVisible
helpviewer_keywords:
- MarkAssembliesWithComVisible
- CA1017
ms.assetid: 4842cb49-8dd8-4e5d-a2d6-ceeaf6c6cf8e
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: e6bc88d3932baa5bbb4a723d7a16509831d58146
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923092"
---
# <a name="ca1017-mark-assemblies-with-comvisibleattribute"></a>CA1017:用 ComVisibleAttribute 标记程序集

|||
|-|-|
|TypeName|MarkAssembliesWithComVisible|
|CheckId|CA1017|
|类别|Microsoft.Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
没有对程序集应用<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>属性。

## <a name="rule-description"></a>规则说明
<xref:System.Runtime.InteropServices.ComVisibleAttribute>特性确定 COM 客户端如何访问托管代码。 合理的设计指出程序集将显式指示 COM 可见性。 可以为整个程序集设置 COM 可见性, 然后为单个类型和类型成员重写 COM 可见性。 如果该属性不存在, 则该程序集的内容对 COM 客户端可见。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将特性添加到程序集。 如果你不希望程序集对 COM 客户端可见, 请应用属性, 并将其值设置为`false`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。 如果希望程序集可见, 请应用属性, 并将其值设置为`true`。

## <a name="example"></a>示例
下面的示例演示一个应用了<xref:System.Runtime.InteropServices.ComVisibleAttribute>特性的程序集, 以防止它对 COM 客户端可见。

[!code-cpp[FxCop.Design.AssembliesCom#1](../code-quality/codesnippet/CPP/ca1017-mark-assemblies-with-comvisibleattribute_1.cpp)]
[!code-vb[FxCop.Design.AssembliesCom#1](../code-quality/codesnippet/VisualBasic/ca1017-mark-assemblies-with-comvisibleattribute_1.vb)]
[!code-csharp[FxCop.Design.AssembliesCom#1](../code-quality/codesnippet/CSharp/ca1017-mark-assemblies-with-comvisibleattribute_1.cs)]

## <a name="see-also"></a>请参阅

- [与非托管代码交互操作](/dotnet/framework/interop/index)
- [为互操作限定 .NET 类型](/dotnet/framework/interop/qualifying-net-types-for-interoperation)