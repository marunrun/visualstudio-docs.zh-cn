---
title: 如何：以编程方式将文件附加到 Outlook 电子邮件项
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: a6cde83fa59f45cbc45e56738f09ccf3099f5c02
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546128"
---
# <a name="how-to-programmatically-attach-files-to-outlook-email-items"></a>如何：以编程方式将文件附加到 Outlook 电子邮件项
  此示例将文件附加到新的邮件项，并将其发送给 Armando Pinto。 该示例假定名为 Armando Pinto 的人员作为接收方存在。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_Outlook_RL_AttachFiles#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_AttachFiles/thisaddin.cs#1)]
 [!code-vb[Trin_Outlook_RL_AttachFiles#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_AttachFiles/thisaddin.vb#1)]

## <a name="see-also"></a>另请参阅
- [使用邮件项](../vsto/working-with-mail-items.md)
- [如何：以编程方式发送电子邮件](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [如何：以编程方式保存 Outlook 电子邮件项的附件](../vsto/how-to-programmatically-save-attachments-from-outlook-e-mail-items.md)
- [如何：以编程方式创建电子邮件项](../vsto/how-to-programmatically-create-an-e-mail-item.md)
