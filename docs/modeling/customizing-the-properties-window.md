---
title: 自定义“属性”窗口
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, Properties window
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 72e0a8393a65d4c0e1549a6617971b0adb8c1df7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72653967"
---
# <a name="customize-the-properties-window"></a>自定义属性窗口

你可以在 Visual Studio 中自定义域特定语言（DSL）的 "属性" 窗口的外观和行为。 在 DSL 定义中，为每个域类定义域属性。 默认情况下，当您在关系图上或在模型资源管理器中选择类的实例时，每个域属性都将列在 "属性" 窗口中。 这使你可以查看和编辑域属性的值，即使尚未将它们映射到关系图上的形状字段。

## <a name="names-descriptions-and-categories"></a>名称、说明和类别

**名称和显示名称**。 在定义域属性时，属性的显示名称是在运行时在 "属性" 窗口中显示的名称。 与此相反，当您编写程序代码以更新属性时，将使用该名称。 名称必须是正确的 CLR 字母数字名称，但显示名称可以包含空格。

在 DSL 定义中设置某个属性的名称时，其显示名称将自动设置为该名称的副本。 如果编写 Pascal 大小写名称（如 "FuelGauge"），则显示名称将自动包含一个空格： "燃料仪表"。 但是，你可以将显示名称显式设置为另一个值。

**说明**。 域属性的说明出现在两个位置：

- 当用户选择属性时，在 "属性" 窗口的底部。 可以使用它向用户说明属性表示的内容。

- 在生成的程序代码中。 如果使用文档工具来提取 API 文档，它将在 API 中显示为此属性的说明。

**Category**。 类别是属性窗口中的标题。

## <a name="expose-style-features"></a>公开样式功能

可以将图形元素的某些动态功能表示或*公开*为域属性。 以这种方式公开的功能可以由用户更新，并且可以更轻松地通过程序代码进行更新。

右键单击 DSL 定义中的形状类，指向 "添加" "**添加**"，然后选择一项功能。

在形状上，可以公开**FillColor**、 **OutlineColor**、 **TextColor**、 **OutlineDashStyle**、 **OutlineThickness**和**FillGradientMode**属性。 在连接器上，可以 `,`**TextColor**、 **DashStyle**和**宽窄**属性公开**颜色**。 在关系图上，可以公开**FillColor**和**TextColor**属性。

## <a name="forwarding-display-properties-of-related-elements"></a>转发：显示相关元素的属性

当 DSL 的用户选择模型中的元素时，该元素的属性将显示在 "属性" 窗口中。 但是，还可以显示指定相关元素的属性。 如果您定义了一组一起工作的元素，这会很有用。 例如，你可以定义一个主元素和一个可选的插件元素。 如果将主元素映射到某一形状，而另一个元素不是，则可以查看它们的所有属性，就好像它们位于一个元素上一样。

这种效果命名为*属性转发*，并且在几种情况下会自动发生。 在其他情况下，可以通过定义域类型描述符来实现属性转发。

### <a name="default-property-forwarding-cases"></a>默认属性转发事例

当用户在资源管理器中选择形状或连接符或元素时，以下属性将显示在属性窗口中：

- 在模型元素的域类上定义的域属性，包括基类中定义的属性。 例外情况是你为其设置**了可浏览**`False` 的域属性。

- 通过具有重数为 0 ..1 的关系链接的元素的名称。 这提供了一种方便的方法来查看链接的元素，即使您没有为关系定义连接器映射也是如此。

- 针对元素的嵌入关系的域属性。 由于嵌入关系通常不会显式显示，因此用户可以查看其属性。

- 在选定的形状或连接线上定义的域属性。

### <a name="add-property-forwarding"></a>添加属性转发

若要转发属性，请定义域类型描述符。 如果两个域类之间存在域关系，则可以使用域类型描述符将第一个类中的域属性设置为第二个域类中的域属性的值。 例如，如果您有一个**book**域类和一个**Author**域类之间的关系，则可以使用域类型描述符使该书**作者**的**Name**属性属性窗口在用户选择书籍。

> [!NOTE]
> 属性转发只会影响用户编辑模型时的属性窗口。 它不会在接收类中定义域属性。 如果要在 DSL 定义或程序代码的其他部分访问转发的域属性，则必须访问转发元素。

以下过程假定已创建 DSL。 前几个步骤汇总了先决条件。

#### <a name="forward-a-property-from-another-element"></a>从另一个元素转发属性

1. 创建一个 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 解决方案，该解决方案至少包含两个类，在此示例中称为**书籍**和**作者**。 **本书**和**Author**之间应有一种类型的关系。

    源角色的重数（**本书**端角色）应为 0 ..1 或 1 ..1，以便每**本书**都有一个**作者**。

