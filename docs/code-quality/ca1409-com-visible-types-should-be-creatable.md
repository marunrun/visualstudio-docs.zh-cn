---
title: CA1409:COM 可见类型应该是可创建的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
helpviewer_keywords:
- ComVisibleTypesShouldBeCreatable
- CA1409
ms.assetid: 9f59569b-de15-4a38-b7cb-cff152972243
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4196cb91e1b866453de54347b8a67edd3dc2dc96
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921894"
---
# <a name="ca1409-com-visible-types-should-be-creatable"></a>CA1409:COM 可见类型应该是可创建的

|||
|-|-|
|TypeName|ComVisibleTypesShouldBeCreatable|
|CheckId|CA1409|
|类别|Microsoft.Interoperability|
|是否重大更改|不间断|

## <a name="cause"></a>原因
特别标记为对组件对象模型 (COM) 可见的引用类型包含公共参数化构造函数, 但不包含公共默认 (无参数) 构造函数。

## <a name="rule-description"></a>规则说明
COM 客户端不能创建没有公共默认构造函数的类型。 但是, COM 客户端仍然可以访问该类型, 如果另一种方法可用于创建类型并将其传递给客户端 (例如, 通过方法调用的返回值)。

规则将忽略派生自<xref:System.Delegate?displayProperty=fullName>的类型。

默认情况下, 以下是对 COM 可见的: 程序集、公共类型、公共类型中的公共实例成员以及公共值类型的所有成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请添加一个公共的默认构造<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>函数或从该类型中删除。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果提供了其他方法来创建对象并将其传递给 COM 客户端, 则可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
[CA1017用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅

- [为互操作限定 .NET 类型](/dotnet/framework/interop/qualifying-net-types-for-interoperation)
- [与非托管代码交互操作](/dotnet/framework/interop/index)