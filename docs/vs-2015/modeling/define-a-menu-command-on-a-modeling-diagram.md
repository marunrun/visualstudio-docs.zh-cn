---
title: 在建模图上定义菜单命令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, menu commands
ms.assetid: 79c277de-5871-4fc7-9701-55eec5c3cd46
caps.latest.revision: 63
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 87acbb53fd8fe5eae744aa4ef72c808da8eb6642
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663480"
---
# <a name="define-a-menu-command-on-a-modeling-diagram"></a>在建模图上定义菜单命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，你可以在 UML 关系图的快捷菜单上定义其他菜单项。 你可以控制是否在关系图上任意元素的快捷菜单上显示和启用菜单命令，并且可以编写在用户选择菜单项时运行的代码。 可以将这些扩展打包到 Visual Studio 集成扩展 ([VSIX](http://go.microsoft.com/fwlink/?LinkId=160780)) 中，并将其分发给其他 Visual Studio 用户。

## <a name="requirements"></a>要求
 请参阅 [要求](../modeling/extend-uml-models-and-diagrams.md#Requirements)。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

## <a name="defining-the-menu-command"></a>定义菜单命令
 要为 UML 设计器创建菜单命令，必须创建一个用于定义命令行为的类，并将该类嵌入 Visual Studio 集成扩展 (VSIX) 中。 VSIX 用作可安装该命令的容器。 有两种替代方法可以定义菜单命令：

- **使用项目模板在其自身 VSIX 中创建菜单命令。** 此方法更快。 如果不希望将菜单命令与其他类型的扩展（如验证扩展、自定义工具箱项或笔势处理程序）组合在一起，可以采用此方法。

- **创建单独的菜单命令和 VSIX 项目。** 如果希望将多种类型的扩展组合到同一个 VSIX 中，可以采用此方法。 例如，如果菜单命令要求模型遵守特定的约束，则可以将该菜单命令作为一种验证方法嵌入同一 VSIX 中。

#### <a name="to-create-a-menu-command-in-its-own-vsix"></a>若要在自己的 VSIX 中创建菜单命令

1. 在 “新建项目”对话框中的“建模项目”下，选择“命令扩展”。

2. 在新项目中打开 **.cs** 文件并修改 `CommandExtension` 类，以实现命令。

    有关详细信息，请参阅 [实现菜单命令](#Implementing)。

3. 可以通过定义新类向此项目中添加其他命令。

4. 按 F5 测试菜单命令。 有关详细信息，请参阅 [执行菜单命令](#Executing)。

5. 在另一台计算机上安装菜单命令，方法是：将文件 bin 复制 \\ 由项目生成的 **\* \\ \*。** 有关详细信息，请参阅 [安装和卸载扩展](#Installing)。

   下面是替代过程：

#### <a name="to-create-a-menu-command-in-a-separate-class-library-dll-project"></a>若要在单独的类库 (DLL) 项目中创建菜单命令

1. 在新的 Visual Studio 解决方案或现有解决方案中创建类库项目。

   1. 在“文件” 菜单上，选择“新建”、“项目”。

   2. 在“已安装的模板”下，选择 “Visual C#”或“Visual Basic”。 在中间栏中，选择“类库”。

   3. 设置 **“解决方案”** 以指示你是希望创建新的解决方案，还是希望向已打开的 VSIX 解决方案添加组件。

   4. 设置项目的名称和位置，然后单击“确定”。

2. 将下列引用添加到项目中。

   |                                                                                                    参考                                                                                                    |                                                                                                  允许执行的操作                                                                                                  |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                                        System.ComponentModel.Composition                                                                                        |                                         通过使用 [Managed Extensibility Framework (MEF)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)定义组件。                                          |
   |                                                                                      Microsoft.VisualStudio.Uml.Interfaces                                                                                      |                                                                                        读取并更改模型元素的属性。                                                                                         |
   |                                                                             Microsoft.VisualStudio.ArchitectureTools.Extensibility                                                                              |                                                                                      在关系图上创建模型元素、修改形状。                                                                                       |
   |                                                                                  Microsoft.VisualStudio.Modeling.Sdk.[版本号]                                                                                  | 定义模型事件处理程序。<br /><br /> 将一系列更改封装到模型中。 有关详细信息，请参阅[使用事务链接 UML 模型更新](../modeling/link-uml-model-updates-by-using-transactions.md)。 |
   |                                                            Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]<br /><br /> （并不总是需要）                                                             |                                                                                   访问笔势处理程序的其他关系图元素。                                                                                   |
   | Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer<br /><br /> 仅层关系图上的命令需要。 有关详细信息，请参阅[扩展层关系图](../modeling/extend-layer-diagrams.md)。 |                                                                                             在层关系图上定义命令。                                                                                              |

3. 将类文件添加到项目中，并将其内容设置为下面的代码。

   > [!NOTE]
   > 根据你的喜好更改 `Text` 返回的命名空间、类名和值。
   >
   >  如果定义多个命令，它们将按类名的字母顺序出现在菜单上。

   ```
   using System.ComponentModel.Composition;
   using System.Linq;
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
   using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
   using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;
   using Microsoft.VisualStudio.Uml.Classes;
       // ADD other UML namespaces if required

   namespace UMLmenu1 // CHANGE
   {
     // DELETE any of these attributes if the command
     // should not appear in some types of diagram.
     [ClassDesignerExtension]
     [ActivityDesignerExtension]
     [ComponentDesignerExtension]
     [SequenceDesignerExtension]
     [UseCaseDesignerExtension]
     // [LayerDesignerExtension]

     // All menu commands must export ICommandExtension:
     [Export (typeof(ICommandExtension))]
     // CHANGE class name – determines order of appearance on menu:
     public class Menu1 : ICommandExtension
     {
       [Import]
       public IDiagramContext DiagramContext { get; set; }

       public void QueryStatus(IMenuCommand command)
       { // Set command.Visible or command.Enabled to false
         // to disable the menu command.
         command.Visible = command.Enabled = true;
       }

       public string Text
       {
         get { return "MENU COMMAND LABEL"; }
       }

       public void Execute(IMenuCommand command)
       {
         // A selection of starting points:
         IDiagram diagram = this.DiagramContext.CurrentDiagram;
         foreach (IShape<IElement> shape in diagram.GetSelectedShapes<IElement>())
         { IElement element = shape.Element; }
         IModelStore modelStore = diagram.ModelStore;
         IModel model = modelStore.Root;
         foreach (IElement element in modelStore.AllInstances<IClass>())
         { }
       }
     }
   }
   ```

    有关要在方法中放置的内容的详细信息，请参阅 [实现菜单命令](#Implementing)。

   你必须将菜单命令添加到一个充当命令安装容器的 VSIX 项目中。 如果需要，可以将其他组件包括在同一 VSIX 中。

#### <a name="to-add-a-menu-command-to-a-vsix-project"></a>若要向 VSIX 项目中添加一个菜单命令

1. 如果已使用自己的 VSIX 创建了菜单命令，则不需要此过程。

2. 创建一个 VSIX 项目（如果解决方案中已有一个 VSIX 项目，则无需执行此步骤）。

    1. 在“解决方案资源管理器”中，在该解决方案的快捷菜单上依次选择“添加”、“新建项目”。

    2. 在“已安装的模板”下，展开 “Visual C#”或“Visual Basic”，然后选择“扩展性”。 在中间栏中，选择“VSIX 项目”。

3. 在“解决方案资源管理器”中，在该 VSIX 项目的快捷菜单上选择“设为启动项目”。

4. 打开 **source.extension.vsixmanifest**。

    1. 在“元数据” 选项卡上，设置 VSIX 的名称。

    2. 在“安装目标” 选项卡上，将 Visual Studio 版本设置为目标。

    3. 在“资产” 选项卡上，选择“新建”，并在对话框中进行如下设置：

         **类型** = **MEF 组件**

          = **当前解决方案中的项目**

          = *你的类库项目*

## <a name="Implementing"></a>实现菜单命令
 该菜单命令类为 <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> 实现所需的方法。

|||
|-|-|
|`string Text { get; }`|返回菜单项的标签。|
|`void QueryStatus(IMenuCommand command);`|当用户在关系图中右击时调用。<br /><br /> 此方法不应更改模型。<br /><br /> 使用 `DiagramContext.CurrentDiagram.SelectedShapes` 确定是否显示并启用该命令。<br /><br /> 设置：<br /><br /> 如果用户在关系图中右键单击时该命令必须出现在菜单中，-    `command.Visible` `true`<br />如果用户可以单击菜单中的命令，则 -    `command.Enabled` `true`<br />-    `command.Text` 动态设置菜单标签|
|`void Execute (IMenuCommand command);`|当用户单击菜单项（如果它可见并已启用）时调用。|

### <a name="accessing-the-model-in-code"></a>访问代码中的模型
 在菜单命令类中包括以下声明：

```
[Import] public IDiagramContext DiagramContext { get; set; }
```

 ...

 `IDiagramContext` 的声明允许你在方法中编写可访问关系图、当前选定内容和模型的代码：

```
IDiagram diagram = this.DiagramContext.CurrentDiagram;
foreach (IShape<IElement> shape in diagram.GetSelectedShapes<IElement>())
{ IElement element = shape.Element; ... }
IModelStore modelStore = diagram.ModelStore;
IModel model = modelStore.Root;
foreach (IElement element in modelStore.AllInstances<IUseCase>()) {...}
```

### <a name="navigating-and-updating-the-model"></a>导航和更新模型
 可通过 API 获得 UML 模型的所有元素。 可以从当前选定内容或模型的根中访问所有其他元素。 有关详细信息，请参阅[导航 uml 模型](../modeling/navigate-the-uml-model.md)和[用 uml API 编程](../modeling/programming-with-the-uml-api.md)。

 如果处理的是序列图，另请参阅[使用 UML API 编辑 uml 序列图](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)。

 还可以利用 API 执行以下操作：更改元素的属性、删除元素和关系以及创建新的元素和关系。

 默认情况下，将在单独的事务中执行你在 Execute 方法中所做的每项更改。 用户将能够单独撤消每项更改。 如果要将更改分组到单个事务中，请使用 "[使用事务链接 UML 模型更新](../modeling/link-uml-model-updates-by-using-transactions.md)" 中所述的 <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ILinkedUndoTransaction>。

### <a name="use-the-ui-thread-for-updates"></a>使用 UI 线程进行更新
 在某些情况下，从后台线程对模型进行更新会很有用。 例如，如果你的命令从速度较慢的资源加载数据，则可以在后台线程中执行加载，以便用户能够查看正在进行的更改，并在必要时取消该操作。

 但请注意，该模型库并不是线程安全的。 应始终使用用户界面 (UI) 线程进行更新，如果可能，应阻止用户在后台操作正在进行的过程中执行编辑。 有关示例，请参阅[从后台线程更新 UML 模型](../modeling/update-a-uml-model-from-a-background-thread.md)。

## <a name="Executing"></a>执行菜单命令
 出于测试目的，在调试模式下执行命令。

#### <a name="to-test-the-menu-command"></a>测试菜单命令

1. 按“F5”，或在“调试” 菜单上，选择“开始调试”。

     此时将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。

     **疑难解答**：如果新的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 未启动：

    - 如果你有多个项目，请确保将 VSIX 项目设置为解决方案的启动项目。

    - 在“解决方案资源管理器”中，在启动或唯一项目的快捷菜单上选择“属性”。 在项目属性编辑器中，选择 "**调试**" 选项卡。请确保 "**启动外部程序**" 字段中的字符串是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的完整路径名，通常为：

         `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`

2. 在实验性 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中，打开或创建一个建模项目，然后打开或创建一个建模图。 使用属于菜单命令类的特性中列出的某个类型的关系图。

3. 在关系图上的任意位置打开快捷菜单。 你的命令应出现在菜单中。

     **故障排除**：如果菜单上没有该命令，请确保：

    - 该菜单命令项目作为一个 MEF 组件在 “资产”选项卡中列出，该选项卡位于 VSIX 项目的 **source.extensions.manifest** 中。

    - `Import` 和 `Export` 特性的参数有效。

    - @No__t_0 方法未设置 `command`。`Enabled` 或 `Visible` 要 `false` 的字段。

    - 正在使用的模型关系图的类型（UML 类、序列等）作为菜单命令类特性（ `[ClassDesignerExtension]`、 `[SequenceDesignerExtension]` 等）之一列出。

## <a name="Installing"></a>安装和卸载扩展
 你可以在自己的计算机和其他计算机上安装 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展。

#### <a name="to-install-an-extension"></a>若要安装扩展

1. 在你的计算机中，找到由 VSIX 项目生成的 **.vsix** 文件。

    1. 在“解决方案资源管理器”中，在 VSIX 项目的快捷菜单上，选择“在 Windows 资源管理器中打开文件夹”。

    2. **@No__t_2 \\** _项目_**中**查找文件 bin \\

2. 将 **.vsix** 文件复制到要安装该扩展的目标计算机。 该计算机可以是自己的计算机或其他计算机。

     目标计算机必须具有你在**source.extension.vsixmanifest**中指定的 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 版本之一。

3. 在目标计算机上，打开 **.vsix** 文件，例如双击打开。

     “” 将会打开并安装扩展。

4. 启动或重启 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]。

#### <a name="to-uninstall-an-extension"></a>若要卸载扩展

1. 在“工具” 菜单上，选择“扩展和更新”。

2. 展开“已安装的扩展”。

3. 选择扩展，然后选择“卸载”。

   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展：

   *% LocalAppData%* **\Local\Microsoft\VisualStudio \\ [version] \Extensions**

## <a name="MenuExample"></a> 示例
 下面的示例演示一个菜单命令的代码，该命令用于交换类图中两个元素的名称。 此代码必须在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展项目中生成，并按前面几节所述进行安装。

```
using System.Collections.Generic; // for IEnumerable
using System.ComponentModel.Composition;
  // for [Import], [Export]
using System.Linq; // for IEnumerable extensions
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
  // for IDiagramContext
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
  // for designer extension attributes
using Microsoft.VisualStudio.Modeling.Diagrams;
  // for ShapeElement
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
  // for IGestureExtension, ICommandExtension, ILinkedUndoContext
using Microsoft.VisualStudio.Uml.Classes;
  // for class diagrams, packages

/// <summary>
/// Extension to swap names of classes in a class diagram.
/// </summary>
namespace SwapClassNames
{
  // Declare the class as an MEF component:
  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  // Add more ExportMetadata attributes to make
  // the command appear on diagrams of other types.
  public class NameSwapper : ICommandExtension
  {
  // MEF required interfaces:
  [Import]
  public IDiagramContext Context { get; set; }
  [Import]
  public ILinkedUndoContext LinkedUndoContext { get; set; }

  /// <summary>
  /// Swap the names of the currently selected elements.
  /// </summary>
  /// <param name="command"></param>
  public void Execute(IMenuCommand command)
  {
    // Get selected shapes that are IClassifiers -
    // IClasses, IInterfaces, IEnumerators.
    var selectedShapes = Context.CurrentDiagram
     .GetSelectedShapes<IClassifier>();
    if (selectedShapes.Count() < 2) return;

    // Get model elements displayed by shapes.
    IClassifier firstElement = selectedShapes.First().Element;
    IClassifier lastElement = selectedShapes.Last().Element;

    // Do the swap in a transaction so that user
    // cannot undo one change without the other.
    using (ILinkedUndoTransaction transaction =
    LinkedUndoContext.BeginTransaction("Swap names"))
    {
    string firstName = firstElement.Name;
    firstElement.Name = lastElement.Name;
    lastElement.Name = firstName;
    transaction.Commit();
    }
  }

  /// <summary>
  /// Called by Visual Studio to determine whether
  /// menu item should be visible and enabled.
  /// </summary>
  public void QueryStatus(IMenuCommand command)
  {
    int selectedClassifiers = Context.CurrentDiagram
     .GetSelectedShapes<IClassifier>().Count();
    command.Visible = selectedClassifiers > 0;
    command.Enabled = selectedClassifiers == 2;
  }

  /// <summary>
  /// Name of the menu command.
  /// </summary>
  public string Text
  {
    get { return "Swap Names"; }
  }
  }

}
```

## <a name="see-also"></a>请参阅
 [定义和安装建模扩展](../modeling/define-and-install-a-modeling-extension.md)[扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)[在建模图上定义笔势处理程序](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)定义[自定义建模工具箱项](../modeling/define-a-custom-modeling-toolbox-item.md)定义[UML 模型编辑的验证约束](../modeling/define-validation-constraints-for-uml-models.md) [使用 uml API](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md) [编程和 uml api](../modeling/programming-with-the-uml-api.md)的 uml 序列图[示例：用于对齐 uml 关系图上的形状的命令](http://go.microsoft.com/fwlink/?LinkID=213809)
