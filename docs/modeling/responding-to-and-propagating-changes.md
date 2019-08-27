---
title: 响应并传播更改
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a1d58ede1370976147b33cf1246f8b582adb3c5b
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476605"
---
# <a name="respond-to-and-propagate-changes"></a>响应并传播更改

元素是创建、 删除或更新时，您可以编写将传播到模型，其他部件或外部资源，例如文件、 数据库或其他组件的更改的代码。

## <a name="reference"></a>参考

作为一般准则，请考虑按以下顺序这些技术：

|技术|方案|更多相关信息|
|-|-|-|
|定义一个计算域属性。|域属性，其值计算从模型中的其他属性。 例如，其价格相关元素的价格总和。|[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)|
|定义自定义存储域属性。|存储在其他部分的模型或外部域属性。 例如，无法解析为模型中的树的表达式字符串。|[计算的和自定义的存储属性](../modeling/calculated-and-custom-storage-properties.md)|
|重写 OnValueChanging 和 OnDeleting 等更改处理程序|使不同的元素保持同步，并保留外部值与模型同步。<br /><br /> 约束定义的范围内的值。<br /><br /> 属性值和其他更改立即之前或之后调用。 可以通过引发异常来终止此更改。|[域属性值更改处理程序](../modeling/domain-property-value-change-handlers.md)|
|规则|可以定义将排队等待发生更改的事务结束前，只需执行的规则。 它们不会撤消或重做上执行。 使用它们来使存储区的一部分与另一个同步。|[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)|
|存储事件|建模存储提供通知的事件，例如添加或删除的元素或链接，或更改属性的值。 该事件还会执行撤消和重做。 使用存储事件更新不在存储中的值。|[事件处理程序在模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)|
|.NET 事件|形状具有响应鼠标单击和其他手势的事件处理程序。 您必须注册这些事件的每个对象。 注册通常是 InitializeInstanceResources，重写中，并且必须执行的每个元素。<br /><br /> 这些事件通常发生事务之外。|[如何：在形状或修饰器上截断单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)|
|边界规则|边界规则专门用于约束形状的边界。|[BoundsRules 约束形状位置和大小](/visualstudio/modeling/boundsrules-constrain-shape-location-and-size?view=vs-2015)|
|选择规则|选择规则专门约束用户可以选择。|[如何：访问和约束当前选定内容](../modeling/how-to-access-and-constrain-the-current-selection.md)|
|OnAssocatedPropertyChanged|指示使用的形状和连接线如卷影、 箭头、 颜色和线条宽度和样式功能的模型元素的状态。|[更新形状和连接线以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)|

## <a name="compare-rules-and-store-events"></a>将规则进行比较和存储事件

在模型中发生更改时运行更改通告程序、 规则和事件。

在更改已发生的最终事务通常应用规则，并提交在事务中的更改后应用的事件。

使用存储事件以同步模型与应用商店和规则，以保持在存储中的一致性之外的对象。

- **创建自定义规则**作为抽象规则从派生类中创建自定义规则。 此外必须通知的自定义规则的相关框架。 有关详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。

- **订阅事件**可以订阅事件之前，请创建一个事件处理程序和委托。 然后，使用<xref:Microsoft.VisualStudio.Modeling.Store.EventManagerDirectory%2A>属性来订阅事件。 有关详细信息，请参阅[事件处理程序传播更改外部模型](../modeling/event-handlers-propagate-changes-outside-the-model.md)。

- **正在撤消更改**时撤销的事务，会引发事件，但不是会应用规则。 如果将值更改为一个规则，并且撤消所做的更改，值是重置为原始值在撤消操作过程。 当引发事件时，你必须手动更改回其原始值的值。 若要了解有关事务和撤消的详细信息，请参阅[如何：使用事务更新模型](../modeling/how-to-use-transactions-to-update-the-model.md)。

- **将事件自变量传递到规则和事件**这两个事件和传递规则`EventArgs`参数，其中包含有关如何信息的模型更改。

## <a name="see-also"></a>请参阅

- [如何：在形状或修饰器上截断单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)
- [编写代码以自定义特定于域的语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
