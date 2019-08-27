---
title: 控制颜色、线型和其他形状属性
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1783ecf3b30207838d93fdb9cda93e3ed7e232c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62422920"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>控制颜色、线型和其他形状属性

某些形状属性，如颜色可以公开。 也就是说，属性可以链接到形状的域属性。 其他人需要进行直接控制。

## <a name="exposing-a-property"></a>公开属性
 某些形状属性，如颜色可以链接到域属性的值。

 在 DSL 定义中，选择形状、 连接符或关系图类。 其右键单击菜单上，选择**公开添加**，然后选择所需的属性，如填充颜色。

 现在，该形状具有域设置的属性，您可以在程序代码中或以用户身份。

## <a name="dynamically-updating-an-exposed-property"></a>动态更新公开的属性
 通常，你想要使依赖于另一个属性公开的属性。 例如，可能想要特定域属性时变为红色的形状小于零。 若要使此依赖项，创建[规则](../modeling/rules-propagate-changes-within-the-model.md)。 例如：

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