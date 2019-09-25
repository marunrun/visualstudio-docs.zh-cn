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
ms.openlocfilehash: 4107800a5623de29448a9213184dd44feed2cac9
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232816"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108:检查有关值类型的声明性安全

|||
|-|-|
|TypeName|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

公共或受保护值类型受[数据和建模](/dotnet/framework/data/index)或[链接要求](/dotnet/framework/misc/link-demands)保护。

## <a name="rule-description"></a>规则说明

值类型在其他构造函数执行之前由其默认构造函数进行分配和初始化。 如果值类型受需求或 LinkDemand 的保护，并且调用方没有满足安全检查要求的权限，则除默认值以外的任何构造函数都将失败，并将引发安全异常。 未解除分配值类型;它保留为其默认构造函数设置的状态。 不要假设传递值类型的实例的调用方有权创建或访问该实例。

## <a name="how-to-fix-violations"></a>如何解决冲突

除非从类型中删除安全检查并在其位置使用方法级安全检查，否则不能修复此规则的冲突。 以这种方式修复冲突不会阻止权限不足的调用方获取值类型的实例。 您必须确保值类型的实例在其默认状态下不公开敏感信息，并且不能以有害方式使用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果任何调用方可以在默认状态下获取值类型的实例，而不会对安全性造成威胁，则可以禁止显示此规则发出的警告。

## <a name="example-1"></a>示例 1

下面的示例显示一个库，其中包含违反此规则的值类型。 `StructureManager`类型假定传递值类型的实例的调用方有权创建或访问该实例。

[!code-csharp[FxCop.Security.DemandOnValueType#1](../code-quality/codesnippet/CSharp/ca2108-review-declarative-security-on-value-types_1.cs)]

## <a name="example-2"></a>示例 2

以下应用程序演示了库的漏洞。

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
