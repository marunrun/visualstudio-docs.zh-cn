---
title: 如何：创建事件接收器 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: bc42a92e1d7dcc73bb6bc0433da4e6a31d7fefb2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62966752"
---
# <a name="how-to-create-an-event-receiver"></a>如何：创建事件接收器
  通过创建*事件接收器*，可以响应用户与 SharePoint 项，如列表或列表项交互时。 例如，当用户更改日历，或从联系人列表中删除一个名称，可以触发事件接收器中的代码。 通过按照本主题，可以了解如何将事件接收器添加到列表实例。

 若要完成这些步骤，您必须安装[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]和支持的 Windows 和 SharePoint 版本。 由于此示例需要 SharePoint 项目，你还必须已完成本主题中的过程[演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)。

## <a name="adding-an-event-receiver"></a>添加事件接收器
 在中创建的项目[演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)包括自定义站点列、 自定义列表和内容类型。 在下面的过程中，将此项目扩展通过将简单的事件处理程序 （事件接收器） 添加到要演示如何处理 SharePoint 项，如列表中发生的事件的列表实例。

#### <a name="to-add-an-event-receiver-to-the-list-instance"></a>若要将事件接收器添加到列表实例

1. 打开你在中创建的项目[演练：创建 SharePoint 网站栏、 内容类型和列表](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)。

2. 在中**解决方案资源管理器**，选择 SharePoint 项目节点，其名称为**Clinic**。

3. 在菜单栏上，依次选择“项目” > “添加新项”。

4. 下**Visual C#** 或**Visual Basic**，展开**SharePoint**节点，然后选择**2010年**项。

5. 在中**模板**窗格中，选择**事件接收器**，其命名为**TestEventReceiver1**，然后选择**确定**按钮。

     **SharePoint 自定义向导**出现。

6. 在中**所需哪种类型的事件接收器？** 列表中，选择**列表项事件**。

7. 在中**哪个项应为事件源？** 列表中，选择**患者 (Clinic\Patients)**。

8. 在中**处理以下事件**列表中，选中复选框旁边**已添加项**，然后选择**完成**按钮。

     新的事件接收器代码文件包含一个方法名为`ItemAdded`。 在下一步中，你会将代码添加到此方法，以便每个联系人将被命名为 Scott Brown 默认情况下。

9. 替换现有`ItemAdded`方法用以下代码，，然后选择**F5**密钥：

     [!code-csharp[SP_EventReceiver#1](../sharepoint/codesnippet/CSharp/CustomField1/TestEventReceiver1/TestEventReceiver1.cs#1)]
     [!code-vb[SP_EventReceiver#1](../sharepoint/codesnippet/VisualBasic/CustomField1_VB/EventReceiver1/EventReceiver1.vb#1)]

     代码运行和 SharePoint 站点将显示在 web 浏览器。

10. 在快速启动栏上依次选择**患者**链接，，然后选择**添加新项**链接。

     在输入窗体的新项将打开。

11. 在字段中，输入数据，然后选择**保存**按钮。

     选择后**保存**按钮，**患者名称**列将自动更新为 Scott Brown 的名称。

## <a name="see-also"></a>请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)