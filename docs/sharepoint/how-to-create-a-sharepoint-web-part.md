---
title: 如何：创建 SharePoint Web 部件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 304e9f29d317a5258467e4ff45248d0dd2066d4f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62966804"
---
# <a name="how-to-create-a-sharepoint-web-part"></a>如何：创建 SharePoint web 部件
  可以创建并通过添加自定义 web 部件**Web 部件**向任何 SharePoint 项目项，然后编辑 web 部件或使用设计器的代码文件。 有关详细信息，请参阅[如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)。

### <a name="to-create-a-sharepoint-web-part"></a>若要创建一个 SharePoint web 部件

1. 创建或打开一个 SharePoint 项目。

     有关详细信息，请参阅[SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 选择中的 SharePoint 项目节点**解决方案资源管理器**，然后选择**项目** > **添加新项**。

3. 在中**添加新项**对话框框中，展开**SharePoint**节点，然后选择**2010年**节点。

4. 在 SharePoint 模板列表中，选择**Web 部件**。

5. 在中**名称**框中，指定 web 部件的名称，然后选择**添加**按钮。

     在显示 web 部件**解决方案资源管理器**。 有关 web 部件所包含的文件的详细信息，请参阅[为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)。

6. 在中**解决方案资源管理器**，打开刚刚创建的 web 部件的代码文件。

     例如，如果您的 web 部件的名称是*WebPart1*，打开*WebPart1.vb* （在 Visual Basic) 或*WebPart1.cs* （在 C# 中)。

7. 在代码文件中，向 <xref:System.Web.UI.Control.CreateChildControls%2A> 方法添加控件。

     有关示例，请参阅[演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)。

## <a name="see-also"></a>请参阅
- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [如何：使用设计器创建 SharePoint web 部件](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
- [演练：为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [演练：使用设计器为 SharePoint 创建 web 部件](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
