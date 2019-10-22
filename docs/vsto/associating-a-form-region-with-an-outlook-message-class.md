---
title: 将窗体区域与 Outlook 邮件类关联
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.InvalidMessageClassName
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FormRegionMessageClassAttribute
- form regions [Office development in Visual Studio], message classes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 45db262b6bf7843a3893c5d60f0b6eaea5fcb70b
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254580"
---
# <a name="associate-a-form-region-with-an-outlook-message-class"></a>将窗体区域与 Outlook 邮件类关联
  您可以通过将窗体区域与每个项的 message 类关联来指定哪些 Microsoft Office Outlook 项显示窗体区域。 例如，如果要将窗体区域追加到邮件项的底部，可以将窗体区域与`IPM.Note` message 类相关联。

 若要将窗体区域与 message 类关联，请在 "**新建 Outlook 窗体区域**" 向导中指定邮件类名称，或将属性应用于窗体区域工厂类。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="understand-outlook-message-classes"></a>了解 Outlook 邮件类
 Outlook 邮件类标识 Outlook 项的类型。 下表列出了这8种标准类型的项及其消息类名称。

|Outlook 项类型|Message 类名称|
|-----------------------|------------------------|
|AppointmentItem|`IPM.Appointment`|
|ContactItem|`IPM.Contact`|
|DistListItem|`IPM.DistList`|
|JournalItem|`IPM.Activity`|
|MailItem|`IPM.Note`|
|PostItem|`IPM.Post` 或 `IPM.Post.RSS`|
|TaskItem|`IPM.Task`|

 您还可以指定自定义邮件类的名称。 自定义邮件类标识你在 Outlook 中定义的自定义窗体。

> [!NOTE]
> 对于替换和全部替换窗体区域，您可以指定新的自定义邮件类名称。 不需要使用现有自定义窗体的 message 类名称。 自定义邮件类的名称必须是唯一的。 确保名称唯一的一种方法是使用类似于下面的命名约定：\<*StandardMessageClassName*>。*公司 >* 。 \<MessageClassName > （例如： `IPM.Note.Contoso.MyMessageClass`）。 \<

## <a name="associate-a-form-region-with-an-outlook-message-class"></a>将窗体区域与 Outlook 邮件类关联
 可以通过两种方法将窗体区域与邮件类相关联：

- 使用 "**新建 Outlook 窗体区域**" 向导。

- 应用类属性。

### <a name="use-the-new-outlook-form-region-wizard"></a>使用 "新建 Outlook 窗体区域" 向导
 在 "**新建 Outlook 窗体区域**" 向导的最后一页上，可以选择 "标准邮件类"，并键入要与窗体区域关联的自定义邮件类的名称。

 如果窗体区域设计为替换整个窗体或窗体的默认页，则标准消息类不可用。 只能为向窗体添加新页的窗体或附加到窗体底部的窗体指定标准邮件类名称。 有关详细信息，请参阅[如何：向 Outlook 外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)添加窗体区域。

 若要包括一个或多个自定义邮件类，请在 "**哪些自定义邮件类将显示此窗体区域？** " 框中键入其名称。

 键入的名称必须符合以下准则：

- 使用完全限定的 message 类名（例如：IPM.请注意，Contoso "）。

- 使用分号分隔多个邮件类名称。

- 不要包含标准 Outlook 邮件类，例如 "IPM。备注 "或" IPM。Contact "。 仅包括自定义邮件类，例如 "IPM。请注意，Contoso "。

- 不要单独指定基本消息类（例如："IPM"）。

- 对于每个邮件类名称，不要超过256个字符。

  单击 "**完成**" 时，"**新建 Outlook 窗体区域**" 向导将验证输入的格式。

> [!NOTE]
> "**新建 Outlook 窗体区域**" 向导不会验证您提供的邮件类名称是正确的还是有效的。

 完成向导后，"**新建 Outlook 窗体区域**" 向导会将特性应用于包含指定的消息类名称的窗体区域类。 你还可以手动应用这些属性。

### <a name="apply-class-attributes"></a>应用类特性
 完成 "**新建 Outlook 窗体区域**" 向导后，可以将窗体区域与 Outlook 邮件类关联。 为此，请将特性应用于窗体区域工厂类。

 下面的示例演示了<xref:Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute>已应用于名为`myFormRegion`的窗体区域工厂类的两个特性。 第一个属性将窗体区域与邮件邮件窗体的标准邮件类相关联。 第二个属性将窗体区域与名为`IPM.Task.Contoso`的自定义邮件类相关联。

 [!code-vb[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Attributes/FormRegion1.vb#1)]
 [!code-csharp[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Attributes/FormRegion1.cs#1)]

 特性必须符合以下准则：

- 对于自定义邮件类，请使用完全限定的消息类名称（例如：IPM.请注意，Contoso "）。

- 不要单独指定基本消息类（例如："IPM"）。

- 对于每个邮件类名称，不要超过256个字符。

- 如果窗体区域替换整个窗体或窗体的默认页，则不要包含标准消息类的名称。 只能为向窗体添加新页的窗体或附加到窗体底部的窗体指定标准邮件类名称。 有关详细信息，请参阅[如何：向 Outlook 外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)添加窗体区域。

  生成项目时，Visual Studio 将验证邮件类名称的格式。

> [!NOTE]
> Visual Studio 不会验证您提供的消息类名称是正确的还是有效的。

## <a name="see-also"></a>请参阅
- [在运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [创建 Outlook 窗体区域的准则](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [窗体名称和消息类概述](/office/vba/outlook/Concepts/Forms/form-name-and-message-class-overview)
- [Outlook 窗体和项如何协同工作](/office/vba/outlook/Concepts/Forms/how-outlook-forms-and-items-work-together)
