---
title: 如何：定义 SharePoint 项目项类型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0e0483f535dfd7a483d2b83728f78fa9c7167bcb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62814039"
---
# <a name="how-to-define-a-sharepoint-project-item-type"></a>如何：定义 SharePoint 项目项类型
  如果想要创建自定义 SharePoint 项目项，定义的项目项类型。 有关详细信息，请参阅[定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)。

### <a name="to-define-a-project-item-type"></a>若要定义项目项类型

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的类。

4. 将以下属性添加到类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>。 此特性使 Visual Studio 能够发现和加载您<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>实现。 传递<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>特性构造函数的类型。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>。 在项目项类型定义中，此属性指定新的项目项的字符串标识符。 我们建议你使用格式*公司名称*。*功能名称*以帮助确保所有项目项都具有唯一的名称。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>。 此属性指定要为此项目项中显示的图标**解决方案资源管理器**。 此属性是可选的;如果不将其应用到您的类，Visual Studio 将显示您的项目项的默认图标。 如果设置此属性时，传递图标或程序集中嵌入的位图的完全限定的名称。

5. 中的实现<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>方法，使用成员*projectItemTypeDefinition*参数来定义项目项类型的行为。 此参数是<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>提供对中定义的事件的访问的对象<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents>和<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents>接口。 若要访问你的项目项类型的特定实例，请处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents>事件，如<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded>和<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized>。

## <a name="example"></a>示例
 下面的代码示例演示如何定义一个简单的项目项类型。 此项目项类型将消息写入**输出**窗口和**错误列表**窗口时用户将此类型的项目项添加到项目。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemtype.vb#2)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemtype.cs#2)]

 此示例使用 SharePoint 项目服务将写入到消息**输出**窗口和**错误列表**窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要启用其他开发人员能够使用您的项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署的项目项，创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包的程序集、 模板和你想要将与项目项一起分发的任何其他文件。 有关详细信息，请参阅[在 Visual Studio 工具部署 SharePoint 扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [创建项模板和用于 SharePoint 项目项的项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [如何：将属性添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义的 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
