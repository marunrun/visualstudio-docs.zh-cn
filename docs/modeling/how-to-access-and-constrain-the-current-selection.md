---
title: 如何：访问和约束当前所选内容
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, accessing the current selection
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5cc93f276dae3caeec08a21a74e3bdcaa365fee9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62993454"
---
# <a name="how-to-access-and-constrain-the-current-selection"></a>如何：访问和约束当前所选内容

当为特定于域的语言编写命令或笔势处理程序时，可以确定用户右键单击哪些元素。 您也可以选择阻止某些形状或字段。 例如，您可以排列当用户单击图标修饰器，而是选择包含该形状。 约束中这种方式的选择可减少必须编写的处理程序的数量。 它还更加简单的用户，可以单击任意位置在形状中而无需避免修饰器。

## <a name="access-the-current-selection-from-a-command-handler"></a>从命令处理程序访问当前所选内容

域特定语言的命令集类包含自定义命令的命令处理程序。 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>派生域特定语言的命令集类的类提供用于访问当前所选内容的几个成员。

根据命令，命令处理程序可能需要在模型设计器、 模型资源管理器或在活动窗口中的选择。

### <a name="to-access-selection-information"></a>若要访问所选内容信息

1. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>类定义可用于访问当前所选内容的以下成员。

    |成员|描述|
    |-|-|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsAnyDocumentSelectionCompartment%2A> 方法|返回`true`如果任何所选模型设计器中的元素为隔离舱形状; 否则为`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsDiagramSelected%2A> 方法|返回`true`关系图是在模型设计器中选定; 否则为如果`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleDocumentSelection%2A> 方法|返回`true`恰好一个元素是在模型设计器中选定; 否则为如果`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleSelection%2A> 方法|返回`true`恰好一个元素是所选活动窗口中; 否则为如果`false`。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentDocumentSelection%2A> 属性|获取在模型设计器中选择的元素的只读集合。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentSelection%2A> 属性|获取所选活动窗口中的元素的只读集合。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleDocumentSelection%2A> 属性|在模型设计器中获取所选内容的主要元素。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleSelection%2A> 属性|在活动窗口中获取所选内容的主要元素。|

2. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet.CurrentDocView%2A>的属性<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>类提供对访问<xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>对象，它表示在模型设计器窗口，并提供模型设计器中的所选的元素的额外的访问权限。

3. 此外，生成的代码定义了一个资源管理器工具窗口中属性和命令中的资源管理器中选择属性设置为域特定语言的类。

    - 资源管理器工具窗口属性返回的域特定语言资源管理器工具窗口类的实例。 资源管理器工具窗口类派生自<xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>类，并表示域特定语言的模型资源管理器。

    - `ExplorerSelection`属性在域特定语言的模型资源管理器窗口中返回所选的元素。

## <a name="determine-which-window-is-active"></a>确定哪个窗口处于活动状态

<xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>接口包含定义提供对在 shell 中的当前选择状态的访问的成员。 可以获取<xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>包类或通过特定于域的语言的命令集类的对象`MonitorSelection`的每个基类中定义的属性。 包类派生自<xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>类和命令集类派生<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>类。

### <a name="to-determine-from-a-command-handler-what-type-of-window-is-active"></a>若要从命令处理程序确定哪种类型的窗口处于活动状态

1. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.MonitorSelection%2A>的属性<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>类返回<xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>提供对在 shell 中的当前选择状态的访问的对象。

2. <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService.CurrentSelectionContainer%2A>属性的<xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>接口获取活动选择项容器，它可以不同于活动窗口。

3. 将添加到命令的以下属性类为你设置特定于域的语言，以确定哪种类型的窗口处于活动状态。

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

## <a name="constrain-the-selection"></a>约束所选内容

通过添加所选内容的规则，可以控制用户在模型中选择某个元素时选择哪些元素。 例如，若要允许用户将大量的元素视为单个单元，可以使用所选内容规则。

### <a name="to-create-a-selection-rule"></a>若要创建一个选择规则

1. 在 DSL 项目中创建自定义代码文件

2. 定义选择规则类派生自<xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>类。

3. 重写<xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules.GetCompliantSelection%2A>选择规则类要应用的选择条件的方法。

4. 将 ClassDiagram 类的分部类定义添加到你的自定义代码文件。

     `ClassDiagram`类派生自<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>类，并在生成的代码文件中，Diagram.cs，在 DSL 项目中定义。

5. 重写<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A>属性的`ClassDiagram`类以返回自定义选择规则。

     默认实现<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A>属性获取不会修改所选内容的所选内容规则对象。

### <a name="example"></a>示例

下面的代码文件创建扩展选择要包括的每个域形状的最初选择的所有实例的所选内容规则。

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

- <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>
- <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>
- <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>