---
title: CA1402:避免在 COM 可见接口中进行重载
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidOverloadsInComVisibleInterfaces
- CA1402
helpviewer_keywords:
- AvoidOverloadsInComVisibleInterfaces
- CA1402
ms.assetid: 2724c1f9-d5d3-4704-b124-21c4d398e5df
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: aa45a54a994d19b1a04bc0785f21b88dfeef4475
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922128"
---
# <a name="ca1402-avoid-overloads-in-com-visible-interfaces"></a>CA1402:避免在 COM 可见接口中进行重载

|||
|-|-|
|TypeName|AvoidOverloadsInComVisibleInterfaces|
|CheckId|CA1402|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
组件对象模型 (COM) 可见接口声明重载方法。

## <a name="rule-description"></a>规则说明
在向 COM 客户端公开重载的方法时，只有第一个方法重载保留其名称。 通过在名称后追加下划线字符 "_" 和一个与重载的声明顺序相对应的整数, 可对后续重载进行唯一重命名。 例如, 考虑以下方法:

```csharp
void SomeMethod(int valueOne);
void SomeMethod(int valueOne, int valueTwo, int valueThree);
void SomeMethod(int valueOne, int valueTwo);
```

如下所示, 将这些方法公开给 COM 客户端。

```csharp
void SomeMethod(int valueOne);
void SomeMethod_2(int valueOne, int valueTwo, int valueThree);
void SomeMethod_3(int valueOne, int valueTwo);
```

Visual Basic 6, COM 客户端无法通过在名称中使用下划线来实现接口方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请重命名重载的方法, 使名称唯一。 或者, 通过将可访问性更改`internal`为 (`Friend`在中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]为) 或<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>将属性设置为`false`, 使接口对 COM 不可见。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示了违反规则的接口和满足规则的接口。

[!code-vb[FxCop.Interoperability.OverloadsInterface#1](../code-quality/codesnippet/VisualBasic/ca1402-avoid-overloads-in-com-visible-interfaces_1.vb)]
[!code-csharp[FxCop.Interoperability.OverloadsInterface#1](../code-quality/codesnippet/CSharp/ca1402-avoid-overloads-in-com-visible-interfaces_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1413避免在 COM 可见值类型中出现非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

[CA1407避免在 COM 可见类型中出现静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

[CA1017用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅

- [与非托管代码交互操作](/dotnet/framework/interop/index)
- [Long 数据类型](/dotnet/visual-basic/language-reference/data-types/long-data-type)