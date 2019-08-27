---
title: 自定义文本和图像字段
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 607809b05688931b139b27fec1803719b928dfea
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445815"
---
# <a name="customizing-text-and-image-fields"></a>自定义文本和图像字段
形状中定义的文本修饰器时，它表示由文本字段。 有关 TextFields 和其他 ShapeFields 的初始化的示例，在 DSL 解决方案中检查 Dsl\GeneratedCode\Shapes.cs。

 文本字段是管理形状，例如分配给标签的空间内的某个区域的对象。 一个文本字段的实例共享同一个类的多个形状之间。 文本字段实例不会存储每个实例单独的标签文本： 相反，`GetDisplayText(ShapeElement)`方法使用作为参数，形状，并可以查找依赖于形状与模型元素的当前状态的文本。

## <a name="how-the-appearance-of-a-text-field-is-determined"></a>如何确定文本字段的外观
 `DoPaint()`方法调用向显示的字段在屏幕上。 可以重写默认`DoPaint(),`也可以重写一些它调用的方法。 下面的简化的版本的默认方法可以帮助您了解如何重写默认行为：

```csharp
// Simplified version:
public override void DoPaint(DiagramPaintEventArgs e, ShapeElement parentShape)
{
  string text = GetDisplayText(shape);
  StringFormat format = GetStringFormat(parentShape);
  Brush brush = GetTextBrush(e.View, shape);
  using (Font font = GetFont(shape))
  {
    e.Graphics.DrawString(text, font, brush, format);
  }
}
// StringFormat determines whether the string is centered etc.
// To customize statically for all instances of this shape field,
// assign to DefaultStringFormat.
// To customize dynamically or per shape, override this:
public virtual StringFormat GetStringFormat(ShapeElement shape)
{ return DefaultStringFormat; }

// Override to customize the displayed string:
public virtual string GetDisplayText(ShapeElement shape)
{ return this.GetValue(shape).ToString(); }

// Brush determines the text color.
// To change the brush for every field, change the shape's styleset.
// To customize to a brush in the style set, override GetTextBrushId.
// To change the brush to non-standard color, override this.
// Should take account of whether selected.
public virtual Brush GetTextBrush(DiagramClientView view, ShapeElement shape)
{ return shape.StyleSet.GetBrush(this.GetTextBrushId(view, shape)); }

// Brush ID selects a brush from a StyleSet.
// Either return a member of DiagramBrushes
// or add your own brush to the shape or application's styleset.
// Override this to change dynamically or per instance.
// To change statically, just assign to default values.
public virtual StyleSetResourceId GetTextBrushId(DiagramClientView view, ShapeElement shape)
{ return IsSelected(view, shape) ? (view.Focused ? DefaultSelectedTextBrushId
: DefaultInactiveSelectedTextBrushId ) : DefaultTextBrushId ;
}

// Font determines the shape and size of the text.
// To change the font for every field, change the shape's styleset.
// To customize to a font in the style set, override GetFontId.
// To change the font to a non-standard font, override this.
public virtual Font GetFont(ShapeElement shape)
{ return shape.StyleSet.GetFont(GetFontId(shape)); }

// Selects a font from a styleset.
// Either return a member of DiagramFonts or
// add your own font to the shape or application's styleset.
// To change statically for all instances of this field,
// assign to DefaultFontId.
// To change per shape or dynamically, override this.
public virtual StyleSetResourceId GetFontId(ShapeElement parentShape)
{ return DefaultFontId; }
```

 有的几个其他对`Get`方法和`Default`属性，如`DefaultMultipleLine/GetMultipleLine()`。 可以将值分配给要更改的所有实例的形状字段的值的默认属性。 若要将值设置到另一个，或依赖于该形状或其模型元素的状态从一个形状实例会有所不同，重写`Get`方法。

