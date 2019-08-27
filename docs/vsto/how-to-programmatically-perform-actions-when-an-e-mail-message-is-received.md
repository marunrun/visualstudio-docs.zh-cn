---
title: 以编程方式执行操作，如果收到电子邮件消息
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], actions when e-mail is received
- NewMail event
- mail items [Office development in Visual Studio], custom actions
- e-mail [Office development in Visual Studio], custom actions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a0787db2f7055bc65871227b9fcf8cbbb60ec1d8
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402200"
---
# <a name="how-to-programmatically-perform-actions-when-an-email-message-is-received"></a>如何：以编程方式执行操作时收到一封电子邮件
  此示例执行自定义操作时用户会收到一封电子邮件。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-vb[Trin_Outlook_RL_PerformActions#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_PerformActions/thisaddin.vb#1)]
 [!code-csharp[Trin_Outlook_RL_PerformActions#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_PerformActions/thisaddin.cs#1)]

## <a name="see-also"></a>请参阅
- [如何：Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)
- [使用邮件项](../vsto/working-with-mail-items.md)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
