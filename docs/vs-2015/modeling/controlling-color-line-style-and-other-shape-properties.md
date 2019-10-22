---
title: 控制颜色、线型和其他形状属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: c06d0066-24aa-4c65-b91c-c2089b81ec8d
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d5d296f5ab3f5c584558b373b57c175fb2bacef4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667856"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>控制颜色、线型和其他形状属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

某些形状属性（如颜色）可以是 "公开的" 的，也就是说，链接到形状的域属性。 其他人必须直接控制。

## <a name="exposing-a-property"></a>公开属性
 某些形状属性（如颜色）可以链接到域属性的值。

 在 DSL 定义中，选择形状、连接符或关系图类。 在其上下文菜单上，选择 "添加" "**公开**"，然后选择所需的属性，例如 "填充颜色"。

 该形状现在具有可在程序代码或用户中设置的域属性。

## <a name="dynamically-updating-an-exposed-property"></a>动态更新公开的属性
 通常，您需要使公开的属性依赖于另一个属性。 例如，如果特定域属性小于零，则您可能希望形状变成红色。 若要生成此依赖项，请创建一个[规则](../modeling/rules-propagate-changes-within-the-model.md)。 例如:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
namespace ExampleNamespace
{
 // Attribute associates the rule with class:
 [RuleOn(typeof(CarShape), FireTime = TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class CarShapeAddRule : AddRule
 {
 // Override the abstract method:
 public override void ElementAdded(ElementAddedEventArgs e)
 {
 base.ElementAdded(e);
 CarShape shape = e.ModelElement as CarShape;
 Store store = shape.Store;
 // Ignore this call if we're currently loading a model:
 if (store.TransactionManager.CurrentTransaction.IsSerializing)
  return;
 Car car = shape.ModelElement as Car;
 // Code here propagates change as required - for example:
 shape.FillColor = car.Somebool ? System.Drawing.Color.Red : System.Drawing.Color.Green;
 }
}
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
 protected override Type[] GetCustomDomainModelTypes()
 {
  List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
  types.Add(typeof(CarShapeAddRule));
  // If you add more rules, list them here.
  return types.ToArray();
 }
 }
}
```
