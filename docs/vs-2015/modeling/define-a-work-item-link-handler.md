---
title: 定义工作项链接处理程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML API
ms.assetid: d52e0bbf-0166-4bb4-a2e3-cefed6188875
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 240f143015f22435deb4f1347f74bebcc8b334c3
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871899"
---
# <a name="define-a-work-item-link-handler"></a>定义工作项链接处理程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以创建一个在用户创建或删除 UML 模型元素和工作项之间的链接时作出响应的 Visual Studio 集成扩展。 例如，当用户选择将新的工作项链接到模型元素时，你的代码可以从模型中的值初始化工作项的字段。

## <a name="set-up-a-uml-extension-solution"></a>设置 UML 扩展解决方案
 这样便可以开发处理程序，然后将它们分配给其他用户。 需要设置两个 Visual Studio 项目：

- 一个类库项目，它包含链接处理程序的代码。

- 一个 VSIX 项目，它充当用于安装命令的容器。 如果需要，可以将其他组件包括在同一 VSIX 中。

#### <a name="to-set-up-the-visual-studio-solution"></a>设置 Visual Studio 解决方案

1. 创建一个类库项目，将该项目添加到现有 VSIX 解决方案或创建一个新的解决方案。

    1. 在“文件” 菜单上，选择“新建”、“项目”。

    2. 在 "**已安装的模板**" 下展开 "**视觉对象C#**  " 或 " **Visual Basic**", 然后在中间栏中单击 "类库"

    3. 设置 **“解决方案”** 以指示你是希望创建新的解决方案，还是希望向已打开的 VSIX 解决方案添加组件。

    4. 设置项目的名称和位置，然后单击“确定”。

2. 除非你的解决方案已经包含一个项目，否则请创建一个 VSIX 项目。

    1. 在“解决方案资源管理器”中，在该解决方案的快捷菜单上依次选择“添加”、“新建项目”。

    2. 在“已安装的模板”下，展开“Visual C#” 或“Visual Basic”，然后选择“扩展性”。 在中间栏中，选择“VSIX 项目”。

3. 将 VSIX 项目设置为解决方案的启动项目。

    - 在“解决方案资源管理器”中，VSIX 项目的快捷菜单上选择“设为启动项目”。

4. 在**source.extension.vsixmanifest**的 "**内容**" 下, 将类库项目添加为 MEF 组件。

    1. 在“元数据” 选项卡上，设置 VSIX 的名称。

    2. 在“安装目标” 选项卡上，将 Visual Studio 版本设置为目标。

    3. 在“资产” 选项卡上，选择“新建”，并在对话框中进行如下设置：

         **类型** = **MEF 组件**

          = **当前解决方案中的项目**

          = *你的类库项目*

## <a name="defining-the-work-item-link-handler"></a>定义工作项链接处理程序
 在类库项目中执行所有以下任务。

### <a name="project-references"></a>项目引用
 向你的项目引用添加以下 [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] 程序集：

 `Microsoft.TeamFoundation.WorkItemTracking.Client.dll`

 `Microsoft.VisualStudio.TeamFoundation.WorkItemTracking.dll Microsoft.VisualStudio.Modeling.Sdk.[version]`

 `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml`

 `Microsoft.VisualStudio.Uml.Interfaces`

 `System.ComponentModel.Composition`

 `System.Drawing`-由示例代码使用

 如果在 "**添加引用**" 对话框的 " **.net** " 选项卡下找不到其中一个引用, 请使用 "浏览" 选项卡在 \Program Files\Microsoft Visual Studio [\\version] \Common7\IDE\PrivateAssemblies 中查找它。

### <a name="import-the-work-item-namespace"></a>导入工作项命名空间
 在项目引用中, 添加对以下程序集的引用: [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]

- Microsoft.TeamFoundation.WorkItemTracking.Client.dll

- Microsoft.VisualStudio.TeamFoundation.WorkItemTracking.dll

  在程序代码中，导入以下命名空间：

```
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Uml.Classes;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.TeamFoundation.WorkItemTracking;
using System.Linq;
```

### <a name="define-the-linked-work-item-event-handler"></a>定义链接的工作项事件处理程序
 将类文件添加到类库项目中，并按如下所示设置其内容。 将命名空间名称和类名更改为你所喜欢的任何名称。

```
using System.ComponentModel.Composition;
using Microsoft.VisualStudio.Uml.Classes;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.TeamFoundation.WorkItemTracking;
using System.Linq;

namespace WorkItems
{
  [Export(typeof(ILinkedWorkItemExtension))]
  public class MyWorkItemExtension : ILinkedWorkItemExtension
  {
    // Called before a new work item is edited by the user.
    // Use this to initialize work item fields from the model element.
    public void OnWorkItemCreated(System.Collections.Generic.IEnumerable<IElement> elementsToBeLinked, IWorkItemDocument workItemDocument)
    {
      INamedElement namedElement =
            elementsToBeLinked.First() as INamedElement;
      if (namedElement != null)
        workItemDocument.Item.Title = namedElement.Name;

    }

    // Called when any work item is linked to a model element.
    public void OnWorkItemLinked(System.Collections.Generic.IEnumerable<IElement> elements, string serverUri, int workItemId)
    {
      foreach (IElement element in elements)
        foreach (IShape shape in element.Shapes())
          shape.Color = System.Drawing.Color.Red;
    }

    // Called when a work item is unlinked from a model element.
    public void OnWorkItemRemoved(IElement element, string serverUri, int workItemId)
    {
      foreach (IShape shape in element.Shapes())
        shape.Color = System.Drawing.Color.White;
    }
  }
}
```

## <a name="testing-the-link-handler"></a>测试链接处理程序
 出于测试目的，在调试模式下执行链接处理程序。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

