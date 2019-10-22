---
title: 向层关系图添加命令和笔势 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams, adding custom commands
- layer diagrams, adding custom gestures
ms.assetid: ac9c417b-0b40-4a90-86f5-ee3cbdce030b
caps.latest.revision: 40
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7b0c54975cdd5bc86f77dddbd5ca1a56c1896394
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655317"
---
# <a name="add-commands-and-gestures-to-layer-diagrams"></a>向层关系图添加命令和笔势
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在 Visual Studio 中的层关系图上定义上下文菜单命令和笔势处理程序。 可以将这些扩展打包到 Visual Studio 集成扩展 (VSIX) 中，以便将其分发给其他 Visual Studio 用户。

 如果你愿意，可以在同一 Visual Studio 项目中定义多个命令和笔势处理程序。 还可以将多个此类项目合并到一个 VSIX 中。 例如，你可以定义其中包含层命令、特定于域的语言和用于 UML 关系图的命令的单个 VSIX。

> [!NOTE]
> 还可以自定义体系结构验证，在其中对用户的源代码和层关系图进行比较。 应在单独的 Visual Studio 项目中定义体系结构验证。 你可以将其添加到其他扩展所在的同一 VSIX 中。 有关详细信息，请参阅[向层关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)。

## <a name="requirements"></a>要求
 请参阅 [要求](../modeling/extend-layer-diagrams.md#prereqs)。

## <a name="defining-a-command-or-gesture-in-a-new-vsix"></a>在新的 VSIX 中定义命令或笔势
 创建扩展的最快方法是使用项目模板。 这会将代码和 VSIX 清单置于同一项目中。

#### <a name="to-define-an-extension-by-using-a-project-template"></a>若要使用项目模板定义扩展

1. 使用“文件” 菜单上的“新建项目” 命令，在新的解决方案中创建项目。

2. 在“新建项目” 对话框的“建模项目”下，选择“层设计器命令扩展” 或“层设计器笔势扩展”。

    模板将创建包含一个小型工作示例的项目。

3. 若要测试此扩展，请按“CTRL+F5” 或“F5”。

    此时将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。 在此实例中创建层关系图。 命令或笔势扩展应在此关系图中使用。

4. 关闭实验实例并修改示例代码。 有关详细信息，请参阅[在程序代码中导航和更新层模型](../modeling/navigate-and-update-layer-models-in-program-code.md)。

5. 可以向同一项目添加更多命令或笔势处理程序。 有关详细信息，请参阅以下章节之一：

    [定义菜单命令](#command)

    [定义笔势处理程序](#gesture)

6. 若要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的主实例中或在另一台计算机上安装扩展，请在*bin \\* 中找到 **.vsix**文件。 将此文件复制到想在其上安装它的计算机，然后双击它。 若要卸载它，请使用“工具” 菜单上的“扩展和更新” 。

## <a name="adding-a-command-or-gesture-to-a-separate-vsix"></a>将命令或笔势添加到单独的 VSIX
 如果想要创建一个包含命令、层验证程序和其他扩展的 VSIX，建议创建一个项目来定义 VSIX，并分隔处理程序的项目。 有关其他类型的建模扩展的信息，请参阅[扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)。

#### <a name="to-add-layer-extensions-to-a-separate-vsix"></a>将层扩展添加到单独的 VSIX

1. 在新的或现有 Visual Studio 解决方案中创建类库项目。 在“新建项目” 对话框中，单击“Visual C#” ，然后单击“类库”。 此项目将包含命令或笔势处理程序类。

    > [!NOTE]
    > 可以在一个类库中定义多个命令或笔势处理程序类，但应在单独的类库中定义层验证类。

2. 在解决方案中标识或创建 VSIX 项目。 VSIX 项目包含名为 **source.extension.vsixmanifest**的文件。 若要添加 VSIX 项目：

    1. 在“新建项目” 对话框中，展开“Visual C#”，单击“扩展性”，然后单击“VSIX 项目”。

    2. 在解决方案资源管理器中，右键单击此 VSIX 项目，然后单击“设为启动项目”。

    3. 单击“选择版本” 并确保选中“Visual Studio” 。

3. 在 **source.extension.vsixmanifest**中的“资产”下，以 MEF 组件的形式添加命令或笔势处理程序。

    1. 在“资产”选项卡中，选择“新建”。

    2. 在“类型”处，选择“Microsoft.VisualStudio.MefComponent”。

    3. 在“源”处，选择“当前解决方案中的项目” ，然后选择命令或笔势处理程序项目的名称。

    4. 保存该文件。

4. 返回到命令或笔势处理程序项目，并添加以下项目引用。

|**引用**|**允许执行的操作**|
|-------------------|------------------------------------|
|Program Files\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|创建和编辑层|
|Microsoft.VisualStudio.Uml.Interfaces|创建和编辑层|
|Microsoft.VisualStudio.ArchitectureTools.Extensibility|修改关系图上的形状|
|System.ComponentModel.Composition|使用 Managed Extensibility Framework (MEF) 定义组件|
|Microsoft.VisualStudio.Modeling.Sdk.[版本号]|定义建模扩展|
|Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]|更新形状和关系图|

1. 编辑 C# 类库项目中的类文件，以包含你的扩展的代码。 有关详细信息，请参阅以下章节之一：

     [定义菜单命令](#command)

     [定义笔势处理程序](#gesture)

     另请参阅[在程序代码中导航和更新层模型](../modeling/navigate-and-update-layer-models-in-program-code.md)。

2. 若要测试此功能，请按 CTRL+F5 或 F5。 将打开 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。 在此实例中创建或打开层关系图。

3. 若要在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的主实例中或在另一台计算机上安装扩展，请找到 **bin\*** 目录中找到 **.vsix** 文件。 将此文件复制到想在其上安装 VSIX 的计算机。 双击 Windows 资源管理器（Windows 8 中的文件资源管理器）中的 VSIX 文件。

     若要卸载它，请使用“工具” 菜单上的“扩展和更新” 。

## <a name="command"></a> 定义菜单命令
 可向现有笔势或命令项目添加更多菜单命令定义。 每个命令均由具有以下特性的类进行定义：

- 类的声明方式如下：

   `[LayerDesignerExtension]`

   `[Export(typeof(ICommandExtension))]`

   `public class`  *MyLayerCommand*  `: ICommandExtension { ... }`

- 命名空间和类的名称并不重要。

- 实现 `ICommandExtension` 的方法如下：

  - `string Text {get;}` - 菜单中显示的标签。

  - `void QueryStatus(IMenuCommand command)` - 用户右键单击关系图时调用它，用于确定对于用户的当前选择内容，命令是否可见和已启用。

  - `void Execute(IMenuCommand command)` - 用户选择此命令时调用它。

- 若要确定当前选择内容，可导入 `IDiagramContext`：

   `[Import]`

   `public IDiagramContext DiagramContext { get; set; }`

   `...`

   `DiagramContext.CurrentDiagram.SelectedShapes.Count()...`

  有关详细信息，请参阅[在程序代码中导航和更新层模型](../modeling/navigate-and-update-layer-models-in-program-code.md)。

  若要添加新命令，请创建包含以下示例的新代码文件。 然后测试并编辑它。

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;

namespace MyLayerExtension // Change to your preference.
{
  // This is a feature for Layer diagrams:
  [LayerDesignerExtension]
  // This feature is a menu command:
  [Export(typeof(ICommandExtension))]
  // Change the class name to your preference:
  public class MyLayerCommand : ICommandExtension
  {
    [Import]
    public IDiagramContext DiagramContext { get; set; }

    [Import]
    public ILinkedUndoContext LinkedUndoContext { get; set; }

    // Menu command label:
    public string Text
    {
      get { return "Duplicate layers"; }
    }

    // Called when the user right-clicks the diagram.
    // Defines whether the command is visible and enabled.
    public void QueryStatus(IMenuCommand command)
    {
      command.Visible =
      command.Enabled = DiagramContext.CurrentDiagram
        .SelectedShapes.Count() > 0;
    }

    // Called when the user selects the command.
    public void Execute(IMenuCommand command)
    {
      // A selection of starting points:
      IDiagram diagram = this.DiagramContext.CurrentDiagram;
      ILayerModel lmodel = diagram.GetLayerModel();
      foreach (ILayer layer in lmodel.Layers)
      { // All layers in model.
      }
      // Updates should be performed in a transaction:
      using (ILinkedUndoTransaction t =
        LinkedUndoContext.BeginTransaction("copy selection"))
      {
        foreach (ILayer layer in
          diagram.SelectedShapes
            .Select(shape=>shape.GetLayerElement())
            .Where(element => element is ILayer))
        {
          ILayer copy = lmodel.CreateLayer(layer.Name + "+");
          // Position the shapes:
          IShape originalShape = layer.GetShape();
          copy.GetShape().Move(
            originalShape.XPosition + originalShape.Width * 1.2,
            originalShape.YPosition);
        }
        t.Commit();
      }
    }
  }
}
```

## <a name="gesture"></a> 定义笔势处理程序
 当用户将项拖动到层关系图上时以及双击关系图中的任意位置时，笔势处理程序进行响应。

 你可以向现有命令或笔势处理程序 VSIX 项目添加定义笔势处理程序的代码文件：

```
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;
namespace MyLayerExtensions // change to your preference
{
  [LayerDesignerExtension]
  [Export(typeof(IGestureExtension))]
  public class MyLayerGestureHandler : IGestureExtension
  {
  }
}
```

 请注意关于笔势处理程序的以下几点：

- `IGestureExtension` 的成员如下：

   **OnDoubleClick** - 用户双击关系图上的任意位置时调用它。

   **CanDragDrop** - 如果用户在将项拖动到关系图上的同时移动鼠标，则重复调用它。 它必须快速运行。

   **OnDragDrop** - 用户将项放到关系图上时调用它。

- 每个方法的第一个参数是 `IShape`，你可以从它获取层元素。 例如:

  ```
  public void OnDragDrop(IShape target, IDataObject data)
  {
      ILayerElement element = target.GetLayerElement();
      if (element is ILayer)
      {
          // ...
      }
  }
  ```

- 已为某些类型的拖动项定义了处理程序。 例如，用户可以将项从解决方案资源管理器拖动到层关系图上。 无法为这些类型的项定义拖动处理程序。 在这些情况下，不会调用 `DragDrop` 方法。

  有关如何在将其他项拖到关系图上时对其进行解码的详细信息，请参阅[在建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)。

## <a name="see-also"></a>请参阅
 [在程序代码中导航和更新层模型](../modeling/navigate-and-update-layer-models-in-program-code.md)[向层关系图添加自定义体系结构验证](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)[定义和安装建模扩展](../modeling/define-and-install-a-modeling-extension.md)
