---
title: 控制颜色、 线型和其他形状属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: c06d0066-24aa-4c65-b91c-c2089b81ec8d
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: cff60ca7fc76563db73c4fc839688e0fba4ab975
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159647"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>控制颜色、线型和其他形状属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

某些形状属性如颜色可以公开 – 即，链接到形状的域属性。 其他人需要进行直接控制。  
  
## <a name="exposing-a-property"></a>公开属性  
 某些形状属性，如颜色可以链接到域属性的值。  
  
 在 DSL 定义中，选择形状、 连接符或关系图类。 在其上下文菜单，选择**公开添加**，然后选择所需的属性，如填充颜色。  
  
 现在，该形状具有域设置的属性，您可以在程序代码中或以用户身份。  
  
## <a name="dynamically-updating-an-exposed-property"></a>动态更新公开的属性  
 通常，你想要使依赖于另一个属性公开的属性。 例如，可能想要特定域属性时变为红色的形状小于零。 若要使此依赖项，创建[规则](../modeling/rules-propagate-changes-within-the-model.md)。 例如:  
  
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
