---
title: 如何：定义 SharePoint 项目项类型 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: ae709bf2d81e2b8b00dc984602c0426fdf272ebd
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016862"
---
# <a name="how-to-define-a-sharepoint-project-item-type"></a>如何：定义 SharePoint 项目项类型
  若要创建自定义 SharePoint 项目项，请定义项目项类型。 有关详细信息，请参阅[定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)。

### <a name="to-define-a-project-item-type"></a>定义项目项类型

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - VisualStudio

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的类。

4. 将以下属性添加到类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>. 此特性使 Visual Studio 能够发现和加载你的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 类型传递给特性构造函数。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. 在项目项类型定义中，此属性为新项目项指定字符串标识符。 建议使用格式 "*公司名称*"。用于帮助确保所有项目项都具有唯一名称的*功能名称*。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>. 此属性指定要在**解决方案资源管理器**中为此项目项显示的图标。 此属性是可选的;如果不将它应用于类，则 Visual Studio 会为项目项显示默认图标。 如果设置此属性，则传递嵌入到程序集中的图标或位图的完全限定名称。

5. 在方法的实现中 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> ，使用*projectItemTypeDefinition*参数的成员定义项目项类型的行为。 此参数是一个 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> 对象，该对象提供对和接口中定义的事件的访问 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> 。 若要访问项目项类型的特定实例，请处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 事件，例如 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 和 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> 。

## <a name="example"></a>示例
 下面的代码示例演示如何定义一个简单的项目项类型。 当用户将此类型的项目项添加到项目中时，此项目项类型将向 "**输出**" 窗口中写入一条消息，并**错误列表**窗口。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemtype.vb#2)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemtype.cs#2)]

 此示例使用 SharePoint 项目服务将消息写入到 "**输出**" 窗口，并**错误列表**"窗口。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- VisualStudio

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要使其他开发人员可以使用您的项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署项目项，请为 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 程序集、模板和要与项目项分发的任何其他文件创建扩展（VSIX）包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [如何：向自定义 SharePoint 项目项类型添加属性](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [如何：向自定义 SharePoint 项目项类型添加快捷菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
