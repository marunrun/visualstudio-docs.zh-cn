---
title: 更新形状和连接线以反映模型
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5b4c0c88e9e096836e32ce427ff78cc94f5d1f72
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62906984"
---
# <a name="update-shapes-and-connectors-to-reflect-the-model"></a>更新形状和连接线以反映模型

在 Visual Studio 中特定于域的语言中，可以使形状的外观反映基础模型的状态。

本主题中的代码示例应添加到`.cs`文件中您`Dsl`项目。 你需要每个文件中的这些语句：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
```

## <a name="set-shape-map-properties-to-control-the-visibility-of-a-decorator"></a>设置形状映射的属性以控制修饰器的可见性

您可以控制修饰器的可见性，而无需编写程序代码中，通过在 DSL 定义中配置形状和域类之间的映射。 有关详细信息，请参阅[如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)。

## <a name="expose-the-color-and-style-of-a-shape-as-properties"></a>将作为属性公开的颜色和形状的样式

在 DSL 定义中，右键单击形状类、 指向**添加公开**，然后单击某一项诸如**填充颜色**。

现在，该形状具有域设置的属性，您可以在程序代码中或以用户身份。 例如，若要将其设置的命令或规则的程序代码中，可以编写：

`shape.FillColor = System.Drawing.Color.Red;`

如果你想要使属性变量仅在程序控制，而不是由用户，选择新的域属性，如**填充颜色**DSL 定义关系图中。 然后，在属性窗口中设置**是可浏览**到`false`，或者设置**是 UI Readonly**到`true`。

## <a name="define-change-rules-to-make-color-style-or-location-depend-on-model-element-properties"></a>定义更改规则，以使颜色、 样式或位置取决于模型元素属性
 可以定义规则，更新依赖于模型的其他部分的形状的外观。 例如，您可以更新其依赖于模型元素的属性的形状的颜色的模型元素上定义更改规则。 有关更改规则的详细信息，请参阅[规则将传播的更改中的模式](../modeling/rules-propagate-changes-within-the-model.md)。

 应使用规则仅用于更新的存储中维护的属性，因为规则不会在执行撤消命令时调用。 这不包括某些图形功能，例如大小和形状的可见性。 若要更新形状的这些功能，请参阅[更新应用商店的非图形功能](#OnAssociatedProperty)。

 下面的示例假定你具有公开`FillColor`作为域属性上一节中所述。

```csharp
[RuleOn(typeof(ExampleElement))]
  class ExampleElementPropertyRule : ChangeRule
  {
    public override void ElementPropertyChanged(ElementPropertyChangedEventArgs e)
    {
      base.ElementPropertyChanged(e);
      ExampleElement element = e.ModelElement as ExampleElement;
      // The rule is called for every property that is updated.
      // Therefore, verify which property changed:
      if (e.DomainProperty.Id == ExampleElement.NameDomainPropertyId)
      {
        // There is usually only one shape:
        foreach (PresentationElement pel in PresentationViewsSubject.GetPresentation(element))
        {
          ExampleShape shape = pel as ExampleShape;
          // Replace this with a useful condition:
          shape.FillColor = element.Name.EndsWith("3")
                     ? System.Drawing.Color.Red : System.Drawing.Color.Green;
        }
      }
    }
  }
  // The rule must be registered:
  public partial class OnAssociatedPropertyExptDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(ExampleElementPropertyRule));
      // If you add more rules, list them here.
      return types.ToArray();
    }
  }
```

## <a name="use-onchildconfigured-to-initialize-a-shapes-properties"></a>使用 OnChildConfigured 初始化形状的属性

若要设置形状的属性，首次创建、 重写`OnChildConfigured()`在关系图类的分部定义中。 在 DSL 定义中，指定的关系图类和生成的代码处于**Dsl\Generated Code\Diagram.cs**。 例如：

```csharp
partial class MyLanguageDiagram
{
  protected override void OnChildConfigured(ShapeElement child, bool childWasPlaced, bool createdDuringViewFixup)
  {
    base.OnChildConfigured(child, childWasPlaced, createdDuringViewFixup);
    ExampleShape shape = child as ExampleShape;
    if (shape != null)
    {
      if (!createdDuringViewFixup) return; // Ignore load from file.
      ExampleElement element = shape.ModelElement as ExampleElement;
      // Replace with a useful condition:
      shape.FillColor = element.Name.EndsWith("3")
          ? System.Drawing.Color.Red : System.Drawing.Color.Green;
    }
    // else deal with other types of shapes and connectors.
  }
}
```

可以使用此方法，为域属性和非应用商店功能，例如形状的大小。

## <a name="OnAssociatedProperty"></a> 使用 AssociateValueWith() 更新形状的其他功能

形状，例如是否具有阴影或连接器的箭头样式的某些功能没有公开为域属性的功能的内置方法。  此类功能的更改不受控制的事务系统中。 因此，不适合更新这些使用规则，因为当用户执行撤消命令不会调用规则。

相反，可以通过使用更新此类功能<xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnAssociatedPropertyChanged%2A>。 在以下示例中，由连接器显示在关系中的域属性的值控制连接线的箭头样式：

```csharp
public partial class ArrowConnector // My connector class.
{
    /// <summary>
    /// Called whenever a registered property changes in the associated model element.
    /// </summary>
    /// <param name="e"></param>
    protected override void OnAssociatedPropertyChanged(VisualStudio.Modeling.Diagrams.PropertyChangedEventArgs e)
    {
      base.OnAssociatedPropertyChanged(e);
      // Can be called for any property change. Therefore,
      // Verify that this is the property we're interested in:
      if ("IsDirected".Equals(e.PropertyName))
      {
        if (e.NewValue.Equals(true))
        { // Update the shape's built-in Decorator feature:
          this.DecoratorTo = LinkDecorator.DecoratorEmptyArrow;
        }
        else
        {
          this.DecoratorTo = null; // No arrowhead.
        }
      }
    }

    // OnAssociatedPropertyChanged is called only for properties
    // that have been registered using AssociateValueWith().
    // InitializeResources is a convenient place to call this.
    // This method is invoked only once per class, even though
    // it is an instance method.
    protected override void InitializeResources(StyleSet classStyleSet)
    {
      base.InitializeResources(classStyleSet);
      AssociateValueWith(this.Store, Wire.IsDirectedDomainPropertyId);
      // Add other properties here.
    }
}
```

`AssociateValueWith()` 应调用一次为每个你想要注册的域属性。 已调用后，将调用对指定的属性的任何更改`OnAssociatedPropertyChanged()`中存在该属性的模型元素的所有形状。

不需要调用`AssociateValueWith()`每个实例。 尽管 InitializeResources 是实例方法，但它是只调用一次为每个形状类。
