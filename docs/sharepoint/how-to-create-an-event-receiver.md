---
title: 如何：创建事件接收器 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.EventReceiver
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, event receivers
- event receivers [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 26d8c9f433fad051716b6ebd37e3d1f3b3f9f4eb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016920"
---
# <a name="how-to-create-an-event-receiver"></a>如何：创建事件接收器
  通过创建 *事件接收器*，你可以在用户与 SharePoint 项（如列表或列表项）交互时做出响应。 例如，当用户更改日历或从联系人列表中删除名称时，可以触发事件接收器中的代码。 通过遵循本主题，可以了解如何将事件接收器添加到列表实例。

 若要完成这些步骤，必须已安装 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 并支持 Windows 和 SharePoint 版本。 由于此示例需要一个 SharePoint 项目，因此还必须完成主题 [演练：创建网站栏、内容类型和 SharePoint 列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)主题中的过程。

## <a name="adding-an-event-receiver"></a>添加事件接收器
 在 [演练：创建网站栏、内容类型和 SharePoint 列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) 中创建的项目包含自定义网站列、自定义列表和内容类型。 在下面的过程中，您将通过添加一个简单的事件处理程序 (事件接收器) 到列表实例来展开此项目，以演示如何处理 SharePoint 项（如列表）中发生的事件。

#### <a name="to-add-an-event-receiver-to-the-list-instance"></a>将事件接收器添加到列表实例

1. 打开在 [演练：创建网站栏、内容类型和 SharePoint 列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)中创建的项目。

2. 在 **解决方案资源管理器**中，选择名为 " **诊所**" 的 SharePoint 项目节点。

3. 在菜单栏上，选择 "**项目**" "  >  **添加新项**"。

4. 在 **Visual c #** 或 **Visual Basic**下，展开 " **SharePoint** " 节点，然后选择 **2010** 项。

5. 在 " **模板** " 窗格中，选择 " **事件接收器**"，将其命名为 **TestEventReceiver1**，然后选择 **"确定"** 按钮。

     " **SharePoint 自定义向导** " 随即出现。

6. 在 " **要执行哪种类型的事件接收器？"** 列表中，选择 " **列表项事件**"。

7. 在 " **哪个项应为事件源？"** 列表中，选择 " **患者 (Clinic\Patients) **"。

8. 在 " **处理以下事件** " 列表中，选中 " **添加项**" 旁边的复选框，然后选择 " **完成** " 按钮。

     新事件接收器的代码文件包含一个名为的方法 `ItemAdded` 。 在下一步中，你将向此方法中添加代码，以便默认将每个联系人命名为 Scott 棕色。

9. 将现有 `ItemAdded` 的方法替换为以下代码，然后选择 **F5** 键：

     [!code-csharp[SP_EventReceiver#1](../sharepoint/codesnippet/CSharp/CustomField1/TestEventReceiver1/TestEventReceiver1.cs#1)]
     [!code-vb[SP_EventReceiver#1](../sharepoint/codesnippet/VisualBasic/CustomField1_VB/EventReceiver1/EventReceiver1.vb#1)]

     代码将运行，SharePoint 站点将显示在 web 浏览器中。

10. 在快速启动栏上，选择 " **患者** " 链接，然后选择 " **添加新项** " 链接。

     此时将打开新项的输入窗体。

11. 在字段中输入数据，然后选择 " **保存** " 按钮。

     选择 " **保存** " 按钮后，" **患者名称** " 列会自动将名称更新为 Scott 棕色。

## <a name="see-also"></a>另请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)