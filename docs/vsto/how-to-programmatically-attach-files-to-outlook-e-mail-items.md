---
title: 如何：以编程方式将文件附加到 Outlook 电子邮件项
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], attachments
- e-mail [Office development in Visual Studio], attachments
- mail items [Office development in Visual Studio], attachments
- attachments [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 707c3bb2b6bec9f8db1744d1f28acd4e90a45a57
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62575619"
---
# <a name="how-to-programmatically-attach-files-to-outlook-email-items"></a>如何：以编程方式将文件附加到 Outlook 电子邮件项
  此示例将文件附加到新的邮件项，并将其发送到 Armando Pinto。 该示例假定一个人名叫 Armando Pinto 存在作为接收方。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_Outlook_RL_AttachFiles#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_AttachFiles/thisaddin.cs#1)]
 [!code-vb[Trin_Outlook_RL_AttachFiles#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_AttachFiles/thisaddin.vb#1)]

## <a name="see-also"></a>请参阅
- [使用邮件项](../vsto/working-with-mail-items.md)
- [如何：以编程方式发送电子邮件](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [如何：以编程方式保存 Outlook 电子邮件项的附件](../vsto/how-to-programmatically-save-attachments-from-outlook-e-mail-items.md)
- [如何：以编程方式创建电子邮件项](../vsto/how-to-programmatically-create-an-e-mail-item.md)
