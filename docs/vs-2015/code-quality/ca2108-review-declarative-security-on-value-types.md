---
title: CA2108:检查有关值类型的声明性安全 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f6a17bf57f00923cfd31bd477f211ba66169672a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687370"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108:检查有关值类型的声明性安全
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 公共或受保护值类型受[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)或[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)。

## <a name="rule-description"></a>规则说明
 分配和其他构造函数执行前通过其默认构造函数初始化值类型。 如果值类型保护的 Demand 或 LinkDemand，并且调用方没有权限而不满足安全检查，任何构造函数的默认值将失败，并且将引发安全异常。 未释放的值类型;它将继续处于其默认构造函数设置的状态。 不要假定将传递值类型的实例的调用方有权创建或访问该实例。

## <a name="how-to-fix-violations"></a>如何解决冲突
 除非从类型中删除的安全检查和使用方法级别的安全检查在其原位置，则无法修复该规则的冲突。 请注意，这种方式解决冲突不会阻止调用方与从获取值类型的实例的权限不足。 您必须确保中默认状态下，值类型的实例不会公开敏感信息，并且不能以有害方式使用。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果任何调用方可以获得在其默认状态的值类型的实例，而不会造成安全风险，可以禁止显示此规则的警告。

## <a name="example"></a>示例
 下面的示例演示一个库，包含与此规则冲突的值类型。 请注意，`StructureManager`类型假定将传递值类型的实例的调用方有权创建或访问该实例。

 [!code-csharp[FxCop.Security.DemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.DemandOnValueType/cs/FxCop.Security.DemandOnValueType.cs#1)]

## <a name="example"></a>示例
 以下应用程序演示库的弱点。

 [!code-csharp[FxCop.Security.TestDemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestDemandOnValueType/cs/FxCop.Security.TestDemandOnValueType.cs#1)]

 本示例生成以下输出。

 **结构自定义构造函数：请求失败。** 
**新值 SecuredTypeStructure 100 100**
**新值 SecuredTypeStructure 200 200**
## <a name="see-also"></a>请参阅
 [链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[数据和建模](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
