---
title: 将窗体区域与 Outlook 消息类相关联
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
ms.openlocfilehash: 5c264048887d3a1ba77d498784dc3e6cc4384159
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440367"
---
# <a name="associate-a-form-region-with-an-outlook-message-class"></a>将窗体区域与 Outlook 消息类相关联
  您可以指定哪些 Microsoft Office Outlook 项显示的窗体区域，通过将窗体区域与每个项的消息类相关联。 例如，如果你想要将窗体区域附加到邮件项的底部，则可以将窗体区域与`IPM.Note`message 类。

 若要将与 message 类关联的窗体区域，指定在的 message 类名**新建 Outlook 窗体区域**向导或将属性应用于窗体区域工厂类。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="understand-outlook-message-classes"></a>了解 Outlook message 类
 Outlook 邮件类标识的 Outlook 项的类型。 下表列出了这些八个标准类型的项和其 message 类名称。

|Outlook 项类型|Message 类名|
|-----------------------|------------------------|
|AppointmentItem|`IPM.Appointment`|
|ContactItem|`IPM.Contact`|
|DistListItem|`IPM.DistList`|
|JournalItem|`IPM.Activity`|
|MailItem|`IPM.Note`|
|PostItem|`IPM.Post` 或 `IPM.Post.RSS`|
|TaskItem|`IPM.Task`|

 此外可以指定自定义 message 类的名称。 自定义邮件类标识在 Outlook 中定义的自定义窗体。

> [!NOTE]
> 对于替换和全部替换窗体区域，可以指定新的自定义邮件类名称。 不需要使用现有的自定义窗体的 message 类名。 自定义邮件类的名称必须是唯一的。 请确保该名称是唯一的一种方法是使用类似于下面的命名约定：\<*标准邮件类名称*>。\<*公司*>。\<*MessageClassName*> (例如： `IPM.Note.Contoso.MyMessageClass`)。

## <a name="associate-a-form-region-with-an-outlook-message-class"></a>将窗体区域与 Outlook 消息类相关联
 有两种方法来将窗体区域的邮件类与相关联：

- 使用**新建 Outlook 窗体区域**向导。

- 应用类属性。

### <a name="use-the-new-outlook-form-region-wizard"></a>使用新建 Outlook 窗体区域向导
 在最后一页**新建 Outlook 窗体区域**向导，您可以选择标准的 message 类并键入你想要将与窗体区域关联的自定义 message 类的名称。

 标准邮件类不可用，如果窗体区域设计为替换整个窗体或窗体的默认页。 可以指定仅为窗体，将新页面添加到窗体或，附加到窗体的底部标准邮件类名称。 有关详细信息，请参阅[如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

 若要包含一个或多个自定义邮件类，请在**哪些自定义邮件类将显示此窗体区域？** 框。

 您键入的名称必须符合以下准则：

- 使用完全限定的邮件类名称 (例如："IPM。Note.Contoso")。

- 使用分号分隔多个邮件类名称。

- 不包括标准 Outlook message 类，如"IPM。请注意"或者"IPM。联系"。 仅包括自定义邮件类，如"IPM。Note.Contoso"。

- 不指定基的 message 类本身 (例如："IPM")。

- 不能超过 256 个字符的每个邮件类名称。

  **新建 Outlook 窗体区域**单击时，向导将验证你输入的格式**完成**。

> [!NOTE]
> **新建 Outlook 窗体区域**向导不会验证你提供的邮件类名称是否正确或有效。

 完成向导后**新建 Outlook 窗体区域**向导将特性应用于包含指定的邮件类名称的窗体区域类。 您还可以手动应用这些属性。

### <a name="apply-class-attributes"></a>将应用类特性
 在完成后，你可以使用 Outlook 邮件类关联的窗体区域**新建 Outlook 窗体区域**向导。 若要执行此操作，请将特性应用于窗体区域工厂类。

 下面的示例演示两个<xref:Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute>已应用于名为的窗体区域工厂类的属性`myFormRegion`。 第一个属性将与邮件窗体一个标准邮件类关联窗体区域。 第二个属性将与名为的自定义邮件类关联窗体区域`IPM.Task.Contoso`。

 [!code-vb[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Attributes/FormRegion1.vb#1)]
 [!code-csharp[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Attributes/FormRegion1.cs#1)]

 属性必须符合以下准则：

- 对于自定义邮件类使用完全限定的邮件类名称 (例如："IPM。Note.Contoso")。

- 不指定基的 message 类本身 (例如："IPM")。

- 不能超过 256 个字符的每个邮件类名称。

- 如果窗体区域替换整个窗体或窗体的默认页，则不包括标准的 message 类的名称。 可以指定仅为窗体，将新页面添加到窗体或，附加到窗体的底部标准邮件类名称。 有关详细信息，请参阅[如何：向 Outlook 外接程序项目添加窗体区域](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

  生成项目时，visual Studio 会验证 message 类名的格式。

> [!NOTE]
> Visual Studio 不会验证你提供的邮件类名称正确或有效。

## <a name="see-also"></a>请参阅
- [访问在运行时的窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计 Outlook 窗体区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [若要创建 Outlook 窗体区域的准则](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [窗体名称和 message 类概述](/office/vba/outlook/Concepts/Forms/form-name-and-message-class-overview)
- [Outlook 窗体和项如何协同工作](/office/vba/outlook/Concepts/Forms/how-outlook-forms-and-items-work-together)
