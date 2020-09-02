---
title: 如何：将自定义 SharePoint 节点添加到服务器资源管理器 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 26a2ea6a7ccbfcc80275b55f9230f1a3152ab545
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86017058"
---
# <a name="how-to-add-a-custom-sharepoint-node-to-server-explorer"></a>如何：将自定义 SharePoint 节点添加到服务器资源管理器
  可以在**服务器资源管理器**中的 " **SharePoint 连接**" 节点下添加自定义节点。 当你希望显示默认情况下未显示在 **服务器资源管理器** 中的其他 SharePoint 组件时，这非常有用。 有关详细信息，请参阅 [服务器资源管理器中的 "扩展 SharePoint 连接" 节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)。

 若要添加自定义节点，请首先创建一个定义新节点的类。 然后创建一个将节点作为现有节点的子节点添加的扩展。

### <a name="to-define-the-new-node"></a>定义新节点

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - VisualStudio

    - VisualStudio （Extension）

    - System.ComponentModel.Composition

    - System.Drawing

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 接口的类。

4. 将以下属性添加到类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>. 此特性使 Visual Studio 能够发现和加载你的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 类型传递给特性构造函数。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute>. 在节点定义中，此属性指定新节点的字符串标识符。 建议使用格式 " *公司名称*"。*节点名称* ，以确保所有节点都具有唯一的标识符。

5. 在方法的实现中 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider.InitializeType%2A> ，使用 *typeDefinition* 参数的成员配置新节点的行为。 此参数是一个 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition> 对象，该对象提供对接口中定义的事件的访问 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> 。

     下面的代码示例演示如何定义新节点。 此示例假定你的项目包含一个名为 CustomChildNodeIcon 的图标作为嵌入资源。

     [!code-vb[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#6)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#6](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#6)]

### <a name="to-add-the-new-node-as-a-child-of-an-existing-node"></a>将新节点添加为现有节点的子节点

1. 在与节点定义相同的项目中，创建一个实现接口的类 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 。

2. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 特性添加到该类中。 此特性使 Visual Studio 能够发现和加载你的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 类型传递给特性构造函数。

3. 将 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 特性添加到该类中。 在节点扩展中，此属性指定要扩展的节点类型的字符串标识符。

     若要指定 Visual Studio 提供的内置节点类型，请将以下枚举值之一传递给特性构造函数：

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>：使用这些值来指定站点连接节点 (在 **服务器资源管理器**中显示站点 url 的节点) 、站点节点或所有其他父节点。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>：使用这些值来指定一个内置节点，这些节点表示 SharePoint 站点上的单个组件，如表示列表、字段或内容类型的节点。

4. 在方法的实现中 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> ，处理参数的 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> 事件 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> 。

5. 在 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> 事件处理程序中，将新节点添加到 <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeEventArgs.Node%2A> 由事件参数参数公开的对象的子节点集合。

     下面的代码示例演示如何将新节点作为 **服务器资源管理器**中 SharePoint 站点节点的子节点添加。

     [!code-vb[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#7)]
     [!code-csharp[SPExtensibility.ProjectSystemExtension.General#7](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#7)]

## <a name="complete-example"></a>完整示例
 下面的代码示例提供了完整的代码，用于定义一个简单的节点并将其作为 **服务器资源管理器**中 SharePoint 站点节点的子节点添加。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb#5)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#5](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs#5)]

## <a name="compiling-the-code"></a>编译代码
 此示例假定你的项目包含一个名为 CustomChildNodeIcon 的图标作为嵌入资源。 此示例还需要引用以下程序集：

- VisualStudio

- System.ComponentModel.Composition

- System.Drawing

## <a name="deploy-the-extension"></a>部署扩展
 若要部署 **服务器资源管理器** 扩展，请 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 为程序集以及要使用该扩展分发的任何其他文件创建扩展 (VSIX) 包。 有关详细信息，请参阅 [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展中的 "SharePoint 连接" 节点服务器资源管理器](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [如何：在服务器资源管理器中扩展 SharePoint 节点](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