2. 在 " **DSL 资源管理器**" 中，右键单击**Book**域类，然后单击 "**添加新 DomainTypeDescriptor**"。

    自定义**类型描述符**节点下将显示名为**的自定义属性描述符的路径**。

3. 右键单击 "**自定义类型描述符**" 节点，然后单击 "**添加新 PropertyPath**"。

    新属性路径出现在 "**自定义属性描述符**" 节点的路径下。

4. 选择新的属性路径，然后在 "**属性**" 窗口中，将 "**路径**" 设置为相应模型元素的路径。

    通过单击此属性右侧的向下箭头，可以在树视图中编辑路径。 有关域路径的详细信息，请参阅[域路径语法](../modeling/domain-path-syntax.md)。 编辑后，路径应类似于**BookReferencesAuthor/！作者**。

5. 将**属性**设置为**Author**的**Name**域属性。

6. 将**显示名称**设置为**作者名称**。

7. 转换所有模板，生成并运行 DSL。

8. 在模型关系图中，创建一本书和一个作者，并使用引用关系进行链接。 选择 "书籍" 元素，然后在 "属性窗口除了书籍的属性之外，还应看到" 作者姓名 "。 更改链接的作者的名称，或将此书籍链接到其他作者，并观察该书籍的作者姓名是否更改。

## <a name="custom-property-editors"></a>自定义属性编辑器

"属性" 窗口为每个域属性的类型提供了相应的默认编辑体验。 例如，对于枚举类型，用户将看到一个下拉列表，对于数值属性，用户可以输入数字。 这仅适用于内置类型。 如果指定外部类型，则用户将能够看到该属性的值，但不能对其进行编辑。

不过，你可以指定以下编辑器和类型：

1. 与标准类型一起使用的另一个编辑器。 例如，可以为字符串属性指定文件路径编辑器。

2. 域属性的外部类型和其编辑器。

3. .NET 编辑器（如文件路径编辑器），也可以创建自己的自定义属性编辑器。

   外部类型与类型（如 String）之间的转换，该类型具有默认编辑器。

   在 DSL 中，*外部类型*是任何不属于简单类型（如布尔值或 Int32）或字符串的类型。

### <a name="define-a-domain-property-that-has-an-external-type"></a>定义具有外部类型的域属性

1. 在**解决方案资源管理器**中，在**Dsl**项目中添加对包含外部类型的程序集（DLL）的引用。

    该程序集可以是 .NET 程序集，也可以是您提供的程序集。

2. 将类型添加到 "**域类型**" 列表中，除非您已执行此操作。

   1. 打开 Dsldefinition.dsl，并在**Dsl 资源管理器**中右键单击根节点，然后单击 "**添加新的外部类型**"。

        新条目出现在 "**域类型**" 节点下。

       > [!WARNING]
       > 该菜单项在 DSL 根节点上，而不是 "**域类型**" 节点上。

   2. 在属性窗口中设置新类型的名称和命名空间。

3. 以常规方式向域类添加域属性。

    在属性窗口的 "**类型**" 字段的下拉列表中，选择 "外部" 类型。

   在此阶段，用户可以查看属性的值，但不能对其进行编辑。 将从 `ToString()` 函数获取显示的值。 您可以编写程序代码以设置属性的值，例如在命令或规则中。

### <a name="set-a-property-editor"></a>设置属性编辑器

将 CLR 特性添加到域属性，格式如下：

```csharp
[System.ComponentModel.Editor (
   typeof(AnEditor),
   typeof(System.Drawing.Design.UITypeEditor))]
```

您可以使用属性窗口中的**自定义特性**项设置属性的属性。

@No__t_0 的类型必须从第二个参数中指定的类型派生而来。 第二个参数应是 <xref:System.Drawing.Design.UITypeEditor> 或 <xref:System.ComponentModel.ComponentEditor>。 有关更多信息，请参见<xref:System.ComponentModel.EditorAttribute>。

您可以指定您自己的编辑器或 .NET 编辑器，如 <xref:System.Windows.Forms.Design.FileNameEditor> 或 <xref:System.Drawing.Design.ImageEditor>。 例如，使用下面的过程可以拥有一个属性，用户可以在其中输入文件名。

#### <a name="define-a-file-name-domain-property"></a>定义文件名域属性

1. 向 DSL 定义中的域类添加域属性。

2. 选择新属性。 在属性窗口的 "**自定义特性**" 字段中，输入以下属性。 若要输入此属性，请单击省略号 **[...]** ，并分别输入属性名称和参数：

    ```csharp
    [System.ComponentModel.Editor (
       typeof(System.Windows.Forms.Design.FileNameEditor)
       , typeof(System.Drawing.Design.UITypeEditor))]

    ```

3. 保留域属性的类型，其默认设置为 "**字符串**"。

