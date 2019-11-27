---
title: 在关系图上显示 UML 模型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: adf1f1f2-2ad9-4ade-82de-c6a5194ab471
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 67eb1a6ce55292415da4a5c4e363941a4285d8b7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296014"
---
# <a name="display-a-uml-model-on-diagrams"></a>在关系图上显示 UML 模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 扩展的程序代码中，可以控制模型元素在关系图上的显示方式。 若要查看支持 UML 模式的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

在本主题中：
- [若要在关系图上显示元素](#Display)

- [访问表示元素的形状](#GetShapes)

- [移动形状并调整其大小](#Moving)

- [从关系图中删除形状](#Removing)

- [打开并创建关系图](#Opening)

- [示例：用于对齐形状的命令](#AlignCommand)

## <a name="Display"></a>若要在关系图上显示元素
 创建用例或操作等元素时，用户可以在 UML 模型资源管理器中看到它，但它并不始终自动显示在关系图中。 在某些情况下，必须编写代码才能显示它。 下表总结了备选项。

|元素的类型|例如|若要显示它，你的代码必须|
|---------------------|-----------------|-------------------------------------|
|分类器|`Class`<br /><br /> `Component`<br /><br /> `Actor`<br /><br /> `Use Case`|在指定关系图上创建关联的形状。 你可以为每个分类器创建任意数目的形状。<br /><br /> `diagram.Display<modelElementType>`<br /><br /> `(modelElement, parentShape,`<br /><br /> `xPosition , yPosition);`<br /><br /> 对于位于关系图顶级的形状，将 `parentShape` 设置为 `null`。<br /><br /> 若要显示形状内部的形状：<br /><br /> `IShape<IUseCase> usecaseShape =`<br /><br /> `useCaseDiagram.Display`<br /><br /> `(useCase,`<br /><br /> `subsystemShape,`<br /><br /> `subsystemShape.XPosition + 5,`<br /><br /> `subsystemShape.YPosition + 5);`**注意：** 如果在**ILinkedUndo**事务中执行显示，则该方法有时不返回任何 `IShape`。 但形状创建无误，且可使用 `IElement.Shapes().` 进行访问|
|分类器的子级|属性、操作、<br /><br /> 部件、端口|自动 - 无需任何代码。<br /><br /> 它显示为父级的一部分。|
|行为|交互（序列），<br /><br /> 活动|将行为绑定到适当的关系图。<br /><br /> 每个行为每次最多可绑定到一个关系图上。<br /><br /> 例如:<br /><br /> `sequenceDiagram.Bind(interaction);`<br /><br /> `activityDiagram.Bind(activity);`|
|行为的子级|生命线、消息、操作、对象节点|自动 - 无需任何代码。<br /><br /> 如果父级绑定到了关系图，则将显示它。|
|关系|关联、泛化、流、依赖关系|自动 - 无需任何代码。<br /><br /> 它将在显示两端的每个关系图上显示。|

## <a name="GetShapes"></a>访问表示元素的形状
 表示元素属于以下类型的形状：

 `IShape`

 `IShape<` *ElementType* `>`

 其中*ElementType*是模型元素（如 `IClass` 或 `IUseCase`）的类型。

|||
|-|-|
|`anElement.Shapes ()`|打开关系图中表示此元素的所有 `IShapes`。|
|`anElement.Shapes(aDiagram)`|特定关系图中表示此元素的所有 `IShapes`。|
|`anIShape.GetElement()`|形状表示的 `IElement`。 通常情况下，会将其转换为的 IElement 的子类。|
|`anIShape.Diagram`|包含形状的 `IDiagram`。|
|`anIShape.ParentShape`|包含 `anIShape` 的形状。 例如，端口形状包含在组件形状中。|
|`anIShape.ChildShapes`|包含在 `IShape` 或 `IDiagram` 中的形状。|
|`anIShape.GetChildShapes<IUseCase>()`|包含在 `IShape` 或 `IDiagram` 中表示指定类型的元素（如 `IUseCase`）的形状。|
|`IShape iShape = ...;`<br /><br /> `IShape<IClass> classShape = iShape.ToIShape<IClass>();`<br /><br /> `IClass aClass = classShape.Element;`|将泛型 `IShape` 转换为强类型 `IShape<IElement>`。|
|`IShape<IClassifier> classifierShape;`<br /><br /> `IShape<IUseCase> usecaseShape =`<br /><br /> `classifierShape.ToIShape<IUseCase>();`|将形状从一个参数化形状类型转换到另一个类型。|

## <a name="Moving"></a>移动形状并调整其大小

|||
|-|-|
|`anIShape.Move(x, y, [width], [height])`|移动形状或调整其大小。|
|`IDiagram.EnsureVisible( IEnumerable<IShape> shapes, bool zoomToFit = false)`|激活窗口并滚动关系图，以便所有给定形状均可见。 这些形状必须都位于关系图上。 如果 `zoomToFit` 为 true，则将在必要时扩展关系图，使所有形状可见。|

 有关示例，请参阅[定义对齐方式命令](#AlignCommand)。

## <a name="Removing"></a>从关系图中删除形状
 可以删除某些类型的元素的形状而不删除元素本身。

|模型元素|若要删除形状|
|-------------------|-------------------------|
|分类器：类、接口、枚举、参与者、用例或组件|`shape.Delete();`|
|行为：交互或活动|可以从项目中删除关系图。 使用 `IDiagram.FileName` 获取路径。<br /><br /> 这不会从模型中删除行为。|
|任何其他形状|不能从关系图中显式删除其他形状。 如果从模型中删除元素，或从关系图中删除父形状，形状将自动消失。|

## <a name="Opening"></a>打开并创建关系图

### <a name="to-access-the-users-current-diagram-from-a-command-or-gesture-extension"></a>若要从命令或笔势扩展访问用户的当前关系图
 在类中声明此导入的属性：

 `[Import]`

 `IDiagramContext Context { get; set; }`

 在方法中，访问关系图：

 `IClassDiagram classDiagram =`

 `Context.CurrentDiagram as IClassDiagram;`

> [!NOTE]
> `IDiagram`（及其 `IClassDiagram` 等子类型）的实例只在你正在处理的命令中有效。 不建议在控件返回至用户时仍存在的变量中保留 `IDiagram` 对象。

 有关详细信息，请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。

### <a name="to-obtain-a-list-of-open-diagrams"></a>若要获取打开关系图的列表
 项目中当前打开的关系图的列表：

```
Context.CurrentDiagram.ModelStore.Diagrams()
```

## <a name="to-access-the-diagrams-in-a-project"></a>若要访问项目中的关系图
 可使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API 打开和创建建模项目和关系图。

 请注意从 `EnvDTE.ProjectItem` 到 `IDiagramContext` 的转换。

```

      using EnvDTE; // Visual Studio API
...
[Import]
public IServiceProvider ServiceProvider { get; set; }
...
// Get Visual Studio API
DTE dte = ServiceProvider.GetService(typeof(DTE)) as DTE;
// Get current Visual Studio project
Project project = dte.ActiveDocument.ProjectItem.ContainingProject;
// Open and process every diagram in the project.
foreach (ProjectItem item in project.ProjectItems)
{
  // Cast ProjectItem to IDiagramContext
  IDiagramContext context = item as IDiagramContext;
  if (context == null)
  {
     // This is not a diagram file.
     continue;
  }
  // Open the file and give the window the focus.
  if (!item.IsOpen)
  {
      item.Open().Activate();
  }
  // Get the diagram.
  IDiagram diagram = context.CurrentDiagram;
  // Deal with specific diagram types.
  ISequenceDiagram seqDiagram = diagram as ISequenceDiagram;
  if (seqDiagram != null)
  { ... } } }
```

 将控件返回至 `IDiagram` 后，[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 及其子类型的实例均无效。

 还可从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目获取模型存储区：

```

      Project project = ...;
IModelStore modelStore = (project as IModelingProject).Store;
```

## <a name="AlignCommand"></a>示例：用于对齐形状的命令
 以下代码实现可准确对齐形状的菜单命令。 用户必须先将两个或更多形状在垂直或水平方向上大致对齐。 然后才能使用对齐命令使它们居中对齐。

 若要使此命令可用，请将此代码添加到菜单命令项目，然后将生成的扩展部署到用户。 有关详细信息，请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel.Composition;
using System.Linq;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace AlignCommand
{
  // Implements a command to align shapes in a UML class diagram.
  // The user first selects shapes that are roughly aligned either vertically or horizontally.
  // This command will straighten them up.

  // Place this file in a menu command extension project.
  // See https://msdn.microsoft.com/library/ee329481.aspx

  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension] // TODO: Add other diagram types if needed
  class CommandExtension : ICommandExtension
  {
    /// <summary>
    /// See https://msdn.microsoft.com/library/ee329481.aspx
    /// </summary>
    [Import]
    IDiagramContext context { get; set; }

    /// <summary>
    /// Transaction context.
    /// See https://msdn.microsoft.com/library/ee330926.aspx
    /// </summary>
    [Import]
    ILinkedUndoContext linkedUndo { get; set; }

    /// <summary>
    /// Called when the user selects the command.
    /// </summary>
    /// <param name="command"></param>
    public void Execute(IMenuCommand command)
    {
      Align(context.CurrentDiagram.SelectedShapes);
    }

    /// <summary>
    /// Called when the user right-clicks on the diagram.
    /// Determines whether the command is enabled.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      IEnumerable<IShape> currentSelection = context.CurrentDiagram.SelectedShapes;
      // Make it visible if there are shapes selected:
      command.Visible = currentSelection.Count() > 0 && !(currentSelection.FirstOrDefault() is IDiagram);

      // Make it enabled if there are two or more shapes that are roughly in line:
      command.Enabled = currentSelection.Count() > 1
        && (HorizontalAlignCenter(currentSelection) > 0.0
        || VerticalAlignCenter(currentSelection) > 0.0);

    }

    /// <summary>
    /// Title of the menu command.
    /// </summary>
    public string Text
    {
      get { return "Align Shapes"; }
    }

    /// <summary>
    /// Find a horizontal line that goes through a list of shapes.
    /// </summary>
    /// <param name="shapes"></param>
    /// <returns></returns>
    private static double HorizontalAlignCenter(IEnumerable<IShape> shapes)
    {
      double Y = -1.0;
      double top = 0.0, bottom = shapes.First().Bottom();
      foreach (IShape shape in shapes)
      {
        top = Math.Max(top, shape.Top());
        bottom = Math.Min(bottom, shape.Bottom());
      }
      if (bottom > top) Y = (bottom + top) / 2.0;
      return Y;
    }

    /// <summary>
    /// Find a vertical line that goes through a list of shapes.
    /// </summary>
    /// <param name="shapes"></param>
    /// <returns></returns>
    private static double VerticalAlignCenter(IEnumerable<IShape> shapes)
    {
      double X = -1.0;
      double left = 0.0, right = shapes.First().Right();
      foreach (IShape shape in shapes)
      {
        left = Math.Max(left, shape.Left());
        right = Math.Min(right, shape.Right());
      }
      if (right > left) X = (right + left) / 2.0;
      return X;
    }

    /// <summary>
    /// Line up those shapes that are roughly aligned.
    /// </summary>
    /// <param name="shapes"></param>
    private void Align(IEnumerable<IShape> shapes)
    {
      if (shapes.Count() > 1)
      {
        // The shapes must all overlap either horizontally or vertically.
        // Find a horizontal line that is covered by all the shapes:
        double Y = HorizontalAlignCenter(shapes);
        if (Y > 0.0) // Negative if they don't overlap.
        {
          // Adjust all the shape positions in one transaction:
          using (ILinkedUndoTransaction t = linkedUndo.BeginTransaction("align"))
          {
            foreach (IShape shape in shapes)
            {
              shape.AlignYCenter(Y);
            }
            t.Commit();
          }
        }
        else
        {
          // Find a vertical line that is covered by all the shapes:
          double X = VerticalAlignCenter(shapes);
          if (X > 0.0) // Negative if they don't overlap.
          {
            // Adjust all the shape positions in one transaction:
            using (ILinkedUndoTransaction t = linkedUndo.BeginTransaction("align"))
            {
              foreach (IShape shape in shapes)
              {
                shape.AlignXCenter(X);
              }
              t.Commit();
            }
          }
        }
      }
    }
  }

  /// <summary>
  /// Convenience extensions for IShape.
  /// </summary>
  public static class IShapeExtension
  {
    public static double Bottom(this IShape shape)
    {
      return shape.YPosition + shape.Height;
    }

    public static double Top(this IShape shape)
    {
      return shape.YPosition;
    }

    public static double Left(this IShape shape)
    {
      return shape.XPosition;
    }

    public static double Right(this IShape shape)
    {
      return shape.XPosition + shape.Width;
    }

    public static void AlignYCenter(this IShape shape, double Y)
    {
      shape.Move(shape.XPosition, Y - shape.YCenter());
    }

    public static void AlignXCenter(this IShape shape, double X)
    {
      shape.Move(X - shape.XCenter(), shape.YPosition);
    }

    /// <summary>
    /// We can adjust what bit of the shape we want to be aligned.
    /// The default is the center of the shape.
    /// </summary>
    /// <param name="shape"></param>
    /// <returns></returns>
    public static double YCenter(this IShape shape)
    {
        return shape.Height / 2.0;
    }

    /// <summary>
    /// We can adjust what bit of the shape we want to be aligned.
    /// The default is the center of the shape.
    /// </summary>
    /// <param name="shape"></param>
    /// <returns></returns>
    public static double XCenter(this IShape shape)
    {
        return shape.Width / 2.0;
    }
  }
}

```

## <a name="see-also"></a>请参阅
 [扩展 uml 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)[导航 uml 模型](../modeling/navigate-the-uml-model.md)[示例：对齐关系图菜单上的形状的命令](https://go.microsoft.com/fwlink/?LinkId=213809)[示例：创建元素、形状和构造型](https://go.microsoft.com/fwlink/?LinkId=213811)