## <a name="static-customizations"></a>静态自定义项
 如果你想要更改此形状字段的每个实例，请先确定是否可以在 DSL 定义中设置该属性。 例如，可以在属性窗口中设置字体大小和样式。

 如果不是，然后重写`InitializeShapeFields`shape 类和分配到相应的值的方法`Default...`文本字段的属性。

> [!WARNING]
> 若要重写`InitializeShapeFields()`，则必须设置**生成双派生**形状类的属性`true`DSL 定义中。

 在此示例中，形状具有将用于用户注释的文本字段。 我们想要使用的标准注释字体。 因为它是一种标准字体样式集中，我们可以设置默认字体 id:

```csharp

 partial class ExampleShape
{   protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Find and update comment field:
      TextField commentField = ShapeElement.FindShapeField(shapeFields, "CommentDecorator") as TextField;
      // Use the standard font for comments:
      commentField.DefaultFontId = DiagramFonts.CommentText;
```

## <a name="dynamic-customizations"></a>动态自定义项
 若要使不同的外观依赖于一个形状或其模型元素的状态，派生的子类`TextField`并重写一个或多个`Get...`方法。 您还必须重写形状的 InitializeShapeFields 方法和文本字段的实例替换为你自己的类的实例。

 下面的示例使字体的文本字段依赖于形状的模型元素的布尔值的域属性的状态。

 若要运行此示例代码，创建新 DSL 解决方案使用最小语言模板。 添加布尔域属性`AlternateState`到 ExampleElement 域类。 将图标修饰器添加到 ExampleShape 类，并将其图像设置为位图文件。 单击**转换所有模板**。 在 DSL 项目中，添加一个新的代码文件并插入以下代码。

 若要测试此代码，按 F5，并在调试解决方案中，打开示例关系图。 应显示的图标的默认状态。 选择形状，然后在属性窗口中的值更改**AlternateState**属性。 应更改元素名称的字体。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...

  partial class ExampleShape
  {
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Replace the text field for NameDecorator:
      TextField oldField = ShapeElement.FindShapeField(shapeFields, "NameDecorator") as TextField;
      shapeFields.Remove(oldField);
      // Replace with my text field based on DSL Definition values:
      MyTextField newField = new MyTextField(oldField);
      shapeFields.Add(newField);
    }
  }
  /// <summary>
  /// Dynamic font depends on state of model element.
  /// </summary>
  public class MyTextField : TextField
  {
    public MyTextField(TextField prototype)
      : base(prototype.Name)
    {
      DefaultText = prototype.DefaultText;
      DefaultFocusable = prototype.DefaultFocusable;
      DefaultAutoSize = prototype.DefaultAutoSize;
      AnchoringBehavior.MinimumHeightInLines = prototype.AnchoringBehavior.MinimumHeightInLines;
      AnchoringBehavior.MinimumWidthInCharacters = prototype.AnchoringBehavior.MinimumWidthInCharacters;
      DefaultAccessibleState = prototype.DefaultAccessibleState;
    }

    public override System.Drawing.Font GetFont(ShapeElement parentShape)
    {
      // Access the Boolean domain property of the model element:
      if ((parentShape.ModelElement as ExampleElement).AlternateState)
        return new System.Drawing.Font("Callisto", 14.0f,
               System.Drawing.FontStyle.Italic |
               System.Drawing.FontStyle.Bold);
      else
        return base.GetFont(parentShape);
    }

  }
