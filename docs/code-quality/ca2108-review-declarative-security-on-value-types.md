---
title: CA2108:检查有关值类型的声明性安全
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
helpviewer_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
ms.assetid: d62bffdd-3826-4d52-a708-1c646c5d48c2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 37f4cac83c83b47fda5cf9cde85a3e14d857d2bc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545533"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108:检查有关值类型的声明性安全

|||
|-|-|
|TypeName|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

公共或受保护值类型受[数据和建模](/dotnet/framework/data/index)或[链接要求](/dotnet/framework/misc/link-demands)。

## <a name="rule-description"></a>规则说明

分配和其他构造函数执行前通过其默认构造函数初始化值类型。 如果值类型保护的 Demand 或 LinkDemand，并且调用方没有权限而不满足安全检查，任何构造函数的默认值将失败，并且将引发安全异常。 未释放的值类型;它将继续处于其默认构造函数设置的状态。 不要假定将传递值类型的实例的调用方有权创建或访问该实例。

## <a name="how-to-fix-violations"></a>如何解决冲突

除非从类型中删除的安全检查和使用方法级别的安全检查在其原位置，则无法修复该规则的冲突。 以这种方式解决冲突不会阻止调用方与从获取值类型的实例的权限不足。 您必须确保中默认状态下，值类型的实例不会公开敏感信息，并且不能以有害方式使用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果任何调用方可以获得在其默认状态的值类型的实例，而不会造成安全风险，可以禁止显示此规则的警告。

## <a name="example-1"></a>示例 1

下面的示例演示一个库，包含与此规则冲突的值类型。 `StructureManager`类型假定将传递值类型的实例的调用方有权创建或访问该实例。

[!code-csharp[FxCop.Security.DemandOnValueType#1](../code-quality/codesnippet/CSharp/ca2108-review-declarative-security-on-value-types_1.cs)]

## <a name="example-2"></a>示例 2

以下应用程序演示库的弱点。

[!code-csharp[FxCop.Security.TestDemandOnValueType#1](../code-quality/codesnippet/CSharp/ca2108-review-declarative-security-on-value-types_2.cs)]

该示例产生下面的输出：

```txt
Structure custom constructor: Request failed.
New values SecuredTypeStructure 100 100
New values SecuredTypeStructure 200 200
```

## <a name="see-also"></a>请参阅

- [链接需求](/dotnet/framework/misc/link-demands)
- [数据和建模](/dotnet/framework/data/index)
