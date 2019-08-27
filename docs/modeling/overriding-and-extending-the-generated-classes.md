---
title: 重写和扩展生成的类
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, providing overridable classes
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9aa4f39fb54617ae1dbf048a1e13f009c8df5185
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814232"
---
# <a name="override-and-extend-the-generated-classes"></a>重写和扩展生成的类

DSL 定义是一个平台，你可以在其生成一组强大的基于域特定语言的工具。 许多扩展和适应可以通过重写和扩展从 DSL 定义生成的类。 这些类包括不只是在 DSL 定义关系图中，显式定义的域类，但还定义工具箱、 资源管理器中，序列化，等其他类。

## <a name="extensibility-mechanisms"></a>扩展性机制

提供了多种机制，以使你可以扩展生成的代码。

### <a name="override-methods-in-a-partial-class"></a>分部类中重写方法

分部类定义允许用于在多个位置中定义的类。 这允许从你自己编写的代码分离生成的代码。 在您手动编写的代码，可以重写由生成的代码继承的类。

例如，如果在 DSL 定义中定义一个名为的域类`Book`，您可以编写添加重写方法的自定义代码：

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
> 若要重写方法生成的类中，始终从生成的文件分隔的文件中编写代码。 通常情况下，该文件包含在名为独特的文件夹中。 如果对生成的代码进行更改，它们将会丢失时重新生成 DSL 定义中的代码。

若要发现哪些可以重写的方法，请键入**重写**在类中，有一个空格。 IntelliSense 工具提示将告诉您哪些方法可以重写。

### <a name="double-derived-classes"></a>双派生的类

从一组固定的建模命名空间中类继承的大多数方法中生成的类。 但是，某些方法生成的代码中定义。 通常，这意味着您不能重写它们。不能重写在一个分部类中的同一个类的另一个分部定义中定义的方法。

不过，通过设置重写这些方法**生成双派生**域类的标志。 要生成此会导致两个类，另一个抽象基类的那个。 所有方法和属性定义在基的类中，而只有构造函数是在派生类中。

例如，在示例 Library.dsl，`CirculationBook`域类具有`Generates``Double Derived`属性设置为`true`。 为此域类生成的代码包含两个类：

- `CirculationBookBase`它是一个抽象，它包含所有方法和属性。

- `CirculationBook`它派生自`CirculationBookBase`。 它是空的但其构造函数除外。

若要重写任何方法，您创建派生类的分部定义如`CirculationBook`。 您可以重写生成的方法和从建模 framework 继承的方法。

与所有类型的元素，包括模型元素、 关系、 形状、 图和连接器，可以使用此方法。 此外可以重写的其他生成的类的方法。 某些生成如 ToolboxHelper 始终是双派生的类。

### <a name="custom-constructors"></a>自定义构造函数

您不能重写构造函数。 甚至在双派生类中，构造函数必须在派生类中。

如果你想要提供自己的构造函数，可以执行此操作通过设置`Has Custom Constructor`为 DSL 定义中的域类。 当您单击**转换所有模板**，生成的代码将不包括此类的构造函数。 它包含对缺少构造函数的调用。 生成解决方案时，这会导致错误报告。 双击错误报告以查看生成的代码，您应提供说明中的注释。

在独立于生成的文件的文件中编写分部类定义，并提供构造函数。

### <a name="flagged-extension-points"></a>已标记的扩展点

已标记的扩展点是在 DSL 定义中，你可以设置的属性或一个复选框以指示您将在提供的自定义方法的地方。 自定义构造函数是一个示例。 其他示例包括设置`Kind`到计算或自定义存储或设置域属性的**为自定义**连接生成器中的标志。

每种情况下，当您设置标志并重新生成代码，将导致生成错误。 双击错误以了解说明你需要提供的注释。

### <a name="rules"></a>规则

事务管理器，可定义在其中指定已发生的事件，例如在属性中更改的事务结束之前运行的规则。 规则通常用于维护 synchronism 存储区中的不同元素之间。 例如，规则用于确保关系图显示模型的当前状态。

基于每个类定义规则，以便不需要有代码用于注册的每个对象的规则。 有关详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。

### <a name="store-events"></a>存储事件

建模存储提供了事件机制，可用于侦听的特定类型的商店的应用，包括添加和删除的元素，对属性值的更改中的更改和其他操作。 后已进行了更改的事务结束调用事件处理程序。 通常情况下，这些事件用于更新在存储外的资源。

### <a name="net-events"></a>.NET 事件

您可以订阅某些事件在形状上。 例如，可以侦听形状上的鼠标单击。 您必须编写订阅的每个对象事件的代码。 此代码可以用 InitializeInstanceResources() 的重写。

ShapeFields，用于绘制的形状上的修饰器上生成一些事件。 有关示例，请参见 [如何：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)。

这些事件通常不会发生在事务内。 如果你想要在应用商店中进行更改，应创建一个事务。