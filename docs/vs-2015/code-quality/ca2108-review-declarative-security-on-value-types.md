---
title: CA2108：查看值类型的声明性安全 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
helpviewer_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
ms.assetid: d62bffdd-3826-4d52-a708-1c646c5d48c2
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 03918353b66c36698b5d17b332da052b6d95c87a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544386"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108:检查有关值类型的声明性安全
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|Category|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 公共或受保护值类型受[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)或[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)保护。

## <a name="rule-description"></a>规则描述
 值类型在其他构造函数执行之前由其默认构造函数进行分配和初始化。 如果值类型受需求或 LinkDemand 的保护，并且调用方没有满足安全检查要求的权限，则除默认值以外的任何构造函数都将失败，并将引发安全异常。 未解除分配值类型;它保留为其默认构造函数设置的状态。 不要假设传递值类型的实例的调用方有权创建或访问该实例。

## <a name="how-to-fix-violations"></a>如何解决冲突
 除非从类型中删除安全检查并在其位置使用方法级安全检查，否则不能修复此规则的冲突。 请注意，以这种方式修复冲突不会阻止权限不足的调用方获取值类型的实例。 您必须确保值类型的实例在其默认状态下不公开敏感信息，并且不能以有害方式使用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果任何调用方可以在默认状态下获取值类型的实例，而不会对安全性造成威胁，则可以禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示一个库，其中包含违反此规则的值类型。 请注意，该 `StructureManager` 类型假定传递值类型的实例的调用方有权创建或访问该实例。

 [!code-csharp[FxCop.Security.DemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.DemandOnValueType/cs/FxCop.Security.DemandOnValueType.cs#1)]

## <a name="example"></a>示例
 以下应用程序演示了库的漏洞。

 [!code-csharp[FxCop.Security.TestDemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestDemandOnValueType/cs/FxCop.Security.TestDemandOnValueType.cs#1)]

 本示例生成以下输出。

 **结构自定义构造函数：请求失败。** 
**新值 SecuredTypeStructure 100 100** 
**新值 SecuredTypeStructure 200 200**
## <a name="see-also"></a>另请参阅
 [链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
