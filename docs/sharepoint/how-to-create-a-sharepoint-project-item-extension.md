---
title: 如何：创建 SharePoint 项目项扩展 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: c46b629227b1b3d73ee4bc6a265c867921937df2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62966958"
---
# <a name="how-to-create-a-sharepoint-project-item-extension"></a>如何：创建 SharePoint 项目项扩展
  如果想要将功能添加到已安装 Visual Studio 中的 SharePoint 项目项，创建项目项扩展。 有关详细信息，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

### <a name="to-create-a-project-item-extension"></a>若要创建项目项扩展

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 接口的类。

4. 将以下属性添加到类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>。 此特性使 Visual Studio 能够发现和加载您<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>实现。 传递<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>特性构造函数的类型。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>。 在项目项扩展中，此属性标识想要扩展的项目项。 将项目项的 ID 传递给特性构造函数。 包含在 Visual Studio 的项目项的 Id 的列表，请参阅[扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)。

5. 中的实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A>方法，使用成员*projectItemType*参数来定义您的扩展插件的行为。 此参数是<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>提供对中定义的事件的访问的对象<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents>和<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents>接口。 若要访问要扩展的项目项类型的特定实例，请处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents>事件，如<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded>和<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized>。

## <a name="example"></a>示例
 下面的代码示例演示如何创建事件接收器项目项的简单扩展。 每次用户将事件接收器项目项添加到 SharePoint 项目，此扩展将消息写入**输出**窗口和**错误列表**窗口。

 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemextension.cs#1)]
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemextension.vb#1)]

 此示例使用 SharePoint 项目服务将写入到消息**输出**窗口和**错误列表**窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>将扩展部署
 若要将扩展部署，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集和你想要将与该扩展一起分发的任何其他文件。 有关详细信息，请参阅[部署 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [扩展 SharePoint 项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
