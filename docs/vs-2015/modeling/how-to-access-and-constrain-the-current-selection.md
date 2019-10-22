---
title: 如何：访问和约束当前所选内容 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, accessing the current selection
ms.assetid: 2990981e-dfae-416f-b0d0-7197f1242dfa
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 00fa99ce9be158b2fe7b0bc4076817892a1b1ba9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646237"
---
# <a name="how-to-access-and-constrain-the-current-selection"></a>如何：访问和约束当前所选内容
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当你为域特定语言编写命令或笔势处理程序时，你可以确定用户右键单击的元素。 您还可以阻止选择某些形状或字段。 例如，可以安排用户单击图标修饰器时，改为选择包含它的形状。 以这种方式约束选定内容将减少您必须编写的处理程序的数量。 它还可让用户更轻松地单击形状中的任意位置，而无需避免修饰器。

## <a name="accessing-the-current-selection-from-a-command-handler"></a>从命令处理程序访问当前所选内容
 域特定语言的命令集类包含自定义命令的命令处理程序。 用于派生域特定语言的命令集类的 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> 类提供一些用于访问当前所选内容的成员。

 根据命令，命令处理程序可能需要在模型设计器、模型资源管理器或活动窗口中进行选择。

#### <a name="to-access-selection-information"></a>访问选择信息

1. @No__t_0 类定义可用于访问当前所选内容的以下成员。

    |成员|描述|
    |------------|-----------------|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsAnyDocumentSelectionCompartment%2A> 方法|如果在模型设计器中选择的任何元素为隔离舱形状，则返回 `true`;否则，`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsDiagramSelected%2A> 方法|如果在模型设计器中选择了关系图，则返回 `true`;否则，`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleDocumentSelection%2A> 方法|如果在模型设计器中仅选择了一个元素，则返回 `true`;否则，`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleSelection%2A> 方法|如果在活动窗口中仅选择了一个元素，则返回 `true`;否则，`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentDocumentSelection%2A> 属性|获取在模型设计器中选定的元素的只读集合。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentSelection%2A> 属性|获取在活动窗口中选定的元素的只读集合。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleDocumentSelection%2A> 属性|获取模型设计器中选定内容的主要元素。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleSelection%2A> 属性|获取活动窗口中选定内容的主要元素。|

2. @No__t_1 类的 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet.CurrentDocView%2A> 属性提供对表示模型设计器窗口的 <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView> 对象的访问，并在模型设计器中提供对所选元素的其他访问权限。

3. 此外，生成的代码在命令集类中为域特定语言定义了资源管理器工具窗口属性和资源管理器选择属性。

    - 资源管理器工具窗口属性为域特定语言返回资源管理器工具窗口类的实例。 "资源管理器" 工具窗口类派生自 <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow> 类，表示域特定语言的模型资源管理器。

    - @No__t_0 属性为域特定语言返回 "模型资源管理器" 窗口中的选定元素。

## <a name="determining-which-window-is-active"></a>确定哪个窗口处于活动状态
 @No__t_0 接口包含用于提供对 shell 中当前选择状态的访问的成员。 可以通过每个的基类中定义的 `MonitorSelection` 属性，从包类或域特定语言的命令集类获取 <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> 对象。 包类派生自 <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage> 类，命令集类派生自 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> 类。

#### <a name="to-determine-from-a-command-handler-what-type-of-window-is-active"></a>从命令处理程序确定活动窗口的类型

1. @No__t_1 类的 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.MonitorSelection%2A> 属性返回一个 <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> 对象，该对象提供对 shell 中当前选择状态的访问。

2. @No__t_1 接口的 <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService.CurrentSelectionContainer%2A> 属性获取活动选择容器，该容器可以不同于活动窗口。

3. 向命令集类添加以下属性，以用于域特定语言，以确定活动窗口的类型。

    ```csharp
    // using Microsoft.VisualStudio.Modeling.Shell;

    // Returns true if the model designer is the active selection container;
    // otherwise, false.
    protected bool IsDesignerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is DiagramDocView);
        }
    }

    // Returns true if the model explorer is the active selection container;
    // otherwise, false.
    protected bool IsExplorerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is ModelExplorerToolWindow);
        }
    }
    ```

