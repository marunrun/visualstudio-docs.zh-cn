---
title: 在建模图上定义笔势处理程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, double-click
- UML - extending, drag and drop
ms.assetid: e5e1d70a-3539-4321-a3b1-89e86e4d6430
caps.latest.revision: 36
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3da0988316f54b75cb8076b1f242280a71d9a624
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67890483"
---
# <a name="define-a-gesture-handler-on-a-modeling-diagram"></a>在建模图上定义笔势处理程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可以定义当用户双击项或将项拖动到 UML 关系图上时将执行的命令。 可以将这些扩展打包到 Visual Studio 集成扩展 ([VSIX](http://go.microsoft.com/fwlink/?LinkId=160780)) 中，并将其分发给其他 Visual Studio 用户。  
  
 如果已存在针对要拖动的关系图类型和元素类型的内置行为，则可能无法添加或重写此行为。  
  
## <a name="requirements"></a>要求  
 请参阅 [要求](../modeling/extend-uml-models-and-diagrams.md#Requirements)。  
  
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
## <a name="creating-a-gesture-handler"></a>创建笔势处理程序  
 若要为 UML 设计器定义一个笔势处理程序，必须创建一个定义该笔势处理程序的行为的类，并将此类嵌入到 Visual Studio 集成扩展 (VSIX) 中。 VSIX 用作可安装该处理程序的容器。 以下是定义笔势处理程序的两种替代方法：  
  
- **在使用项目模板其自身 VSIX 中创建笔势处理程序。** 此方法更快。 如果你不希望将处理程序与其他类型的扩展（如验证扩展、自定义工具箱项或菜单命令）合并，则可以使用此方法。  
  
- **创建单独的笔势处理程序和 VSIX 项目。** 如果希望将多种类型的扩展组合到同一个 VSIX 中，可以采用此方法。 例如，如果笔势处理程序需要模型遵守特定约束，则可以将笔势处理程序嵌入到验证方法所在的 VSIX 中。  
  
#### <a name="to-create-a-gesture-handler-in-its-own-vsix"></a>要在笔势处理程序自己的 VSIX 中创建它  
  
1. 在“新建项目”  对话框中的“建模项目”  下，选择“笔势扩展”  。  
  
2. 在新项目中打开 **.cs** 文件并修改 `GestureExtension` 类，以实现笔势处理程序。  
  
    有关详细信息，请参阅 [实现笔势处理程序](#Implementing)。  
  
3. 按 F5 测试笔势处理程序。 有关详细信息，请参阅 [执行笔势处理程序](#Executing)。  
  
4. 在另一台计算机上安装笔势处理程序，通过将文件复制**bin\\\*\\\*.vsix**生成的项目。 有关详细信息，请参阅 [安装和卸载扩展](#Installing)。  
  
   下面是替代过程：  
  
#### <a name="to-create-a-separate-class-library-dll-project-for-the-gesture-handler"></a>要为笔势处理程序创建一个单独的类库 (dll) 项目  
  
1. 在新的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案或现有解决方案中创建类库项目。  
  
   1. 在“文件”  菜单上，选择“新建”  、“项目”  。  
  
   2. 在“已安装的模板”  下，展开“Visual C#”  或“Visual Basic”  ，然后在中间栏中选择“类库”  。  
  
2. 将下列引用添加到项目中。  
  
    `Microsoft.VisualStudio.Modeling.Sdk.[version]`  
  
    `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]`  
  
    `Microsoft.VisualStudio.ArchitectureTools.Extensibility`  
  
    `Microsoft.VisualStudio.Uml.Interfaces`  
  
    `System.ComponentModel.Composition`  
  
    `System.Windows.Forms`  
  
    `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer` – 仅当扩展层关系图时才需要此项。 有关详细信息，请参阅[扩展层关系图](../modeling/extend-layer-diagrams.md)。  
  
3. 将类文件添加到项目中，并将其内容设置为下面的代码。  
  
   > [!NOTE]
   > 根据你的偏好更改命名空间和类名。  
  
   ```  
   using System.ComponentModel.Composition;  
   using System.Linq;  
   using System.Collections.Generic;  
   using Microsoft.VisualStudio.Modeling.Diagrams;  
   using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;  
   using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
   using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
   using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;  
   using Microsoft.VisualStudio.Modeling;  
   using Microsoft.VisualStudio.Uml.Classes;  
   // ADD other UML namespaces if required  
  
   namespace MyGestureHandler // CHANGE  
   {  
     // DELETE any of these attributes if the handler  
     // should not work with some types of diagram.  
     [ClassDesignerExtension]  
     [ActivityDesignerExtension]  
     [ComponentDesignerExtension]  
     [SequenceDesignerExtension]  
     [UseCaseDesignerExtension]  
     // [LayerDesignerExtension]  
  
     // Gesture handlers must export IGestureExtension:  
     [Export(typeof(IGestureExtension))]  
     // CHANGE class name  
     public class MyGesture1 : IGestureExtension  
     {  
       [Import]  
       public IDiagramContext DiagramContext { get; set; }  
  
       /// <summary>  
       /// Called when the user double-clicks on the diagram  
       /// </summary>  
       /// <param name="targetElement"></param>  
       /// <param name="diagramPointEventArgs"></param>  
       public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)  
       {  
         // CHANGE THIS CODE FOR YOUR APPLICATION.  
  
         // Get the target shape, if any. Null if the target is the diagram.  
         IShape targetIShape = targetElement.CreateIShape();  
  
         // Do something...  
       }  
  
       /// <summary>  
       /// Called repeatedly when the user drags from anywhere on the screen.  
       /// Return value should indicate whether a drop here is allowed.  
       /// </summary>  
       /// <param name="targetMergeElement">References the element to be dropped on.</param>  
       /// <param name="diagramDragEventArgs">References the element to be dropped.</param>  
       /// <returns></returns>  
       public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)  
       {  
         // CHANGE THIS CODE FOR YOUR APPLICATION.  
  
         // Get the target element, if any. Null if the target is the diagram.  
         IShape targetIShape = targetMergeElement.CreateIShape();  
  
         // This example allows drag of any UML elements.  
         return GetModelElementsFromDragEvent(diagramDragEventArgs).Count() > 0;  
       }  
  
       /// <summary>  
       /// Execute the action to be performed on the drop.  
       /// </summary>  
       /// <param name="targetDropElement"></param>  
       /// <param name="diagramDragEventArgs"></param>  
       public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)  
       {  
         // CHANGE THIS CODE FOR YOUR APPLICATION.  
       }  
  
       /// <summary>  
       /// Retrieves UML IElements from drag arguments.  
       /// Works for drags from UML diagrams.  
       /// </summary>  
       private IEnumerable<IElement> GetModelElementsFromDragEvent  
               (DiagramDragEventArgs dragEvent)  
       {  
         //ElementGroupPrototype is the container for  
         //dragged and copied elements and toolbox items.  
         ElementGroupPrototype prototype =  
            dragEvent.Data.  
            GetData(typeof(ElementGroupPrototype))  
                 as ElementGroupPrototype;  
         // Locate the originals in the implementation store.  
         IElementDirectory implementationDirectory =  
            dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;  
  
         return prototype.ProtoElements.Select(  
           prototypeElement =>  
           {  
             ModelElement element = implementationDirectory  
               .FindElement(prototypeElement.ElementId);  
             ShapeElement shapeElement = element as ShapeElement;  
             if (shapeElement != null)  
             {  
               // Dragged from a diagram.  
               return shapeElement.ModelElement as IElement;  
             }  
             else  
             {  
               // Dragged from UML Model Explorer.  
               return element as IElement;  
             }  
           });  
       }  
  
     }  
   }  
  
   ```  
  
    有关要在方法中放置的内容的详细信息，请参阅 [实现笔势处理程序](#Implementing)。  
  
   你必须将菜单命令添加到一个充当命令安装容器的 VSIX 项目中。 如果需要，可以将其他组件包括在同一 VSIX 中。  
  
#### <a name="to-add-a-separate-gesture-handler-to-a-vsix-project"></a>将单独的笔势处理程序添加到 VSIX 项目  
  
1. 如果已创建了自带 VSIX 的笔势处理程序，则不需要此过程。  
  
2. 创建一个 VSIX 项目（如果解决方案中已有一个 VSIX 项目，则无需执行此步骤）。  
  
    1. 在“解决方案资源管理器”  中，在该解决方案的快捷菜单上依次选择“添加”  、“新建项目”  。  
  
    2. 在“已安装的模板”  下，展开“Visual C#”  或“Visual Basic”  ，然后选择“扩展性”  。 在中间栏中，选择“VSIX 项目”  。  
  
3. 将 VSIX 项目设置为解决方案的启动项目。  
  
    - 在解决方案资源管理器中，在该 VSIX 项目的快捷菜单上选择“设为启动项目”  。  
  
4. 在 **source.extension.vsixmanifest**中，将笔势处理程序类库项目添加为 MEF 组件：  
  
    1. 在“元数据”  选项卡上，设置 VSIX 的名称。  
  
    2. 在“安装目标”  选项卡上，将 Visual Studio 版本设置为目标。  
  
    3. 在“资产”  选项卡上，选择  “新建”，并在对话框中进行如下设置：  
  
         **类型** = **MEF 组件**  
  
          = **当前解决方案中的项目**   
  
           = *你的类库项目*  
  
## <a name="Executing"></a> 执行笔势处理程序  
 出于测试目的，在调试模式下执行笔势处理程序。  
  
#### <a name="to-test-the-gesture-handler"></a>要测试笔势处理程序  
  
1. 按“F5”  ，或在“调试”  菜单上，单击“开始调试”  。  
  
    此时将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。  
  
    **故障排除**:如果新[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]不会启动：  
  
   - 如果你有多个项目，请确保将 VSIX 项目设置为解决方案的启动项目。  
  
   - 在“解决方案资源管理器”中，在“启动”或“仅项目”的快捷菜单上选择“属性”。 在项目属性编辑器中，选择“调试”  选项卡。请确保“启动外部程序”  字段中的字符串是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的完整路径名，通常为：  
  
        `C:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\devenv.exe`  
  
2. 在实验性 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中，打开或创建一个建模项目，然后打开或创建一个建模图。 使用属于笔势处理程序类的特性中列出的某个类型的关系图。  
  
3. 在关系图上的任意位置双击。 应调用你的双击处理程序。  
  
4. 将一个元素从 UML 资源管理器拖动到关系图上。 应调用你的拖动处理程序。  
  
   **故障排除**:如果笔势处理程序不起作用，请确保：  
  
- 该笔势处理程序项目作为一个 MEF 组件在“资产”  选项卡中列出，该选项卡位于 VSIX 项目的 **source.extensions.manifest** 中。  
  
- 所有 `Import` 和 `Export` 特性的参数都有效。  
  
- `CanDragDrop` 方法未返回 `false`。  
  
- 正在使用的模型图的类型（UML 类、序列等）作为笔势处理程序类特性（[ClassDesignerExtension] 和 [SequenceDesignerExtension] 等）之一列出。  
  
- 尚未为此类型的目标和放置的元素定义内置功能。  
  
## <a name="Implementing"></a> 实现笔势处理程序  
  
### <a name="the-gesture-handler-methods"></a>笔势处理程序方法  
 笔势处理程序类实现并导出 <xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement.IGestureExtension>。 以下是需要定义的方法：  
  
|||  
|-|-|  
|`bool CanDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|返回 `true` 将允许要在此目标上放置的 `dragEvent` 引用源元素。<br /><br /> 此方法不应更改模型。 由于此方法是用于在用户移动鼠标时确定箭头状态，因此它应快速工作。|  
|`void OnDragDrop (ShapeElement target, DiagramDragEventArgs dragEvent)`|基于目标和在 `dragEvent`中引用的源对象来更新模型。<br /><br /> 当用户在拖动后释放鼠标时调用。|  
|`void OnDoubleClick (ShapeElement target, DiagramPointEventArgs pointEvent)`|`target` 是用户双击的形状。|  
  
 可以编写可接受 UML 以及各种其他项（如文件、.NET 类视图中的节点等）的处理程序。 用户可将这些项中的任意项拖动到 UML 关系图上，前提是编写了可对这些项的序列化格式进行解码的 `OnDragDrop` 方法。 解码方法因项的类型而异。  
  
 这些方法的参数包括：  
  
- `ShapeElement target`。 用户已将某项拖动到其上的形状或关系图。  
  
    `ShapeElement` 是作为 UML 建模工具的基础的实现中的一个类。 为降低使 UML 模型和关系图处于不一致状态的风险，建议你不要直接使用此类的方法。 相反，包装中的元素`IShape`，然后使用中所述的方法[关系图上显示 UML 模型](../modeling/display-a-uml-model-on-diagrams.md)。  

  - 要获取 `IShape`：  

      ```  
      IShape targetIShape = target.CreateIShape(target);  
      ```  

  - 要获取拖动或双击操作的目标模型元素：  

      ```  
      IElement target = targetIShape.Element;  
      ```  

      可将此元素强制转换为一个更明确的元素类型。  

  - 要获取包含 UML 模型的 UML 模型存储区：  

      ```  
      IModelStore modelStore =   
        targetIShape.Element.GetModelStore();   
      ```  

  - 要获取对主机和服务提供程序的访问权限：  

      ```  
      target.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE  
      ```  
  
- `DiagramDragEventArgs eventArgs`。 此参数传送拖动操作的源对象的序列化格式：  
  
    ```  
    System.Windows.Forms.IDataObject data = eventArgs.Data;    
    ```  
  
     可从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的不同部分或从 Windows 桌面将许多不同类型的元素拖动到关系图上。 在 `IDataObject`中按照不同的方式对不同类型的元素进行编码。 若要从其中提取元素，请参考相应类型对象的文档。  
  
     如果源对象是从 UML 模型资源管理器或另一个 UML 关系图拖动的 UML 元素，请参阅[从 IDataObject 获取 UML 模型元素](../modeling/get-uml-model-elements-from-idataobject.md)。  
  
### <a name="writing-the-code-of-the-methods"></a>编写方法的代码  
 有关编写代码以读取和更新模型的详细信息，请参阅 [Programming with the UML API](../modeling/programming-with-the-uml-api.md)。  
  
 有关访问拖动操作中的模型信息的信息，请参阅[从 IDataObject 获取 UML 模型元素](../modeling/get-uml-model-elements-from-idataobject.md)。  
  
 如果处理的序列图，另请参阅[通过使用 UML API 编辑 UML 序列图](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)。  
  
 除了这些方法的参数之外，你还可以在提供对当前关系图和模型的访问权限的类中声明一个导入属性。  
  
```  
[Import] public IDiagramContext DiagramContext { get; set; }  
```  
  
 `IDiagramContext` 的声明允许你在方法中编写可访问关系图、当前选定内容和模型的代码：  
  
```  
IDiagram diagram = this.DiagramContext.CurrentDiagram;  
foreach (IShape<IElement> shape in diagram.GetSelectedShapes<IElement>)  
{ IElement element = shape.Element; ... }  
IModelStore modelStore = diagram.ModelStore;  
IModel model = modelStore.Root;  
foreach (IDiagram diagram in modelStore.Diagrams) {...}  
foreach (IElement element in modelStore.AllInstances<IUseCase>) {...}  
```  
  
 有关详细信息，请参阅[导航 UML 模型](../modeling/navigate-the-uml-model.md)。  
  
## <a name="Installing"></a> 安装和卸载扩展  
 你可以在自己的计算机和其他计算机上安装 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展。  
  
#### <a name="to-install-an-extension"></a>若要安装扩展  
  
1. 在你的计算机中，找到由 VSIX 项目生成的 **.vsix** 文件。  
  
    1. 在“解决方案资源管理器”  中，在 VSIX 项目的快捷菜单上，选择“在 Windows 资源管理器中打开文件夹”  。  
  
    2. 找到的文件**bin\\\*\\** _YourProject_ **.vsix**  
  
2. 将 **.vsix** 文件复制到要安装该扩展的目标计算机。 该计算机可以是自己的计算机或其他计算机。  
  
     目标计算机必须具有的版本之一[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]中指定**source.extension.vsixmanifest**。  
  
3. 在目标计算机上，打开 **.vsix** 文件。  
  
     “”  将会打开并安装扩展。  
  
4. 启动或重启 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]。  
  
#### <a name="to-uninstall-an-extension"></a>若要卸载扩展  
  
1. 在“工具”  菜单上，选择“扩展和更新”  。  
  
2. 展开“已安装的扩展”  。  
  
3. 选择扩展，然后选择“卸载”  。  
  
   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展：  
  
   *%LocalAppData%* **\Local\Microsoft\VisualStudio\\[version]\Extensions**  
  
## <a name="DragExample"></a> 示例  
 下面的示例演示如何在序列图中基于从组件图中拖动的组件的部件和端口来创建生命线。  
  
 若要对其进行测试，请按 F5。 这将打开一个 Visual Studio 实验实例。 在此实例中，打开 UML 模型并在组件图上创建一个组件。 向该组件添加一些接口和内部组件部件。 选择接口和部件。 然后，将接口和部件拖动到序列图上。 （从组件图向上拖动到序列图的选项卡，然后向下拖动到序列图中。）将为每个接口和部件显示一条生命线。  
  
 有关将交互绑定到序列图的详细信息，请参阅[通过使用 UML API 编辑 UML 序列图](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md)。  
  
```  
using System.Collections.Generic;  
using System.ComponentModel.Composition;  
using System.Linq;  
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;  
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
using Microsoft.VisualStudio.Uml.AuxiliaryConstructs;  
using Microsoft.VisualStudio.Uml.Classes;  
using Microsoft.VisualStudio.Uml.Interactions;  
using Microsoft.VisualStudio.Uml.CompositeStructures;  
using Microsoft.VisualStudio.Uml.Components;  
  
/// <summary>  
/// Creates lifelines from component ports and parts.  
/// </summary>  
[Export(typeof(IGestureExtension))]  
[SequenceDesignerExtension]  
public class CreateLifelinesFromComponentParts : IGestureExtension  
{  
  [Import]  
  public IDiagramContext Context { get; set; }  
  
  /// <summary>  
  /// Called by the modeling framework when  
  /// the user drops something on a target.  
  /// </summary>  
  /// <param name="target">The target shape or diagram </param>  
  /// <param name="dragEvent">The item being dragged</param>  
  public void OnDragDrop(ShapeElement target,  
           DiagramDragEventArgs dragEvent)  
  {  
    ISequenceDiagram diagram = Context.CurrentDiagram  
            as ISequenceDiagram;  
    IInteraction interaction = diagram.Interaction;  
    if (interaction == null)  
    {  
      // Sequence diagram is empty: create an interaction.  
      interaction = diagram.ModelStore.Root.CreateInteraction();  
      interaction.Name = Context.CurrentDiagram.Name;  
      diagram.Bind(interaction);  
    }  
    foreach (IConnectableElement connectable in  
       GetConnectablesFromDrag(dragEvent))  
    {  
      ILifeline lifeline = interaction.CreateLifeline();  
      lifeline.Represents = connectable;  
      lifeline.Name = connectable.Name;  
    }  
  }  
  
  /// <summary>  
  /// Called by the modeling framework to determine whether  
  /// the user can drop something on a target.  
  /// Must not change anything.  
  /// </summary>  
  /// <param name="target">The target shape or diagram</param>  
  /// <param name="dragEvent">The item being dragged</param>  
  /// <returns>true if this item can be dropped on this target</returns>  
  public bool CanDragDrop(ShapeElement target,  
           DiagramDragEventArgs dragEvent)  
  {  
    IEnumerable<IConnectableElement> connectables = GetConnectablesFromDrag(dragEvent);  
    return connectables.Count() > 0;  
  }  
  
  ///<summary>  
  /// Get dragged parts and ports of an IComponent.  
  ///</summary>  
  private IEnumerable<IConnectableElement>  
    GetConnectablesFromDrag(DiagramDragEventArgs dragEvent)  
  {  
    foreach (IElement element in  
      GetModelElementsFromDragEvent(dragEvent))  
    {  
      IConnectableElement part = element as IConnectableElement;  
      if (part != null)  
      {  
        yield return part;  
      }  
    }  
  }  
  
  /// <summary>  
  /// Retrieves UML IElements from drag arguments.  
  /// Works for drags from UML diagrams.  
  /// </summary>  
  private IEnumerable<IElement> GetModelElementsFromDragEvent  
          (DiagramDragEventArgs dragEvent)  
  {  
    //ElementGroupPrototype is the container for  
    //dragged and copied elements and toolbox items.  
    ElementGroupPrototype prototype =  
       dragEvent.Data.  
       GetData(typeof(ElementGroupPrototype))  
            as ElementGroupPrototype;  
    // Locate the originals in the implementation store.  
    IElementDirectory implementationDirectory =  
       dragEvent.DiagramClientView.Diagram.Store.ElementDirectory;  
  
    return prototype.ProtoElements.Select(  
      prototypeElement =>  
      {  
        ModelElement element = implementationDirectory  
          .FindElement(prototypeElement.ElementId);  
        ShapeElement shapeElement = element as ShapeElement;  
        if (shapeElement != null)  
        {  
          // Dragged from a diagram.  
          return shapeElement.ModelElement as IElement;  
        }  
        else  
        {  
          // Dragged from UML Model Explorer.  
          return element as IElement;  
        }  
      });  
  }  
  
  public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)  
  {  
  }  
}  
  
```  
  
 代码`GetModelElementsFromDragEvent()`中所述[从 IDataObject 获取 UML 模型元素](../modeling/get-uml-model-elements-from-idataobject.md)。  
  
## <a name="see-also"></a>请参阅  
 [定义和安装建模扩展](../modeling/define-and-install-a-modeling-extension.md)   
 [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)   
 [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)   
 [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)
