---
title: 自定义元素工具 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6dac48b6-db68-4bcd-8aa2-422c2ad5d28b
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b6b35bbb0592f7ec9f8defcd9d78dbba5a6a47a5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655011"
---
# <a name="customizing-element-tools"></a>自定义元素工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在某些 DSL 定义中，你将单个概念表示为一组元素。 例如，如果您创建一个模型，其中组件具有一组固定的端口，则您始终需要创建与其父组件相同的端口。 因此，您必须自定义元素创建工具，以便创建一组元素，而不是只创建一个元素。 若要实现此目的，你可以自定义元素创建工具的初始化方式。

 还可以重写将工具拖到关系图或元素上时会发生的情况。

## <a name="customizing-the-content-of-an-element-tool"></a>自定义元素工具的内容
 每个元素工具都存储 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> （EGP）的实例，该实例包含一个或多个模型元素和链接的序列化版本。 默认情况下，元素工具的 EGP 包含你为该工具指定的类的一个实例。 可以通过重写*YourLanguage* `ToolboxHelper.CreateElementToolPrototype` 来对此进行更改。 加载 DSL 包时将调用此方法。

 方法的参数是在 DSL 定义中指定的类的 ID。 当你感兴趣的类调用方法时，可以将额外的元素添加到 EGP 中。

 EGP 必须包括从一个主元素到子公司元素的嵌入链接。 它还可以包括引用链接。

 下面的示例创建一个主元素和两个嵌入元素。 主类称为电阻器，它具有两个到名为 Terminal 的元素的嵌入关系。 嵌入角色属性的名称为 Terminal1 和 Terminal2，两者的重数为 1 ..1。

```
using Microsoft.VisualStudio.Modeling; ...
public partial class CircuitDiagramToolboxHelper
{
  protected override ElementGroupPrototype    CreateElementToolPrototype(Store store, Guid domainClassId)
  {
    // A case for each tool to customize:
    if (domainClassId == Resistor.DomainClassId)
    {
      // Set up the prototype elements and links:
      Resistor resistor = new Resistor(store);
      resistor.Terminal1 = new Terminal(store);
      resistor.Terminal2 = new Terminal(store);
      resistor.Terminal1.Name = "T1"; // embedding
      resistor.Terminal2.Name = "T2"; // embedding
      // We could also set up reference links.

      // Create an element group prototype for the toolbox:
      ElementGroup egp = new ElementGroup(store.DefaultPartition);
      egp.AddGraph(resistor, true);
      // We do not have to explicitly include embedded children.
      return egp.CreatePrototype();
    }
    // Element tools for other classes:
    else
      return base.CreateElementToolPrototype(store, domainClassId);
  }
}
```

## <a name="see-also"></a>请参阅
 [自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)
