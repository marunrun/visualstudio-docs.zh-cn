---
title: 重写和扩展生成的类
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, providing overridable classes
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c3374f67f4fba11543e3dbbca47fef621dd2e714
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595886"
---
# <a name="override-and-extend-the-generated-classes"></a>重写和扩展生成的类

DSL 定义是一种平台，可在该平台上构建一组基于域特定语言的强大工具。 可以通过重写和扩展从 DSL 定义生成的类来进行许多扩展和适应。 这些类不仅包括在 DSL 定义关系图中显式定义的域类，还包括定义工具箱、资源管理器、序列化等的其他类。

## <a name="extensibility-mechanisms"></a>扩展性机制

提供了几种机制来扩展生成的代码。

### <a name="override-methods-in-a-partial-class"></a>重写分部类中的方法

分部类定义允许在多个位置定义一个类。 这使您可以将生成的代码与自己编写的代码分开。 在手动编写的代码中，你可以重写由生成的代码继承的类。

例如，如果在 DSL 定义中定义了一个名为 `Book`的域类，则可以编写自定义代码来添加重写方法：

```csharp
public partial class Book
{
   protected override void OnDeleting()
   {
      MessageBox.Show("Deleting book " + this.Title);
      base.OnDeleting();
   }
}
```

> [!NOTE]
> 若要重写生成的类中的方法，请始终在与生成的文件分离的文件中编写代码。 通常，该文件包含在名为 CustomCode 的文件夹中。 如果对生成的代码进行了更改，则在重新生成 DSL 定义中的代码时，它们将丢失。

若要发现可以重写的方法，请在类中键入**override** ，后跟一个空格。 IntelliSense 工具提示将告诉您哪些方法可以重写。

### <a name="double-derived-classes"></a>双派生类

生成的类中的大多数方法都继承自建模命名空间中的一组固定的类。 但是，某些方法是在生成的代码中定义的。 通常，这意味着你不能重写它们;在一个分部类中，不能重写在同一类的另一个分部定义中定义的方法。

尽管如此，你可以通过设置域类的**生成双派生**标志来重写这些方法。 这会生成两个类，一个是另一个类的抽象基类。 所有方法和属性定义都在基类中，只有构造函数在派生类中。

例如，在示例库 dsl 中，`CirculationBook` 域类的 `Generates``Double Derived` 属性设置为 "`true`"。 为该域类生成的代码包含两个类：

- `CirculationBookBase`，它是一个抽象的，其中包含所有方法和属性。

- `CirculationBook`，它派生自 `CirculationBookBase`。 除了其构造函数，它是空的。

若要重写任何方法，请创建派生类的分部定义，如 `CirculationBook`。 您可以重写生成的方法和从建模框架继承的方法。

此方法可用于所有类型的元素，包括模型元素、关系、形状、关系图和连接线。 您还可以重写其他生成的类的方法。 某些生成的类（如 ToolboxHelper）始终是双重派生的。

### <a name="custom-constructors"></a>自定义构造函数

不能重写构造函数。 即使在双向派生类中，构造函数也必须位于派生类中。

如果要提供自己的构造函数，可以通过在 DSL 定义中设置域类 `Has Custom Constructor` 来执行此操作。 单击 "**转换所有模板**" 时，生成的代码将不包含该类的构造函数。 它将包括对缺少的构造函数的调用。 生成解决方案时，这会导致错误报告。 双击错误报告以查看生成的代码中的注释，该注释说明了应提供的内容。

在独立于生成的文件的文件中编写分部类定义，并提供构造函数。

### <a name="flagged-extension-points"></a>标记的扩展点

标记的扩展点是 DSL 定义中的一个位置，你可以在其中设置属性或复选框，以指示你将提供自定义方法。 自定义构造函数是一个示例。 其他示例包括将域属性的 `Kind` 设置为计算或自定义存储，或在连接生成器中设置**为自定义**标志。

在每种情况下，设置标志并重新生成代码时，将导致生成错误。 双击错误以查看说明必须提供的注释。

### <a name="rules"></a>规则

使用事务管理器可以定义在发生指定事件的事务结束之前运行的规则，如属性更改。 规则通常用于维护存储区中不同元素之间的 synchronism。 例如，规则用于确保关系图显示模型的当前状态。

规则是基于每个类定义的，因此你不必具有为每个对象注册规则的代码。 有关详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。

### <a name="store-events"></a>存储事件

建模存储提供了一种事件机制，可用于在存储中侦听特定类型的更改，包括添加和删除元素、更改属性值等。 事件处理程序在进行更改的事务结束后调用。 通常，这些事件用于更新存储外部的资源。

### <a name="net-events"></a>.NET 事件

您可以订阅一些形状上的事件。 例如，您可以侦听形状上的鼠标单击。 您必须编写订阅每个对象的事件的代码。 可以在 InitializeInstanceResources （）的重写中编写此代码。

某些事件在在 mapcontrol.shapefields 上生成，用于在形状上绘制修饰器。 有关示例，请参阅[如何：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)。

这些事件通常不在事务中发生。 如果要在存储中进行更改，则应创建一个事务。
