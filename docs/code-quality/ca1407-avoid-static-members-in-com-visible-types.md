---
title: CA1407:避免在 COM 可见类型中使用静态成员
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
helpviewer_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
ms.assetid: bebd0776-ad04-453c-bca8-8c124c2d7840
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 631be1a93318cd24af4251fefbc710294fa52bf7
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922012"
---
# <a name="ca1407-avoid-static-members-in-com-visible-types"></a>CA1407:避免在 COM 可见类型中使用静态成员

|||
|-|-|
|TypeName|AvoidStaticMembersInComVisibleTypes|
|CheckId|CA1407|
|类别|Microsoft.Interoperability|
|是否重大更改|不间断|

## <a name="cause"></a>原因
特别标记为对组件对象模型 (COM) 可见的类型包含`public``static`方法。

## <a name="rule-description"></a>规则说明
COM 不支持`static`方法。

此规则忽略属性和事件访问器、运算符重载方法或使用<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName>特性<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>或特性标记的方法。

默认情况下, 以下是对 COM 可见的: 程序集、公共类型、公共类型中的公共实例成员以及公共值类型的所有成员。

若要发生此规则<xref:System.Runtime.InteropServices.ComVisibleAttribute> , 程序集级别必须设置为`false` , 并且类<xref:System.Runtime.InteropServices.ComVisibleAttribute>必须设置为`true`, 如以下代码所示。

```csharp
using System;
using System.Runtime.InteropServices;

[assembly: ComVisible(false)]
namespace Samples
{
    [ComVisible(true)]
    public class MyClass
    {
        public static void DoSomething()
        {
        }
    }
}
```

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将设计更改为使用提供与`static`方法相同的功能的实例方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果 COM 客户端不需要访问由`static`方法提供的功能, 则可以安全地禁止显示此规则发出的警告。

## <a name="example-violation"></a>示例冲突

### <a name="description"></a>描述
下面的示例演示`static`了违反此规则的方法。

### <a name="code"></a>代码
[!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersViolation#1](../code-quality/codesnippet/CSharp/ca1407-avoid-static-members-in-com-visible-types_1.cs)]

### <a name="comments"></a>注释
在此示例中, 无法从 COM 调用**FromPages**方法。

## <a name="example-fix"></a>示例修复

### <a name="description"></a>描述
若要解决上一示例中的冲突, 可以将方法更改为实例方法, 但这在此实例中没有意义。 更好的解决方案是显式应用`ComVisible(false)`于方法, 以使其他开发人员清楚地看不到 COM 中的方法。

下面的示例适用<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>于方法。

### <a name="code"></a>代码
[!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersFixed#1](../code-quality/codesnippet/CSharp/ca1407-avoid-static-members-in-com-visible-types_2.cs)]

## <a name="related-rules"></a>相关规则
[CA1017用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

[CA1406避免 Visual Basic 6 客户端的 Int64 参数](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)

[CA1413避免在 COM 可见值类型中出现非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

## <a name="see-also"></a>请参阅
[与非托管代码交互操作](/dotnet/framework/interop/index)