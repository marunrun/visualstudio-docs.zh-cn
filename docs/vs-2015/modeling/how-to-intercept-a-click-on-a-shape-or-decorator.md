---
title: 如何：截获对形状或修饰器的单击 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
ms.assetid: e2bc3124-c0c0-4104-9779-a5bf565d7f51
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 865cd15416fbc901b6c5e58e1d83385f64f6a5a8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441076"
---
# <a name="how-to-intercept-a-click-on-a-shape-or-decorator"></a>如何：截获对形状或修饰器的单击
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下过程演示如何截获的单击的形状或图标修饰器。 可以截获单击、 双击、 拖动，和其他手势，并使响应的元素。  
  
## <a name="to-intercept-clicks-on-shapes"></a>若要截获对形状的单击  
 在 Dsl 项目中，独立于生成的代码文件中，代码文件中编写形状类的分部类定义。 重写`OnDoubleClick()`或其他名称开头的方法之一`On...`。 例如：  
  
```  
public partial class MyShape // change  
  {  
    public override void OnDoubleClick(DiagramPointEventArgs e)  
    {  
      base.OnDoubleClick(e);  
      System.Windows.Forms.MessageBox.Show("Click");  
      e.Handled = true;  
  }  }  
```  
  
> [!NOTE]
> 设置`e.Handled`到`true`，除非你想要传递给包含形状或关系图的事件。  
  
## <a name="to-intercept-clicks-on-decorators"></a>若要截获对修饰器的单击  
 图像修饰器 ImageField 类，该类包含 OnDoubleClick 方法的实例上执行。 可以截获下鼠标，如果您编写 ImageField 子类。 InitializeShapeFields 方法中设置字段。 因此，您必须更改该方法，以实例化而不是正则 ImageField 子类。 InitializeShapeFields 方法是形状类的生成的代码中。 可以重写形状类，如果您设置其`Generates Double Derived`属性，如以下过程中所述。  
  
 尽管 InitializeShapeFields 是实例方法，但它是只调用一次为每个类。 因此，只有一个实例 ClickableImageField 存在未一个实例为每个形状图中的每个类中每个字段。 当用户双击实例时，则必须标识已命中哪个实例，如在示例代码所示。  
  
#### <a name="to-intercept-a-click-on-an-icon-decorator"></a>若要截获图标修饰器的单击  
  
1. 打开或创建 DSL 解决方案。  
  
2. 选择或创建具有图标修饰器的形状，并将其映射到域类。  
  
3. 在单独的文件中的代码文件中`GeneratedCode`文件夹中，创建新的 ImageField 子类：  
  
    ```  
    using Microsoft.VisualStudio.Modeling;  
    using Microsoft.VisualStudio.Modeling.Design;  
    using Microsoft.VisualStudio.Modeling.Diagrams;  
    using System.Collections.Generic;  
    using System.Linq;  
  
    namespace Fabrikam.MyDsl { // Change to your namespace  
    internal class ClickableImageField : ImageField  
    {  
      // You can also override OnClick and so on.  
      public override void OnDoubleClick(DiagramPointEventArgs e)  
      {  
        base.OnDoubleClick(e);  
        // Work out which instance was hit.  
        MyShape shapeHit = e.HitDiagramItem.Shape as MyShape;  
        if (shapeHit != null)  
        {  
          MyDomainClass element =   
              shapeHit.ModelElement as MyDomainClass;  
          System.Windows.Forms.MessageBox.Show(  
             "Double click on shape for " + element.Name);  
          // If we do not set Handled, the event will  
          // be passed to the containing shape:  
          e.Handled = true;  
        }  
      }  
  
       public ClickableImageField(string fieldName)  
         : base(fieldName)  
       { }  
    }  
    ```  
  
     应设置为 true，如果你确实想要传递给包含形状的事件的处理。  
  
4. 通过添加以下的分部类定义，重写中形状 classs InitializeShapeFields 方法。  
  
    ```  
    public partial class MyShape // change  
    {  
     protected override void InitializeShapeFields  
          (IList<ShapeField> shapeFields)  
     {  
      base.InitializeShapeFields(shapeFields);  
      // You can see the above method in MyShapeBase   
      // in the generated Shapes.cs  
      // It has already added fields for the Icons.  
      // So you will have to retrieve them and replace with your own.  
      ShapeField unwantedField = shapeFields.First  
          (field => field.Name == "IconDecorator1");  
      shapeFields.Remove(unwantedField);  
  
      // Now replicate the generated code from the base class   
      // in Shape.cs, but with your own image constructor.  
      ImageField field2 = new ClickableImageField("IconDecorator1");        
      field2.DefaultImage = ImageHelper.GetImage(  
        MyDslDomainModel.SingletonResourceManager  
        .GetObject("MyShapeIconDecorator1DefaultImage"));  
          shapeFields.Add(field2);  
    }  
    ```  
  
1. 生成和运行解决方案。  
  
2. 双击该形状的实例上的图标。 应显示你的测试消息。  
  
## <a name="intercepting-clicks-and-drags-on-compartmentshape-lists"></a>截获单击和拖动 CompartmentShape 列表上  
 下面的示例，用户可以在隔离舱形状中通过拖动它们重新排序项。 若要运行此代码：  
  
1. 使用创建新 DSL 解决方案**类图**解决方案模板。  
  
    此外可以使用你自己的解决方案，其中包含隔离舱形状。 此代码假定是由形状表示的模型元素和隔离舱列表项中表示的元素之间的嵌入关系。  
  
2. 设置**生成双派生**隔离舱形状的属性。  
  
3. 在文件中添加此代码**Dsl**项目。  
  
4. 调整此代码，以匹配你自己的 DSL 中的域类和形状名称。  
  
   总之，代码如下所示。 在此示例中，`ClassShape`隔离舱形状的名称。  
  
- 在创建时，鼠标事件处理程序的一组附加到每个隔离舱实例中。  
  
- `ClassShape.MouseDown`事件存储的当前项。  
  
- 当鼠标移出当前项创建 MouseAction 的实例，该设置的光标和捕获鼠标，直到它被释放。  
  
     若要避免干扰其他鼠标操作，例如，选择项的文本 MouseAction 不创建直到鼠标离开原始项。  
  
     创建 MouseAction 的替代方法是只需侦听 MouseUp。 但是，这会无法正常工作如果用户在拖动隔离舱之外后释放鼠标。 MouseAction 仍然能够执行相应的操作无论松开鼠标。  
  
- 释放鼠标后，MouseAction.MouseUp 重新排列模型元素之间的链接的顺序。  
  
- 角色顺序的更改会触发更新显示的规则。 已定义此行为，并且不需要任何其他代码。  
  
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
// This code assumes that the embedding relationships   
// displayed in the compartments don't use inheritance   
// (don't have base or derived domain relationships).  
  
namespace Company.CompartmentDrag  
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
  /// click somewhere else in the source shape.  
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
   dragStartElement = e.HitDiagramItem.RepresentedElements  
     .OfType<ClassModelElement>().FirstOrDefault();  
   compartmentBounds = e.HitDiagramItem.Shape.AbsoluteBoundingBox;  
  }  
  
  /// <summary>  
  /// When the mouse moves away from the initial list item,  
  /// but still inside the compartment, create an Action   
  /// to supervise the cursor and handle subsequent mouse events.  
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
 [响应并传播更改](../modeling/responding-to-and-propagating-changes.md)   
 [修饰器的属性](../modeling/properties-of-decorators.md)
