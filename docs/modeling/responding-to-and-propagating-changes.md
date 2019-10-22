---
title: 响应并传播更改
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 537f41418b6e66055acd9bedd5f0ccf4e01db524
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660328"
---
# <a name="respond-to-and-propagate-changes"></a>响应并传播更改

创建、删除或更新元素时，您可以编写将更改传播到模型的其他部分的代码，或者编写为外部资源（如文件、数据库或其他组件）的代码。

## <a name="reference"></a>参考

作为指导原则，请按以下顺序考虑这些技术：

|采用|方案|更多相关信息|
|-|-|-|
|定义计算域属性。|值由模型中的其他属性计算的域属性。 例如，价格是相关元素的价格之和。|[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)|
|定义自定义存储域属性。|存储在模型的其他部分或外部的域属性。 例如，可以将表达式字符串分析为模型中的树。|[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)|
|重写更改处理程序，如 OnValueChanging 和 OnDeleting|使不同元素保持同步，并使外部值与模型保持同步。<br /><br /> 将值约束为定义的范围。<br /><br /> 紧跟在属性值和其他更改之前调用。 可以通过引发异常来终止更改。|[域属性值更改处理程序](../modeling/domain-property-value-change-handlers.md)|
|规则|可以定义在发生更改的事务结束之前，排队等待执行的规则。 它们不会在撤消或重做时执行。 使用它们来使存储区的一部分与另一部分保持同步。|[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)|
|存储事件|建模应用商店提供事件通知，如添加或删除元素或链接，或更改属性的值。 此事件也会在撤消和重做时执行。 使用存储事件更新不在存储中的值。|[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)|
|.NET 事件|形状具有响应鼠标单击和其他笔势的事件处理程序。 必须为每个对象注册这些事件。 注册通常是在 InitializeInstanceResources 的重写中完成的，并且必须为每个元素完成。<br /><br /> 这些事件通常发生在事务外。|[如何：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)|
|边界规则|边界规则专用于限制形状的边界。|[BoundsRules 约束形状位置和大小](/visualstudio/modeling/boundsrules-constrain-shape-location-and-size?view=vs-2015)|
|选择规则|选择规则专门限制用户可以选择的内容。|[如何：访问和约束当前所选内容](../modeling/how-to-access-and-constrain-the-current-selection.md)|
|OnAssocatedPropertyChanged|使用形状和连接线的功能（如阴影、箭头、颜色、线条宽度和样式）指示模型元素的状态。|[更新形状和连接线以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)|

## <a name="compare-rules-and-store-events"></a>比较规则和存储事件

更改通告、规则和事件会在模型中发生更改时运行。

规则通常应用于发生更改的结束事务，并在提交事务中的更改后应用事件。

使用存储事件将模型与存储外部的对象进行同步，并使用规则来保持存储中的一致性。

- **创建自定义规则**您可以创建自定义规则作为抽象规则的派生类。 还必须通知框架有关自定义规则。 有关详细信息，请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。

- **订阅事件**在订阅事件之前，请创建事件处理程序和委托。 然后使用 <xref:Microsoft.VisualStudio.Modeling.Store.EventManagerDirectory%2A>property 订阅该事件。 有关详细信息，请参阅[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

- **撤消更改**撤消事务时，将引发事件，但不会应用规则。 如果规则更改了某个值，而您撤消了该更改，则在撤消操作期间，该值将重置为原始值。 引发事件时，必须手动将值更改回其原始值。 若要了解有关事务和撤消的详细信息，请参阅[如何：使用事务更新模型](../modeling/how-to-use-transactions-to-update-the-model.md)。

- **将事件参数传递到规则和事件**事件和规则都传递有 `EventArgs` 参数，该参数包含有关模型如何更改的信息。

## <a name="see-also"></a>请参阅

- [如何：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
