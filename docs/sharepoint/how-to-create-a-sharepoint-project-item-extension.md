---
title: 如何：创建 SharePoint 项目项扩展 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 345bfa49da4bf5d5b73fe1d3f209675fe2814de2
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015355"
---
# <a name="how-to-create-a-sharepoint-project-item-extension"></a>如何：创建 SharePoint 项目项扩展
  如果要向已安装在 Visual Studio 中的 SharePoint 项目项添加功能，请创建项目项扩展。 有关详细信息，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

### <a name="to-create-a-project-item-extension"></a>创建项目项扩展

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - VisualStudio

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 接口的类。

4. 将以下属性添加到类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>. 此特性使 Visual Studio 能够发现和加载你的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 类型传递给特性构造函数。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. 在项目项扩展中，此属性标识要扩展的项目项。 将项目项的 ID 传递给特性构造函数。 有关包含在 Visual Studio 中的项目项的 Id 列表，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

5. 在方法的实现中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> ，使用*projectItemType*参数的成员定义扩展的行为。 此参数是一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> 对象，该对象提供对和接口中定义的事件的访问 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> 。 若要访问要扩展的项目项类型的特定实例，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 和等事件 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> 。

## <a name="example"></a>示例
 下面的代码示例演示如何为事件接收器项目项创建简单扩展。 用户每次向 SharePoint 项目中添加一个事件接收器项目项时，此扩展都会向 "**输出**" 窗口中写入一条消息，并**错误列表**窗口。

 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemextension.cs#1)]
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemextension.vb#1)]

 此示例使用 SharePoint 项目服务将消息写入到 "**输出**" 窗口，并**错误列表**"窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署该扩展，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 该程序集创建一个扩展（VSIX）包，并为要使用该扩展分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
