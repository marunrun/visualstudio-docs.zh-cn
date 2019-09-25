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
ms.openlocfilehash: 817cf9fe8698c2908e873246a8971f90fe72b460
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254444"
---
# <a name="custom-actions-in-outlook-form-regions"></a>Outlook 窗体区域中的自定义操作
  操作显示使用户能够响应 Microsoft Office Outlook 项目的按钮。 例如，若要对邮件项做出响应，用户可单击 "**答复**"、"**全部答复**" 或 "**转发**" 操作按钮。 其中每个操作都将创建一个新的邮件项，并使用原始项中的信息填充该项的字段。

 你可以创建一个自定义操作，该操作将打开任何类型的 Outlook 项。 例如，你可以添加一个打开新约会或任务项的自定义操作。 设置自定义操作的属性，或使用自定义代码填充新项的字段。 自定义操作显示在 Outlook 检查器窗口中打开的项的 "**自定义操作**" 下拉菜单中。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-custom-actions-to-a-form-region"></a>向窗体区域添加自定义操作
 若要向窗体区域添加自定义操作，请使用 "**自定义操作**" 对话框。 您可以通过解决方案资源管理器**在 "** 属性" 窗口中选择窗体区域，展开 "**属性" 窗口**中的 "**清单**" 节点，选择**CustomActions**属性，然后单击省略号按钮（![ASP.NET mobile 设计器 "椭圆形](../sharepoint/media/mwellipsis.gif "ASP.NET mobile 设计器\" 椭圆")）。

 您可以使用 "**自定义操作**" 对话框指定*目标窗体*。 目标窗体是用户执行自定义操作时显示的窗体。

 您还可以使用 "**自定义操作**" 对话框指定您希望原始项中的信息在目标窗体中的显示方式。

 下表介绍了 "**自定义操作**" 对话框中可用的属性。

|属性|描述|
|--------------|-----------------|
|**AddressLike**|指定将如何处理目标窗体。|
|**正文**|指定将原始项的正文追加到目标窗体的方式。|
|**启用**|指示是否已启用自定义操作。 如果将此属性设置为**false**，则禁用自定义操作。|
|**方法**|指定执行自定义操作时可用的响应类型。 自定义操作可以发送窗体，打开窗体，或提示用户是否要发送或打开窗体。|
|**Name**|指定可用于在代码中引用此自定义操作的内部名称。|
|**ShowOnRibbon**|指示是否在原始项的功能区中显示自定义操作。|
|**SubjectPrefix**|指定在目标窗体的主题行的开头插入的文本。|
|**TargetForm**|指定目标窗体的 message 类名称。 例如，键入**IPM。** 用于打开任务窗体的任务。|
|**标题**|指定自定义操作按钮的标签。|

## <a name="customize-a-custom-action-at-run-time"></a>在运行时自定义自定义操作
 你还可以使用代码将行为添加到自定义操作。 例如，你可以添加采用电子邮件收件人名称的代码，并在新约会项中将这些姓名添加为与会者。 为此，请处理[MailItem 对象](/office/vba/api/Outlook.MailItem)的[CustomAction](/office/vba/api/Outlook.MailItem.CustomAction)事件。

## <a name="see-also"></a>请参阅
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [将窗体区域与 Outlook 邮件类关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
