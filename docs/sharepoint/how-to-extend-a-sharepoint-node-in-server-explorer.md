---
title: 如何：扩展服务器资源管理器中的 SharePoint 节点 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c5e617b57437033f4194d96647ebff9d1c4e2c2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813992"
---
# <a name="how-to-extend-a-sharepoint-node-in-server-explorer"></a>如何：扩展服务器资源管理器中的 SharePoint 节点
  您可以扩展节点下的**SharePoint 连接**中的节点**服务器资源管理器**。 当你想要将新的子节点、 快捷菜单项或属性添加到现有节点时，这很有用。 有关详细信息，请参阅[扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

### <a name="to-extend-a-sharepoint-node-in-server-explorer"></a>若要扩展服务器资源管理器中的 SharePoint 节点

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.SharePoint.Explorer.Extensions

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口的类。

4. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到该类中。 此特性使 Visual Studio 能够发现和加载您<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension>实现。 传递<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension>特性构造函数的类型。

5. 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 特性添加到该类中。 此属性指定您想要扩展的节点的类型的字符串标识符。

     若要指定所提供的 Visual Studio 的内置节点类型，请将以下枚举值之一传递给特性构造函数：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>：使用这些值来指定站点连接节点 （节点显示站点 Url），站点中的所有其他父节点或节点**服务器资源管理器**。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>：使用这些值来指定一个表示 SharePoint 站点，例如表示列表、 字段或内容类型的节点上的单个组件的内置节点。

6. 中的实现<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A>方法，使用成员*nodeType*参数，将功能添加到节点。 此参数是<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType>提供对中定义的事件的访问的对象<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents>接口。 例如，你可以处理以下事件：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>：处理此事件，以便将新的子节点添加到节点。 有关详细信息，请参阅[如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeMenuItemsRequested>：处理此事件，以便将自定义的快捷菜单项添加到节点。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodePropertiesRequested>：处理此事件，以便将自定义属性添加到节点。 属性将显示在**属性**窗口时选择的节点。

## <a name="example"></a>示例
 下面的代码示例演示如何创建两个不同类型的节点扩展：

- 将一个上下文菜单项添加到 SharePoint 站点节点扩展。 当单击菜单项时，将会显示被单击的节点的名称。

- 添加名为的自定义属性的扩展**ContosoExampleProperty**到每个节点都表示一个名为字段**正文**。

  [!code-csharp[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextension.cs#9)]
  [!code-vb[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextension.vb#9)]

  此扩展可编辑的字符串属性添加到节点。 此外可以创建显示 SharePoint server 的只读数据的自定义属性。 有关演示如何执行此操作的示例，请参阅[演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.SharePoint.Explorer.Extensions

- System.ComponentModel.Composition

- System.Windows.Forms

## <a name="deploy-the-extension"></a>将扩展部署
 若要部署**服务器资源管理器**扩展中，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
