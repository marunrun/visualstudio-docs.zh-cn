---
title: 如何：添加拖放处理程序
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b15e0d305140e6e04464091df59432a2cd261796
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821943"
---
# <a name="how-to-add-a-drag-and-drop-handler"></a>如何：添加拖放处理程序

可以对你的 DSL，添加拖放事件的处理程序，以便用户可以将项拖到关系图上从其他关系图或从 Visual Studio 的其他部分。 还可以添加诸如双击事件的处理程序。 拖放和双击处理程序在一起，称为*笔势处理程序*。

本主题讨论了在其他关系图上发起的拖放笔势。 对于单个关系图内的移动和复制事件，请考虑另一种方法：定义 `ElementOperations` 的子类。 有关详细信息，请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。 你可能还可以自定义 DSL 定义。

## <a name="defining-gesture-handlers-by-overriding-shapeelement-methods"></a>通过重写 ShapeElement 方法定义笔势处理程序

`OnDragDrop`、`OnDoubleClick`、`OnDragOver` 以及其他可以进行重写的方法。

将新的代码文件添加到 DSL 项目。 对于笔势处理程序，通常必须至少具有以下 `using` 语句：

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using System.Linq;
```

在新文件中，为应响应拖动操作的形状或关系图类定义分部类。 重写以下方法：

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDragOver%2A> - 当鼠标指针在拖动操作期间进入该形状时调用此方法。 你的方法应检查用户正在拖动的项，并设置“效果”属性以指示用户是否可以将项放置在此形状上。 “效果”属性确定当指针悬停在此形状上时指针的外观，还确定当用户释放鼠标按钮时是否将调用 `OnDragDrop()`。

    ```csharp
    partial class MyShape // MyShape generated from DSL Definition.
    {
        public override void OnDragOver(DiagramDragEventArgs e)
        {
          base.OnDragOver(e);
          if (e.Effect == System.Windows.Forms.DragDropEffects.None
               && IsAcceptableDropItem(e)) // To be defined
          {
            e.Effect = System.Windows.Forms.DragDropEffects.Copy;
          }
        }
    ```

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDragDrop%2A> -如果用户释放鼠标按钮时鼠标指针停留在此形状或关系图中，如果调用此方法`OnDragOver(DiagramDragEventArgs e)`之前设置`e.Effect`以外的值为`None`。

    ```csharp
    public override void OnDragDrop(DiagramDragEventArgs e)
    {
          if (!IsAcceptableDropItem(e))
          {
            base.OnDragDrop(e);
          }
          else
          { // Process the dragged item, for example merging a copy into the diagram
            ProcessDragDropItem(e); // To be defined
          }
    }
    ```

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDoubleClick%2A> -当用户双击的形状或关系图时，调用此方法。

     有关详细信息，请参阅[如何：截获对形状或修饰器的单击](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)。

定义 `IsAcceptableDropItem(e)` 以确定拖动项是否是可接受的，并定义 ProcessDragDropItem(e) 以在放置该项后更新模型。 这些方法必须先从事件参数中提取项。 有关如何执行该操作的信息，请参阅[如何获取对拖动项的引用](#to-send-an-object-from-a-source-dsl)。

## <a name="define-gesture-handlers-by-using-mef"></a>通过使用 MEF 定义笔势处理程序

如果希望第三方开发人员能够对你的 DSL 定义他们自己的处理程序，则使用此方法。 用户可以在安装了你的 DSL 后选择安装第三方扩展。

MEF (Managed Extensibility Framework) 允许定义可使用最小配置安装的组件。 有关详细信息，请参阅 [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)。

### <a name="to-define-a-mef-gesture-handler"></a>定义 MEF 笔势处理程序

1. 将添加到您**Dsl**并**DslPackage**项目**MefExtension**中所述的文件[使用 MEF 扩展 DSL](../modeling/extend-your-dsl-by-using-mef.md)。

2. 现在可以将笔势处理程序定义为 MEF 组件：

    ```csharp
    // This attribute is defined in the generated file
    // DslPackage\MefExtension\DesignerExtensionMetaDataAttribute.cs:
    [MyDslGestureExtension]
    public class MyGestureHandlerClassName : IGestureExtension
    {
      /// <summary>
      /// Called to determine whether a drag onto the diagram can be accepted.
      /// </summary>
      /// <param name="diagramDragEventArgs">Contains a link to the item that is being dragged</param>
      /// <param name="targetMergeElement">The shape or connector that the mouse is over</param>
      /// <returns>True if the item can be accepted on the targetMergeElement.</returns>
      public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)
      {
        MyShape target = targetMergeElement as MyShape;
        if (target == null) return false;
        if (target.IsAcceptableDropItem(diagramDragEventArgs)) return true;
        return false;
      }
      public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
      {
        MyShape target = targetMergeElement as MyShape;
        if (target == null || ! target.IsAcceptableDropItem(diagramDragEventArgs)) return;
        // Process the dragged item, for example merging a copy into the diagram:
        target.ProcessDragDropItem(diagramDragEventArgs);
     }
    ```

     可创建多个笔势处理程序组件，例如当你具有不同类型的拖动对象时。

3. 添加目标形状、连接符或关系图类的分部类定义，并定义方法 `IsAcceptableDropItem()` 和 `ProcessDragDropItem()`。 必须通过从事件参数中提取拖动项开始使用这些方法。 有关详细信息，请参阅[如何获取对拖动项的引用](#to-send-an-object-from-a-source-dsl)。

## <a name="how-to-decode-the-dragged-item"></a>如何解码拖动项

可以从任何窗口或桌面以及从 DSL 中拖动元素。

当用户将某个项拖动到关系图上，或从关系图的一个部分拖动到另一个部分时，`DiagramDragEventArgs` 中提供了有关正在拖动的项的信息。 由于拖动操作可以开始于屏幕上的任何对象，因此采用任何一种格式的数据都可用。 你的代码必须识别它能够处理的格式。

若要发现拖动源信息可采用的格式，请在调试模式下运行代码，从而在 `OnDragOver()` 或 `CanDragDrop()` 入口设置断点。 检查 `DiagramDragEventArgs` 参数的值。 信息将采用以下两种方式提供：

- <xref:System.Windows.Forms.IDataObject>  `Data` -此属性包含序列化的版本的源对象，通常在多个格式。 其最有用的函数是：

  - diagramEventArgs.Data.GetDataFormats()-列出了可以在其中解码拖动的对象的格式。 例如，如果用户从桌面拖动文件，则可用的格式包括文件名（“`FileNameW`”）。

  - `diagramEventArgs.Data.GetData(format)` -解码拖动的对象中指定的格式。 将该对象转换为相应的类型。 例如:

    `string fileName = diagramEventArgs.Data.GetData("FileNameW") as string;`

    还可以采用自己的自定义格式从源中传输对象（例如模型总线引用）。 有关详细信息，请参阅[如何在拖放发送模型总线引用](#to-send-an-object-from-a-source-dsl)。

- <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> `Prototype` -如果你希望用户从 DSL 或 UML 模型拖动项，则使用此属性。 元素组原型包含一个或多个对象、链接及其属性值。 在粘贴操作中以及要从工具箱添加元素时，也会使用它。 在原型中，对象及其类型由 Guid 标识。 例如，此代码允许用户从 UML 关系图或 UML 模型资源管理器拖动类元素：

    ```csharp
    private bool IsAcceptableDropItem(DiagramDragEventArgs e)
    {
      return e.Prototype != null && e.Prototype.RootProtoElements.Any(element =>
            element.DomainClassId.ToString()
            == "3866d10c-cc4e-438b-b46f-bb24380e1678"); // Accept UML class shapes.
     // Or, from another DSL: SourceNamespace.SourceShapeClass.DomainClassId
    }
    ```

     若要接受 UML 形状，请通过试验确定 UML 形状类的 Guid。 请记住，在任何关系图上通常都有多种类型的元素。 还请记住，从 DSL 或 UML 关系图拖动的对象是形状，而不是模型元素。

`DiagramDragEventArgs` 还具有指示当前鼠标指针位置以及用户是否按下 CTRL、ALT 或 SHIFT 键的属性。

## <a name="how-to-get-the-original-of-a-dragged-element"></a>如何获取拖动元素的原始状态

如果拖动项是 DSL 元素，则可以打开源模型并访问该元素。

事件参数的 `Data` 和 `Prototype` 属性只包含对拖动形状的引用。 通常，如果希望以某种方式在派生自原型的目标 DSL 中创建对象，则需要获取对原始状态的访问权限，例如，读取文件内容或导航到由形状表示的模型元素。 可使用 Visual Studio 模型总线帮助实现此目的。

### <a name="to-prepare-a-dsl-project-for-model-bus"></a>准备用于模型总线的 DSL 项目

确保源 DSL 可由 Visual Studio 模型总线访问：

1. 如果未安装 Visual Studio 模型总线扩展，请下载并安装它。 有关详细信息，请参阅[可视化和建模 SDK](http://go.microsoft.com/fwlink/?LinkID=185579)。

2. 在 DSL 设计器中打开源 DSL 的 DSL 定义文件。 右键单击设计图面，然后单击**启用 Modelbus**。 在该对话框中，选择一个或两个选项。  单击 **“确定”** 。 新项目“ModelBus”随即添加到 DSL 解决方案中。

3. 单击**转换所有模板**重新生成解决方案。

### <a name="to-send-an-object-from-a-source-dsl"></a>从源 DSL 发送对象

1. 在 ElementOperations 子类中，重写 `Copy()`，以便它将模型总线引用 (MBR) 编码到 IDataObject 中。 当用户开始从源关系图进行拖动时，将调用此方法。 当用户在目标关系图中进行放置时，随后在 IDataObject 中提供编码的 MBR。

    ```csharp
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Shell;
    using Microsoft.VisualStudio.Modeling.Diagrams;
    using Microsoft.VisualStudio.Modeling.Integration;
    using Microsoft.VisualStudio.Modeling.Integration.Shell;
    using System.Drawing; // PointF
    using  System.Collections.Generic; // ICollection
    using System.Windows.Forms; // for IDataObject
    ...
    public class MyElementOperations : DesignSurfaceElementOperations
    {
        public override void Copy(System.Windows.Forms.IDataObject data, System.Collections.Generic.ICollection<ModelElement> elements, ClosureType closureType, System.Drawing.PointF sourcePosition)
        {
          base.Copy(data, elements, closureType, sourcePosition);

          // Get the ModelBus service:
          IModelBus modelBus =
              this.Store.GetService(typeof(SModelBus)) as IModelBus;
          DocData docData = ((VSDiagramView)this.Diagram.ActiveDiagramView).DocData;
          string modelFile = docData.FileName;
          // Get an adapterManager for the target DSL:
          ModelBusAdapterManager manager =
              (modelBus.FindAdapterManagers(modelFile).First());
          ModelBusReference modelReference = manager.CreateReference(modelFile);
          ModelBusReference elementReference = null;
          using (ModelBusAdapter adapter = modelBus.CreateAdapter(modelReference))
          {
            elementReference = adapter.GetElementReference(elements.First());
          }

          data.SetData("ModelBusReference", elementReference);
        }
    ...}
    ```

### <a name="to-receive-a-model-bus-reference-from-a-dsl-in-a-target-dsl-or-uml-project"></a>在目标 DSL 或 UML 项目中从 DSL 接收模型总线引用

1. 在目标 DSL 项目中，将项目引用添加到：

    - 源 DSL 项目。

    - 源 ModelBus 项目。

2. 在笔势处理程序代码文件中，添加以下命名空间引用：

    ```csharp
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
    using Microsoft.VisualStudio.Modeling.Diagrams;
    using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
    using Microsoft.VisualStudio.Modeling.Integration;
    using SourceDslNamespace;
    using SourceDslNamespace.ModelBusAdapters;
    ```

3. 以下示例说明了如何获取对源模型元素的访问权限：

    ```csharp
    partial class MyTargetShape // or diagram or connector
    {
      internal void ProcessDragDropItem(DiagramDragEventArgs diagramDragEventArgs)
      {
        // Verify that we're being passed an Object Shape.
        ElementGroupPrototype prototype = diagramDragEventArgs.Prototype;
        if (prototype == null) return;
        if (Company.InstanceDiagrams.ObjectShape.DomainClassId
          != prototype.RootProtoElements.First().DomainClassId)
          return;
        // - This is an ObjectShape.
        // - We need to access the originating Store, find the shape, and get its object.

        IModelBus modelBus = targetDropElement.Store.GetService(typeof(SModelBus)) as IModelBus;

        // Unpack the MBR that was packed in Copy:
        ModelBusReference reference = diagramDragEventArgs.Data.GetData("ModelBusReference") as ModelBusReference;
        using (SourceDslAdapter adapter = modelBus.CreateAdapter(reference) as SourceDslAdapter)
        {
          using (ILinkedUndoTransaction t = LinkedUndoContext.BeginTransaction("doing things"))
          {
            // Quickest way to get the shape from the MBR:
            ObjectShape firstShape = adapter.ResolveElementReference<ObjectShape>(reference);

            // But actually there might be several shapes - so get them from the prototype instead:
            IElementDirectory remoteDirectory = adapter.Store.ElementDirectory;
            foreach (Guid shapeGuid in prototype.SourceRootElementIds)
            {
              PresentationElement pe = remoteDirectory.FindElement(shapeGuid) as PresentationElement;
              if (pe == null) continue;
              SourceElement instance = pe.ModelElement as SourceElement;
              if (instance == null) continue;

              // Do something with the object:
          instance...
            }
            t.Commit();
          }
        }
    }
    ```

### <a name="to-accept-an-element-sourced-from-a-uml-model"></a>接受来源于 UML 模型的元素

- 以下代码示例接受从 UML 关系图拖放的对象。

    ```csharp
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Diagrams;
    using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
    using Microsoft.VisualStudio.Uml.Classes;
    using System;
    using System.ComponentModel.Composition;
    using System.Linq;
    ...
    partial class TargetShape
    {
      internal void ProcessDragDropItem(DiagramDragEventArgs diagramDragEventArgs)
      {
            EnvDTE.DTE dte = this.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE;
            // Find the UML project
            foreach (EnvDTE.Project project in dte.Solution.Projects)
            {
              IModelingProject modelingProject = project as IModelingProject;
              if (modelingProject == null) continue; // not a modeling project
              IModelStore store = modelingProject.Store;
              if (store == null) return;

              foreach (IDiagram dd in store.Diagrams())
              {
                  // Get Modeling.Diagram that implements UML.IDiagram:
                  Diagram diagram = dd.GetObject<Diagram>();

                  foreach (Guid elementId in e.Prototype.SourceRootElementIds)
                  {
                    ShapeElement shape = diagram.Partition.ElementDirectory.FindElement(elementId) as ShapeElement;
                    if (shape == null) continue;
                    // This example assumes the shape is a UML class:
                    IClass classElement = shape.ModelElement as IClass;
                    if (classElement == null) continue;

                    // Now do something with the UML class element ...
                  }
            }
          break; // don't try any more projects
    }  }  }
    ```

## <a name="using-mouse-actions-dragging-compartment-items"></a>使用鼠标操作：拖动隔离舱项

您可以编写在形状的字段截获鼠标操作的处理程序。 下面的示例使用户可以通过使用鼠标拖动对隔离舱中的项重新排序。

若要生成此示例中，创建解决方案，通过使用**类图**解决方案模板。 添加代码文件和以下代码。 将命名空间调整为与你自己的命名空间相同。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Design;
using Microsoft.VisualStudio.Modeling.Diagrams;
using System.Collections.Generic;
using System.Linq;

// This sample allows users to re-order items in a compartment shape by dragging.

// This example is built on the "Class Diagrams" solution template of VMSDK (DSL Tools).
// You will need to change the following domain class names to your own:
// ClassShape = a compartment shape
// ClassModelElement = the domain class displayed using a ClassShape
// This code assumes that the embedding relationships displayed in the compartments
// don't use inheritance (don't have base or derived domain relationships).

namespace Company.CompartmentDrag  // EDIT.
{
 /// <summary>
 /// Manage the mouse while dragging a compartment item.
 /// </summary>
 public class CompartmentDragMouseAction : MouseAction
 {
  private ModelElement sourceChild;
  private ClassShape sourceShape;
  private RectangleD sourceCompartmentBounds;

  public CompartmentDragMouseAction(ModelElement sourceChildElement, ClassShape sourceParentShape, RectangleD bounds)
   : base (sourceParentShape.Diagram)
  {
   sourceChild = sourceChildElement;
   sourceShape = sourceParentShape;
   sourceCompartmentBounds = bounds; // For cursor.
  }

  /// <summary>
  /// Call back to the source shape to drop the dragged item.
  /// </summary>
  /// <param name="e"></param>
  protected override void OnMouseUp(DiagramMouseEventArgs e)
  {
   base.OnMouseUp(e);
   sourceShape.DoMouseUp(sourceChild, e);
   this.Cancel(e.DiagramClientView);
   e.Handled = true;
  }

  /// <summary>
  /// Ideally, this shouldn't happen. This action should only be active
  /// while the mouse is still pressed. However, it can happen if you
  /// move the mouse rapidly out of the source shape, let go, and then
  /// click somewhere else in the source shape. Yuk.
  /// </summary>
  /// <param name="e"></param>
  protected override void OnMouseDown(DiagramMouseEventArgs e)
  {
   base.OnMouseDown(e);
   this.Cancel(e.DiagramClientView);
   e.Handled = false;
  }

  /// <summary>
  /// Display an appropriate cursor while the drag is in progress:
  /// Up-down arrow if we are inside the original compartment.
  /// No entry if we are elsewhere.
  /// </summary>
  /// <param name="currentCursor"></param>
  /// <param name="diagramClientView"></param>
  /// <param name="mousePosition"></param>
  /// <returns></returns>
  public override System.Windows.Forms.Cursor GetCursor(System.Windows.Forms.Cursor currentCursor, DiagramClientView diagramClientView, PointD mousePosition)
  {
   // If the cursor is inside the original compartment, show up-down cursor.
   return sourceCompartmentBounds.Contains(mousePosition)
    ? System.Windows.Forms.Cursors.SizeNS // Up-down arrow.
    : System.Windows.Forms.Cursors.No;
  }
 }

 /// <summary>
 /// Override some methods of the compartment shape.
 /// *** GenerateDoubleDerived must be set for this shape in DslDefinition.dsl. ****
 /// </summary>
 public partial class ClassShape
 {
  /// <summary>
  /// Model element that is being dragged.
  /// </summary>
  private static ClassModelElement dragStartElement = null;
  /// <summary>
  /// Absolute bounds of the compartment, used to set the cursor.
  /// </summary>
  private static RectangleD compartmentBounds;

  /// <summary>
  /// Attach mouse listeners to the compartments for the shape.
  /// This is called once per compartment shape.
  /// The base method creates the compartments for this shape.
  /// </summary>
  public override void EnsureCompartments()
  {
   base.EnsureCompartments();
   foreach (Compartment compartment in this.NestedChildShapes.OfType<Compartment>())
   {
    compartment.MouseDown += new DiagramMouseEventHandler(compartment_MouseDown);
    compartment.MouseUp += new DiagramMouseEventHandler(compartment_MouseUp);
    compartment.MouseMove += new DiagramMouseEventHandler(compartment_MouseMove);
   }
  }

  /// <summary>
  /// Remember which item the mouse was dragged from.
  /// We don't create an Action immediately, as this would inhibit the
  /// inline text editing feature. Instead, we just remember the details
  /// and will create an Action when/if the mouse moves off this list item.
  /// </summary>
  /// <param name="sender"></param>
  /// <param name="e"></param>
  void compartment_MouseDown(object sender, DiagramMouseEventArgs e)
  {
   dragStartElement = e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault();
   compartmentBounds = e.HitDiagramItem.Shape.AbsoluteBoundingBox;
  }

  /// <summary>
  /// When the mouse moves away from the initial list item, but still inside the compartment,
  /// create an Action to supervise the cursor and handle subsequent mouse events.
  /// Transfer the details of the initial mouse position to the Action.
  /// </summary>
  /// <param name="sender"></param>
  /// <param name="e"></param>
  void compartment_MouseMove(object sender, DiagramMouseEventArgs e)
  {
   if (dragStartElement != null)
   {
    if (dragStartElement != e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault())
    {
     e.DiagramClientView.ActiveMouseAction = new CompartmentDragMouseAction(dragStartElement, this, compartmentBounds);
     dragStartElement = null;
    }
   }
  }

  /// <summary>
  /// User has released the mouse button.
  /// </summary>
  /// <param name="sender"></param>
  /// <param name="e"></param>
  void compartment_MouseUp(object sender, DiagramMouseEventArgs e)
  {
    dragStartElement = null;
  }

  /// <summary>
  /// Forget the source item if mouse up occurs outside the
  /// compartment.
  /// </summary>
  /// <param name="e"></param>
  public override void OnMouseUp(DiagramMouseEventArgs e)
  {
   base.OnMouseUp(e);
   dragStartElement = null;
  }

  /// <summary>
  /// Called by the Action when the user releases the mouse.
  /// If we are still on the same compartment but in a different list item,
  /// move the starting item to the position of the current one.
  /// </summary>
  /// <param name="dragFrom"></param>
  /// <param name="e"></param>
  public void DoMouseUp(ModelElement dragFrom, DiagramMouseEventArgs e)
  {
   // Original or "from" item:
   ClassModelElement dragFromElement = dragFrom as ClassModelElement;
   // Current or "to" item:
   ClassModelElement dragToElement = e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault();
   if (dragFromElement != null && dragToElement != null)
   {
    // Find the common parent model element, and the relationship links:
    ElementLink parentToLink = GetEmbeddingLink(dragToElement);
    ElementLink parentFromLink = GetEmbeddingLink(dragFromElement);
    if (parentToLink != parentFromLink && parentFromLink != null && parentToLink != null)
    {
     // Get the static relationship and role (= end of relationship):
     DomainRelationshipInfo relationshipFrom = parentFromLink.GetDomainRelationship();
     DomainRoleInfo parentFromRole = relationshipFrom.DomainRoles[0];
     // Get the node in which the element is embedded, usually the element displayed in the shape:
     ModelElement parentFrom = parentFromLink.LinkedElements[0];

     // Same again for the target:
     DomainRelationshipInfo relationshipTo = parentToLink.GetDomainRelationship();
     DomainRoleInfo parentToRole = relationshipTo.DomainRoles[0];
     ModelElement parentTo = parentToLink.LinkedElements[0];

     // Mouse went down and up in same parent and same compartment:
     if (parentTo == parentFrom && relationshipTo == relationshipFrom)
     {
      // Find index of target position:
      int newIndex = 0;
      var elementLinks = parentToRole.GetElementLinks(parentTo);
      foreach (ElementLink link in elementLinks)
      {
       if (link == parentToLink) { break; }
       newIndex++;
      }

      if (newIndex < elementLinks.Count)
      {
       using (Transaction t = parentFrom.Store.TransactionManager.BeginTransaction("Move list item"))
       {
        parentFromLink.MoveToIndex(parentFromRole, newIndex);
        t.Commit();
       }
      }
     }
    }
   }
  }

  /// <summary>
  /// Get the embedding link to this element.
  /// Assumes there is no inheritance between embedding relationships.
  /// (If there is, you need to make sure you've got the relationship
  /// that is represented in the shape compartment.)
  /// </summary>
  /// <param name="child"></param>
  /// <returns></returns>
  ElementLink GetEmbeddingLink(ClassModelElement child)
  {
   foreach (DomainRoleInfo role in child.GetDomainClass().AllEmbeddedByDomainRoles)
   {
    foreach (ElementLink link in role.OppositeDomainRole.GetElementLinks(child))
    {
     // Just the assume the first embedding link is the only one.
     // Not a valid assumption if one relationship is derived from another.
     return link;
    }
   }
   return null;
  }
 }
}
```

## <a name="see-also"></a>请参阅

- [自定义复制行为](../modeling/customizing-copy-behavior.md)
- [部署域特定语言解决方案](msi-and-vsix-deployment-of-a-dsl.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