```

## <a name="style-sets"></a>样式设置
 前面的示例说明如何将文本字段更改为任何可用的字体。 但是，更可取方法是将其更改为一组与该形状或应用程序相关联的样式之一。 若要执行此操作，重写<xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField.GetFontId%2A>或 GetTextBrushId()。

 或者，请考虑更改形状的样式集通过重写<xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.InitializeResources%2A>。 更改字体和形状字段的所有画笔效果。

## <a name="customizing-image-fields"></a>自定义图像字段
 当在形状中，定义图像修饰器且定义了图像形状时，由 ImageField 管理在其中显示该形状的区域。 有关 ImageFields 和其他 ShapeFields 的初始化的示例，在 DSL 解决方案中检查 Dsl\GeneratedCode\Shapes.cs。

 ImageField 是管理形状，如的修饰器分配的空间内的某个区域的对象。 一个 ImageField 实例共享相同的形状类的多个形状之间。 ImageField 实例不会存储每个形状的单独映像： 相反，`GetDisplayImage(ShapeElement)`方法使用作为参数，形状，并可以查看映像依赖于形状与模型元素的当前状态。

 如果你想特殊行为，例如可变图像，可以创建自己的类派生自 ImageField。

#### <a name="to-create-a-subclass-of-imagefield"></a>若要创建的 ImageField 子类

1. 设置**生成双派生**的 DSL 定义中的父形状类的属性。

2. 重写`InitializeShapeFields`形状类的方法。

    - 在 DSL 项目中，创建一个新代码文件并编写形状类的分部类定义。 重写的方法定义。

3. 检查的代码`InitializeShapeFields`DSL\GeneratedCode\Shapes.cs 中。

     在重写方法中，调用基方法，然后创建你自己的图像字段类的实例。 用于替换中的正则图像字段`shapeFields`列表。

## <a name="dynamic-icons"></a>动态图标
 此示例使依赖于形状的模型元素的状态更改的图标。

> [!WARNING]
> 此示例演示如何使动态图像修饰器。 但如果只想要一个或两个映像，具体取决于模型变量的状态之间切换，它会更易于创建多个图像修饰器，找到在同一位置上相应的形状，并设置要取决于模型的特定值的可见性筛选器变量。 若要设置此筛选器，在 DSL 定义中选择形状地图，打开 DSL 详细信息窗口中，然后单击修饰器选项卡。

 若要运行此示例代码，创建新 DSL 解决方案使用最小语言模板。 添加布尔域属性`AlternateState`到 ExampleElement 域类。 将图标修饰器添加到 ExampleShape 类，并将其图像设置为位图文件。 单击**转换所有模板**。 在 DSL 项目中，添加一个新的代码文件并插入以下代码。

 若要测试此代码，按 F5，并在调试解决方案中，打开示例关系图。 应显示的图标的默认状态。 选择形状，然后在属性窗口中的值更改**AlternateState**属性。 然后显示旋转 90 度，该形状上通过该图标。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...
partial class ExampleShape
{
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    /// <param name="shapeFields"></param>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);

      // Replace the image field:
      ShapeField oldField = ShapeElement.FindShapeField(shapeFields, "IconDecorator");
      shapeFields.Remove(oldField);
      // Must keep the same name:
      MyImageField newField = new MyImageField(oldField.Name);
      shapeFields.Add(newField);
      newField.DefaultImage = (oldField as ImageField).DefaultImage.Clone() as System.Drawing.Image;
    }
  }

  public class MyImageField : ImageField
  {
    public MyImageField(string tag) : base(tag) { }

    /// <summary>
    /// Get the image for this field in the given shape.
    /// </summary>
    public override System.Drawing.Image GetDisplayImage(ShapeElement parentShape)
    {
      ExampleElement element = parentShape.ModelElement as ExampleElement;
      if (element.AlternateState == true)
        return AlternateImage;
      else
        return base.GetDisplayImage(parentShape);
    }

    private System.Drawing.Image alternateImage;
    public System.Drawing.Image AlternateImage
    {
      get
      {
        if (alternateImage == null)
        {
          // Alternate image is a copy of the default, rotated by 90 degrees:
          alternateImage = this.DefaultImage.Clone() as System.Drawing.Image;
          alternateImage.RotateFlip(System.Drawing.RotateFlipType.Rotate90FlipNone);
        }
        return alternateImage;
      }
    }
  }
}
```

## <a name="see-also"></a>请参阅

- [定义形状和连接线](../modeling/defining-shapes-and-connectors.md)
- [在图表上设置背景图像](../modeling/setting-a-background-image-on-a-diagram.md)
- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)