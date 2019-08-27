---
title: 如何：以编程方式发送电子邮件
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], sending e-mail
- Outlook [Office development in Visual Studio], creating e-mail
- Outlook [Office development in Visual Studio], sending e-mail
- e-mail [Office development in Visual Studio], sending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 72d033add2ba8320b14eebd5af700ab225d34410
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551752"
---
# <a name="how-to-programmatically-send-email"></a>如何：以编程方式发送电子邮件
  此示例向其电子邮件地址中具有域名**example.com**的联系人发送电子邮件。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_ProgramEmail#1](../vsto/codesnippet/CSharp/Trin_OL_ProgramEMail/thisaddin.cs#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 其电子邮件地址中具有域名**example.com**的联系人。

## <a name="robust-programming"></a>可靠编程
 请勿删除搜索域名**example.com**的筛选器代码。 如果删除筛选器, 你的解决方案将向你的所有联系人发送电子邮件。

## <a name="see-also"></a>请参阅
- [使用邮件项](../vsto/working-with-mail-items.md)
- [如何：以编程方式创建电子邮件项](../vsto/how-to-programmatically-create-an-e-mail-item.md)
- [如何：以编程方式访问 Outlook 联系人](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [如何：收到电子邮件时, 以编程方式执行操作](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