4. 若要测试编辑器，请验证用户是否可以打开文件名编辑器来编辑域属性。

    1. 按 CTRL + F5 或 F5。 在调试解决方案中，打开测试文件。 创建域类的元素并将其选中。

    2. 在属性窗口中，选择 "域" 属性。 值字段显示省略号 **[...]** 。

    3. 单击省略号。 此时将显示一个文件对话框。 选择一个文件并关闭对话框。 文件路径现在为域属性的值。

### <a name="define-your-own-property-editor"></a>定义自己的属性编辑器

您可以定义自己的编辑器。 您可以通过此操作来允许用户编辑您定义的类型，或以特殊方式编辑标准类型。 例如，您可以允许用户输入表示公式的字符串。

通过编写派生自 <xref:System.Drawing.Design.UITypeEditor> 的类来定义编辑器。 你的类必须重写：

- <xref:System.Drawing.Design.UITypeEditor.EditValue%2A>，用于与用户交互并更新属性值。

- <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A>，指定编辑器是打开对话框还是提供下拉菜单。

还可以提供属性的值的图形表示形式，该属性的值将显示在属性网格中。 为此，请重写 `GetPaintValueSupported` 和 `PaintValue`。  有关更多信息，请参见<xref:System.Drawing.Design.UITypeEditor>。

> [!NOTE]
> 在**Dsl**项目的单独代码文件中添加代码。

例如:

```csharp
internal class TextFileNameEditor : System.Windows.Forms.Design.FileNameEditor
{
  protected override void InitializeDialog(System.Windows.Forms.OpenFileDialog openFileDialog)
  {
    base.InitializeDialog(openFileDialog);
    openFileDialog.Filter = "Text files(*.txt)|*.txt|All files (*.*)|*.*";
    openFileDialog.Title = "Select a text file";
  }
}
```

若要使用此编辑器，请将域属性的**自定义属性**设置为：

```csharp
[System.ComponentModel.Editor (
   typeof(MyNamespace.TextFileNameEditor)
   , typeof(System.Drawing.Design.UITypeEditor))]
```

有关更多信息，请参见<xref:System.Drawing.Design.UITypeEditor>。

## <a name="provide-a-drop-down-list-of-values"></a>提供值的下拉列表

您可以为用户提供值列表以供选择。

> [!NOTE]
> 此方法提供了在运行时可以更改的值的列表。 如果希望提供不会更改的列表，请考虑改用枚举类型作为域属性的类型。

若要定义标准值的列表，请将一个具有以下格式的 CLR 特性添加到域属性：

```csharp
[System.ComponentModel.TypeConverter
(typeof(MyTypeConverter))]
```

定义一个从 <xref:System.ComponentModel.TypeConverter> 派生的类。 将代码添加到**Dsl**项目的单独文件中。 例如:

```csharp
/// <summary>
/// Type converter that provides a list of values
/// to be displayed in the property grid.
/// </summary>
/// <remarks>This type converter returns a list
/// of the names of all "ExampleElements" in the
/// current store.</remarks>
public class MyTypeConverter : System.ComponentModel.TypeConverter
{
  /// <summary>
  /// Return true to indicate that we return a list of values to choose from
  /// </summary>
  /// <param name="context"></param>
  public override bool GetStandardValuesSupported
    (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Returns true to indicate that the user has
  /// to select a value from the list
  /// </summary>
  /// <param name="context"></param>
  /// <returns>If we returned false, the user would
  /// be able to either select a value from
  /// the list or type in a value that is not in the list.</returns>
  public override bool GetStandardValuesExclusive
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Return a list of the values to display in the grid
  /// </summary>
  /// <param name="context"></param>
  /// <returns>A list of values the user can choose from</returns>
  public override StandardValuesCollection GetStandardValues
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    // Try to get a store from the current context
    // "context.Instance"  returns the element(s) that
    // are currently selected i.e. whose values are being
    // shown in the property grid.
    // Note that the user could have selected multiple objects,
    // in which case context.Instance will be an array.
    Store store = GetStore(context.Instance);

    List<string> values = new List<string>();

    if (store != null)
    {
      values.AddRange(store.ElementDirectory
        .FindElements<ExampleElement>()
        .Select<ExampleElement, string>(e =>
      {
        return e.Name;
      }));
    }
    return new StandardValuesCollection(values);
  }

  /// <summary>
  /// Attempts to get to a store from the currently selected object(s)
  /// in the property grid.
  /// </summary>
  private Store GetStore(object gridSelection)
  {
    // We assume that "instance" will either be a single model element, or
    // an array of model elements (if multiple items are selected).

    ModelElement currentElement = null;

    object[] objects = gridSelection as object[];
    if (objects != null && objects.Length > 0)
    {
      currentElement = objects[0] as ModelElement;
    }
    else
    {
        currentElement = gridSelection as ModelElement;
    }

    return (currentElement == null) ? null : currentElement.Store;
  }

}
```

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)