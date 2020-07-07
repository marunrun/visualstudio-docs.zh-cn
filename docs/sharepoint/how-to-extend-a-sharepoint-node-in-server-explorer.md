---
title: 如何：在服务器资源管理器中扩展 SharePoint 节点 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: ea556d18641b96ea6a38ef5abf6efe4c93a44cdf
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015022"
---
# <a name="how-to-extend-a-sharepoint-node-in-server-explorer"></a>如何：在服务器资源管理器中扩展 SharePoint 节点
  可以在**服务器资源管理器**中的 " **SharePoint 连接**" 节点下扩展节点。 如果要向现有节点添加新的子节点、快捷菜单项或属性，这会很有用。 有关详细信息，请参阅[服务器资源管理器中的 "扩展 SharePoint 连接" 节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

### <a name="to-extend-a-sharepoint-node-in-server-explorer"></a>在服务器资源管理器中扩展 SharePoint 节点

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - VisualStudio

    - VisualStudio （Extension）

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 接口的类。

4. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到该类中。 此特性使 Visual Studio 能够发现和加载你的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 类型传递给特性构造函数。

5. 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 特性添加到该类中。 此属性指定要扩展的节点类型的字符串标识符。

     若要指定 Visual Studio 提供的内置节点类型，请将以下枚举值之一传递给特性构造函数：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>：使用这些值来指定站点连接节点（显示站点 Url 的节点）、站点节点或**服务器资源管理器**中的所有其他父节点。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>：使用这些值来指定一个内置节点，这些节点表示 SharePoint 站点上的单个组件，如表示列表、字段或内容类型的节点。

6. 在方法的实现中 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> ，使用*nodeType*参数的成员向节点添加功能。 此参数是一个 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> 对象，该对象提供对接口中定义的事件的访问 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 。 例如，你可以处理以下事件：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>：处理此事件以便将新的子节点添加到节点。 有关详细信息，请参阅[如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeMenuItemsRequested>：处理此事件可向节点添加自定义快捷菜单项。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodePropertiesRequested>：处理此事件可向节点添加自定义属性。 选择节点时，属性将显示在 "**属性**" 窗口中。

## <a name="example"></a>示例
 下面的代码示例演示如何创建两种不同类型的节点扩展：

- 向 SharePoint 站点节点添加上下文菜单项的扩展。 单击菜单项时，将显示已单击的节点的名称。

- 将名为**ContosoExampleProperty**的自定义属性添加到表示名为**Body**的字段的每个节点的扩展。

  [!code-csharp[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextension.cs#9)]
  [!code-vb[SPExtensibility.ProjectSystemExtension.General#9](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextension.vb#9)]

  此扩展将可编辑的字符串属性添加到节点。 你还可以创建自定义属性，用于显示 SharePoint 服务器中的只读数据。 有关演示如何执行此操作的示例，请参阅[演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio

- VisualStudio （Extension）

- System.ComponentModel.Composition

- System.Windows.Forms

## <a name="deploy-the-extension"></a>部署扩展
 若要部署**服务器资源管理器**扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 程序集以及要使用该扩展分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：将自定义 SharePoint 节点添加到服务器资源管理器](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [扩展中的 "SharePoint 连接" 节点服务器资源管理器](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