## <a name="constraining-the-selection"></a>约束选定内容
 通过添加选择规则，可以控制用户在模型中选择元素时选择的元素。 例如，若要允许用户将多个元素视为单个单元，可以使用选择规则。

#### <a name="to-create-a-selection-rule"></a>创建选择规则

1. 在 DSL 项目中创建自定义代码文件

2. 定义派生自 <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules> 类的选择规则类。

3. 重写选择规则类的 <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules.GetCompliantSelection%2A> 方法，以应用选择条件。

4. 将 .Classdiagram 类的分部类定义添加到自定义代码文件中。

     @No__t_0 类派生自 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram> 类，在 DSL 项目中生成的代码文件 Diagram.cs 中定义。

5. 重写 `ClassDiagram` 类的 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A> 属性以返回自定义选择规则。

     @No__t_0 属性的默认实现将获取不会修改所选内容的选择规则对象。

### <a name="example"></a>示例
 下面的代码文件创建一个选择规则，该规则将选定内容扩展为包含最初选定的每个域形状的所有实例。

```csharp
using System;
using System.Collections.Generic;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

namespace CompanyName.ProductName.GroupingDsl
{
    public class CustomSelectionRules : DiagramSelectionRules
    {
        protected Diagram diagram;
        protected IElementDirectory elementDirectory;

        public CustomSelectionRules(Diagram diagram)
        {
            if (diagram == null) throw new ArgumentNullException();

            this.diagram = diagram;
            this.elementDirectory = diagram.Store.ElementDirectory;
        }

        /// <summary>Called by the design surface to allow selection filtering.
        /// </summary>
        /// <param name="currentSelection">[in] The current selection before any
        /// ShapeElements are added or removed.</param>
        /// <param name="proposedItemsToAdd">[in/out] The proposed DiagramItems to
        /// be added to the selection.</param>
        /// <param name="proposedItemsToRemove">[in/out] The proposed DiagramItems
        /// to be removed from the selection.</param>
        /// <param name="primaryItem">[in/out] The proposed DiagramItem to become
        /// the primary DiagramItem of the selection. A null value signifies that
        /// the last DiagramItem in the resultant selection should be assumed as
        /// the primary DiagramItem.</param>
        /// <returns>true if some or all of the selection was accepted; false if
        /// the entire selection proposal was rejected. If false, appropriate
        /// feedback will be given to the user to indicate that the selection was
        /// rejected.</returns>
        public override bool GetCompliantSelection(
            SelectedShapesCollection currentSelection,
            DiagramItemCollection proposedItemsToAdd,
            DiagramItemCollection proposedItemsToRemove,
            DiagramItem primaryItem)
        {
            if (currentSelection.Count == 0 && proposedItemsToAdd.Count == 0) return true;

            HashSet<DomainClassInfo> itemsToAdd = new HashSet<DomainClassInfo>();

            foreach (DiagramItem item in proposedItemsToAdd)
            {
                if (item.Shape != null)
                    itemsToAdd.Add(item.Shape.GetDomainClass());
            }
            proposedItemsToAdd.Clear();
            foreach (DomainClassInfo classInfo in itemsToAdd)
            {
                foreach (ModelElement element
                    in this.elementDirectory.FindElements(classInfo, false))
                {
                    if (element is ShapeElement)
                    {
                        proposedItemsToAdd.Add(
                            new DiagramItem((ShapeElement)element));
                    }
                }
            }

            return true;
        }
    }

    public partial class ClassDiagram
    {
        protected CustomSelectionRules customSelectionRules = null;

        protected bool multipleSelectionMode = true;

        public override DiagramSelectionRules SelectionRules
        {
            get
            {
                if (multipleSelectionMode)
                {
                    if (customSelectionRules == null)
                    {
                        customSelectionRules = new CustomSelectionRules(this);
                    }
                    return customSelectionRules;
                }
                else
                {
                    return base.SelectionRules;
                }
            }
        }
    }
}
```

## <a name="see-also"></a>请参阅
 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>
 <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>
 <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>
 <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>
 <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>
 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>
