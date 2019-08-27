---
title: 以编程方式在联系人中查找电子邮件地址
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- e-mail [Office development in Visual Studio], searching
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 26e32314db68ae064edac5537222447625cb051d
ms.sourcegitcommit: 7eb2fb21805d92f085126f3a820ac274f2216b4e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2019
ms.locfileid: "67328971"
---
# <a name="how-to-programmatically-search-for-an-email-address-in-contacts"></a>如何：以编程方式在联系人中的电子邮件地址搜索
  以下示例将在联系人文件夹搜索电子邮件地址中具有域名 **example.com** 的联系人。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_SearchEmail#1](../vsto/codesnippet/CSharp/Trin_OL_SearchEmail/thisaddin.cs#1)]

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 电子邮件地址中具有域名 **example.com** （例如， `somebody@example.com`且具有的名字和姓氏的联系人。

## <a name="see-also"></a>请参阅
- [使用联系人项](../vsto/working-with-contact-items.md)
- [如何：以编程方式发送电子邮件](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [如何：以编程方式访问 Outlook 联系人](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [如何：以编程方式将条目添加到 Outlook 联系人](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