#### <a name="to-test-the-link-handler"></a>测试链接处理程序

1. 按“F5”，或在“调试” 菜单上，选择“开始调试”。

     此时将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。

     **故障排除**:如果新[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的未启动, 请确保将 VSIX 项目设置为解决方案的启动项目。

2. 在实验性 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中，打开或创建一个建模项目，然后打开或创建一个建模图。

3. 创建模型元素（如 UML 类）并设置其名称。

4. 右键单击元素, 然后单击 "**创建工作项**"。

    - 如果子菜单显示 "**打开 Team Foundation Server 连接**", 则需要关闭项目, 连接到相应的 TFS, 然后重新启动此过程。

    - 如果子菜单显示工作项类型的列表，请单击其中一个类型。

         将打开一个新的工作项表单。

5. 如果使用了上一节中的示例代码，请验证工作项的标题与模型元素相同。 这将演示 `OnWorkItemCreated()` 已运行。

6. 完成表单，保存并关闭工作项。

7. 验证工作项现在是否以红色显示。 这将演示示例代码中的 `OnWorkItemLinked()`。

     **故障排除**:如果处理程序方法未运行, 请验证:

    - 类库项目作为一个 MEF 组件列在 VSIX 项目的 "**内容**" 列表中。

    - 正确的 `Export` 特性附加到处理程序类，该类实现 `ILinkedWorkItemExtension`。

    - 所有 `Import` 和 `Export` 特性的参数都有效。

## <a name="about-the-work-item-handler-code"></a>关于工作项处理程序代码

### <a name="listening-for-new-work-items"></a>侦听新的工作项
 用户选择创建要链接到模型元素的新工作项时调用 `OnWorkItemCreated`。 你的代码可以初始化工作项字段。 然后将向用户呈现工作项，用户可以更新字段和保存工作项。 已成功保存工作项之前，将不会创建指向模型元素的链接。

```
public void OnWorkItemCreated(
    IEnumerable<IElement> elementsToBeLinked,
    IWorkItemDocument workItem)
{
  INamedElement namedElement =
         elementsToBeLinked.First() as INamedElement;
  if (namedElement != null)
      workItem.Item.Title = namedElement.Name;
}
```

### <a name="listening-for-link-creation"></a>侦听链接创建
 `OnWorkItemLinked` 于创建链接后立即调用。 无论链接是指向新工作项还是现有项，均调用它。 为每个工作项调用一次。

```
public void OnWorkItemLinked
        (IEnumerable<IElement> elements,
         string serverUri, // TFS server
         int workItemId)
{
  foreach (IElement element in elements)
    foreach (IShape shape in element.Shapes())
         shape.Color = System.Drawing.Color.Red;
}
```

> [!NOTE]
> 若要使此示例中起作用，必须添加对 `System.Drawing.dll`的项目引用，并导入命名空间 `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation`。 但是，对于 `OnWorkItemLinked` 的其他实现则无需这些添加。

### <a name="listening-for-link-removal"></a>侦听链接删除
 恰好在删除的每个工作项之前调用 `OnWorkItemRemoved`。 如果删除了模型元素，则将删除其所有链接。

```
public void OnWorkItemRemoved
         (IElement element, string serverUri, int workItemId)
{...}
```

## <a name="updating-a-work-item"></a>更新工作项
 使用 Team Foundation 命名空间，可以操作工作项。

 若要使用下面的示例，将这些.NET 程序集添加到你的项目的引用中：

- Microsoft.TeamFoundation.Client.dll

- Microsoft.TeamFoundation.WorkItemTracking.Client.dll

```

using Microsoft.TeamFoundation.Client;
using Microsoft.TeamFoundation.WorkItemTracking.Client;
...
public void OnWorkItemLinked
        (IEnumerable<IElement> elements,
         string serverUri, // TFS server
         int workItemId)
{
  TfsTeamProjectCollection tfs =
        TfsTeamProjectCollectionFactory
            .GetTeamProjectCollection(new Uri(serverUri));
  WorkItemStore workItemStore = new WorkItemStore(tfs);
  WorkItem item = workItemStore.GetWorkItem(workItemId);
  item.Open();
  item.Title = "something";
  item.Save();
} 
```

## <a name="accessing-the-work-item-reference-links"></a>访问工作项引用链接
 可以访问链接，如下：

```
//Get:
string linkString = element.GetReference(ReferenceConstants.WorkItem);
// Set:
element.AddReference(ReferenceConstants.WorkItem, linkString, true);

```

 `linkString` 的格式如下：

 `string.Format(@"%{0}\{1}#{1}${2}", tfServer, projectCollection, RepositoryGuid, workItem.Id);`

 其中：

- 你的服务器的 URI 将为：

   `http://tfServer:8080/tfs/projectCollection`

   在 `projectCollection` 中大小写至关重要。

- 可以从你的 TFS 连接获取 `RepositoryGuid`：

  ```csharp
  TfsTeamProjectCollection tpc = TfsTeamProjectCollectionFactory...;
  RepositoryGuid= tpc.InstanceId;

  ```

  有关引用的详细信息, 请参阅[将引用字符串附加到 UML 模型元素](../modeling/attach-reference-strings-to-uml-model-elements.md)。

## <a name="see-also"></a>请参阅

- [TeamFoundation. WorkItemTracking. WorkItemStore](/previous-versions/visualstudio/visual-studio-2013/bb179850(v=vs.120))
- [链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)
- [将引用字符串附加到 UML 模型元素](../modeling/attach-reference-strings-to-uml-model-elements.md)
- [定义和安装建模扩展](../modeling/define-and-install-a-modeling-extension.md)
- [使用 UML API 编程](../modeling/programming-with-the-uml-api.md)
