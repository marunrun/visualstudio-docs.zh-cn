---
title: Outlook 窗体区域中的自定义操作
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], custom actions
- custom actions [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0044991b330594d80422f0c6ac1d1d64b1fec237
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951165"
---
# <a name="custom-actions-in-outlook-form-regions"></a>Outlook 窗体区域中的自定义操作
  操作显示按钮，使用户能够对 Microsoft Office Outlook 项做出响应。 例如，若要对邮件项做出响应，用户单击**答复**，**全部答复**，或**向前**操作按钮。 每个操作创建新的邮件项，并通过使用原始项中的信息填充的项的字段。

 可以创建自定义操作打开任何类型的 Outlook 项。 例如，可以添加将打开一个新的约会或任务项的自定义操作。 设置自定义操作的属性或使用自定义代码以填充新项的字段。 自定义操作显示在**自定义操作**的项在 Outlook 检查器窗口中处于打开状态的下拉列表。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-custom-actions-to-a-form-region"></a>将自定义操作添加到窗体区域
 若要添加到窗体区域自定义操作，请使用**自定义操作**对话框。 您可以打开**自定义操作**对话框中的选择窗体区域中**解决方案资源管理器**、 扩展**清单**中的节点**属性窗口**，选择**CustomActions**属性，并单击省略号按钮 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆"))。

 可以使用**自定义操作**对话框可以指定*目标窗体*。 目标窗体是用户执行自定义操作时显示的窗体。

 此外可以使用**自定义操作**对话框可以指定希望从原始项目以在目标窗体中显示的信息的方式。

 下表描述了中可用的属性**自定义操作**对话框。

|属性|描述|
|--------------|-----------------|
|**AddressLike**|指定将如何处理目标窗体。|
|**正文**|指定如何对原始项的正文追加到目标窗体。|
|**启用**|指示是否启用自定义操作。 如果此属性设置为**false**，自定义操作将被禁用。|
|**方法**|执行自定义操作时，请指定可用的响应的类型。 自定义操作可发送窗体中，打开窗体，或提示用户，他们想要发送还是打开窗体。|
|**名称**|指定可用于引用此自定义操作代码中的内部名称。|
|**ShowOnRibbon**|指示是否对原始项的功能区上显示的自定义操作。|
|**SubjectPrefix**|指定的目标窗体的主题行的开始处插入的文本。|
|**TargetForm**|指定目标窗体的 message 类名。 例如，键入**IPM。任务**以打开任务窗体。|
|**标题**|指定自定义操作按钮的标签。|

## <a name="customize-a-custom-action-at-runtime"></a>自定义在运行时的自定义操作
 此外可以使用代码的自定义操作中添加行为。 例如，可以添加代码，使用电子邮件收件人的名称并将这些名称添加为与会者中新的约会项。 若要执行此操作，处理[CustomAction](/office/vba/api/Outlook.MailItem.CustomAction)的事件[MailItem 对象](/office/vba/api/Outlook.MailItem)。

## <a name="see-also"></a>请参阅
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [将窗体区域与 Outlook 消息类相关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
